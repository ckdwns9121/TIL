## Lexical Scope

1. 렉시컬스코프란?
- 함수를 어디서 호출하는지가 아니라 어디에 선언하였는지에 따라 결정되는 것.
- 함수를 어디에 선언하였는지에 따라 상위 스코프를 결정한다는 뜻.
- 가장 중요한점은 함수의 호출이 아니라 함수의 선언에 따라 결정되는 것.
- 다른 말로 정적 스코프라고 부름 

```javascript

    var x=1; //global
    function test(){
        var x=10;
        second();
    }
    
    function second(){
        console.log(x);
    }

    test(); //1
    second(); //1
```

### 1과 1이 출력되는 이유는?

자바스크립트에서는 위와 같은 코드를 작성할 때, 이미 실행 단계에서 코드들의 스코프를 결정한다.   

- global 범위에 있는 변수 x
- test() 함수 안에 있는 변수 x
- second() 함수 안에 있는 변수 x


