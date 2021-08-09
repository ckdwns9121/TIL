## 클로저

- 클로저는 자바스크립트에서 매우 중요한 개념.    
- 클로저는 자바스크립트내의 고유 개념이 아닌 함수형 언어의 중요한 특성이다.

1. 클로저의 개념
- 클로저는 함수와 그 함수가 선언됐을 때의 렉시컬 환경과의 조합이다.

```javascript
    function outerFunc(){
        var x = 10;
        var innerFunc = function(){ console.log(x);};
        innerFunc();
    }

    outerFunc(); // 10
```

함수 outerFunc내에서 내부함수 innerFunc가 선언되고 호출되었다. 이때 내부함수 innerFunc은 자신을 포함하고있는 외부함수 outerFunc의 변수 x에 직접 접근 할 수 있다. 이는 함수 innterFunc가 함수 outerFunc 내부에 선언됐기 때문이다.


```
    스코프는 함수를 호출할 때가 아니라 어디에 선언하였는지에 따라 결정된다.   
    이를 렉시컬 스코핑(Lexical Scoping)이라 한다. 위 함수 innerFunc은   
    함수 outerFunc의 내부에서 선언되었기 때문에 함수 innerFunc의 상위 스코프는
    outerFunc이다. 함수 innerFunc가 전역에 선언되었다면 함수 innerFunc의 상위스코프는 전역 스코프가 된다.
```


내부함수 innerFunc을 반환하도록 작성해보자.

```javascript
   function outerFunc(){
        var x = 10;
        var innerFunc = function(){ console.log(x);};
        return innerFunc;
    }

    var inner = outerFunc();
    inner();// 10

```


함수 outerFunc은 내부 함수 innterFunc을 반환하고 끝났다.   즉, 함수 outerFunc은 실행된 이후 콜스택(실행 컨텍스트 스택)에서 제거되었으므로 함수 ouuterFunc의 변수 x또한 더이상    유효하지 않게되어 변수 x에 접은할 수 있는 방법은 없어보인다.   그러나 위의 코드는 변수 x값인 10이다. 이미 life-cycle이 종료되어 시행 컨텍스트 스택에서 제거된 함수 outerFunc의 지역변수 x가 살아있다.


이처럼 자신을 포함하고 있는 외부함수보다 내부함수가 더 오래 유지되는 경우, 외부 함수 밖에서 내부함수가 호출되더라도 외부함수의 지역 변수에 접근할 수 있는데 이러한 함수를 클로저라고 부른다.



2. 클로저의 활용

- 클로저는 자신이 생성될 떄의 환경을 기억해야하므로 메모리 차원에서 손해를 볼 수 있다. 하지만 클로저는 자바스크립트의 강력한 기능이므로 이를 적극 활용 하여야한다.

## 상태유지

클로저가 가장 유용하게 사용되는 상황은 현재상태를 기억하고 변경된 최신상태를 유지하는것.


```javascript
    <!DOCTYPE html>
    <html>
    <body>
    <button class="toggle">toggle</button>
    <div class="box" style="width: 100px; height: 100px; background: red;"></div>

    <script>
        var box = document.querySelector('.box');
        var toggleBtn = document.querySelector('.toggle');

        var toggle = (function () {
        var isShow = false;

        // ① 클로저를 반환
        return function () {
            box.style.display = isShow ? 'block' : 'none';
            // ③ 상태 변경
            isShow = !isShow;
        };
        })();

        // ② 이벤트 프로퍼티에 클로저를 할당
        toggleBtn.onclick = toggle;
    </script>
    </body>
    </html>
```


1. 즉시실행함수는 함수를 반환하고 즉시 소멸한다. 즉시실행함수가 반환하는 함수는 자신이 실행됐을 때의 렉시컬 환경에 속한 변수 isShow를 기억하는 클로저이다.

2. 클로저를 이벤트 핸들러로서 이벤트 프로퍼티에 할당하였다. 이벤트 프로퍼티에서 클로저를 제거하지 않는 한 클로저가 기억하는 렉시컬 환경의 변수 isShow는 소멸하지 않는다. 다시말해 현재상태를 기억한다.

3. 버튼을 클릭하면 이벤트 핸들러인 클로저가 호출된다. 이때 isShow값이 변경된다. isShow는 클로저에의해 참조되고 있기 때문에 유효하며 자신의 변경된 최신상태를 계속해서 유지한다.


만약 자바스크립트에 클로저라는 기능이 없다면 전역변수를 선언해서 사용해야 할 것이다.    
전역변수는 누구든 어디서 접근가능하기 때문에 오류를 발생시킬 수 있다.