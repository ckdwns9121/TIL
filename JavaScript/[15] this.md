## this에 대해알아보자

### 1. this란
> **this**는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수이다. this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메소드를 참조할 수 있다.

### 2. this의 이해
그렇다면 이 this값은 어떤 상황에서 어떻게 변할까? this 바인딩을 통해 this가 어떤 값과 연결되는지 확인해볼 수 있다.   
this 바인딩은 4가지 상황에서 각자 다르게 적용된다.
- 일반 함수 내부
- 메서드 내부
- 생성자 함수 내부
- Call, Apply, Bind를 통한 '호출 방식'

1. 일반함수 호출
```js
console.log(this===window) //true
var a=30;
console.log(this.a); //30
function x(){
    return this;
}
x()===window ; //true;
```

2. 객체 메소드 호출시 this는 호출한 객체에 바인딩
```js
let person ={
    firstName:'Changjun',
    lastName: 'Park',

    getFullName() {
        console.log(this.firstName + this.LastName);
    }
}

person.getFullName(); // ChangejunPark
```

3. 생성자 함수로 호출시 생성자 함수가 생성할 객체에 바인딩
```js
function Person(){
    this.firstName ='Changjun',
    this.lastName='Park',

    this.start = function(){
        console.log(this.firstName + this.lastName); 
    }
}
let jone = new Person();
jone.start() // ChangjunPark
```

4. Call,Apply,Bind 메소드 사용시 메소드에 첫번째 인자로 전달하는 객체에 바인딩.


### 정리
this는 **함수 호출 방식**에 따라 동적으로 결정된다. 함수를 일반함수로 호출할 경우 this는 전역객체를, 메소드로 호출할 경우 이를 호출한 객체를, 생성자 함수를 호출할 때는 생성자 함수가 생성할 인스턴스를 가르킨다.