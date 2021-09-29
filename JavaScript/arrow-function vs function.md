## Arrow Function이란?

- ES6부터 추가된 표현
- function 표현에 비해 구문이 짧다.
- 자신의 this, arguments, super 또는 new.target을 바인딩 하지 않는다.
- **항상 익명 함수**이다.
- 메소드 함수가 아닌 곳에 적합하다. 그래서 생성자로 사용할 수 없다.

## this를 바인딩 하지 않는다는 의미는?

arrow function은 자신을 포함하는 외부 scope에서 this를 계승받는다.   
즉, arrow function은 자신만의 this를 생성하지 않는다. (자신을 포함하고 있는 context의 this를 이어받는다.)

아래의 코드를 보자. 아래의 코드는 undefined를 출력하고 있다. 콜백함수(setTimeout) 내부의 this는 전역객체 window를 가리킨다.   
myVar 속성은 window 속성이 아니라 obj의 속성이기 떄문에 undefined가 출력되는 것이다.
```javascript
let obj={
    myVar :'foo',
    myFunc : function(){
        console.log(this.myVar);
        setTimeout(function(){
            console.log(this.myVar);
        },1000);
    }
}

obj.myFunc() // foo , undefined
```

이것을 해결하기 위한 3가지 방법을 알아보자.

1. this를 변수에 할당하기

```javascript
let obj={
    myVar : 'foo',
    myFunc:function(){
        let self = this;
        console.log(this.myVar);
        setTimeout(function(){
            console.log(self.myVar);
        },1000)
    }
}
obj.myFunc() // foo .. foo
```

2. bind, call apply를 사용하기

this는 자바스크립트에서 조금 골치아픈 존재이다.   
그리고 경우에 따라 this가 가리키는것이 바뀔 경우가 생긴다. 그렇기 때문에 this를 고정시키는 방법이 존재한다.   
이를 this 바인딩이라고 한다.

```javascript
let obj={
    myVar= 'foo',
    myFunc : function(){
        console.log(this.myVar);
        setTimeout(function(){
            console.log(this.myVar);

        }.bind(this),1000)
    }
}
obj.myFunc() //foo...foo
```

3. arrow function 사용하기

arrow function은 자신만의 this를 생성하지 않는다. (자신을 포함하고 있는 context의 this를 이어받는다.)
```javascript
let obj={
    myVar :'foo',
    myFunc:function(){
        console.log(this.myVar);
        setTimeout(()=>{
            console.log(this.myVar);
        },1000)
    }
}
obj.myFunc() // foo ... foo
```