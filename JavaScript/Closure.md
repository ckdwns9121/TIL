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


