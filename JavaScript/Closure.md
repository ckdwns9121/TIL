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

```
함수 outerFunc은 내부 함수 innterFunc을 반환하고 끝났다. 즉, 함수 outerFunc은 실행된 이후 콜스택(실행 컨텍스트 스택)에서 제거되었으므로 함수 ouuterFunc의 변수 x또한 더이상 유효하지 않게되어 변수 x에 접은할 수 있는 방법은 없어보인다.   그러나 위의 코드는 변수 x값인 10이다. 이미 life-cycle이 종료되어 시행 컨텍스트 스택에서 제거된 함수 outerFunc의 지역변수 x가 살아있다.
```

```
이처럼 자신을 포함하고 있는 외부함수보다 내부함수가 더 오래 유지되는 경우, 외부 함수 밖에서 내부함수가 호출되더라도 외부함수의 지역 변수에 접근할 수 있는데 이러한 함수를 클로저라고 부른다.
```

