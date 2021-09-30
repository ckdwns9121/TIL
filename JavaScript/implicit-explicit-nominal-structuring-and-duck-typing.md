## 타입변환

### 암묵적 타입변환

암묵적 타입변환이란 자바스크립트에서 타입을 받았을 때 예상 가능한 타입으로 바꿔주는것이다.

지정해놓은 타입에 다른 타입을 넣을수도 있기때문에 자바스크립트 엔진은 사용자가 잘못 넣은 타입을 올바른 타입으로 변환하려고 시도한다. 이것은 자바스크립트의 중요한(편한) 기능중 하나이며 프로젝트 사이즈가 커지고 유지보수가 어려워 질 수록 이러한 편한 기능들은 오히려 독이될 수도 있으니 조심하자(타입스크립트 쓰는 이유)

```javascript
let a= 5;
let b= '5';
console.log(a*b) // 25;

true + true //2
10-true //9

```

```
number + number // number
number + string // string
string + string // string
number + boolean // number
```

다른 연산자(-,/,*,%)는 number형이 string보다 우선시 되기 때문에 더하기와 같은 문자열로 변환이 일어나지 않는다. (문자<숫자)

```
//다른 연산자(-,*,/,%)
string * number // number
string * string // number
number * number // number
string * boolean //number
number * boolean //number
“2” * false; //0
2 * true; //2
```

### 명시적타입 변환

명시적 변환이란 개발자가 의도를 가지고 데이터 타입을 변환시키는 것이다.

타입을 변경하는 기본적인 방법은 `Object(), Number(),String(),Boolean()` 과 같은 함수를 사용한다.


1. string to number

숫자를 이용한 식에서 **string**을 피연산자로 전달할 때, 숫자만 포함된 string을 number로 변환되고 이외의 다른 문자열을 포함하면 NaN으로 변환된다.

```javascript
Number('1') //1
Number('3' * 3 ) //9
Number("3.14") //1.34
Number("1 + hello") //NaN
```


2. number to string

```javascript
String(123) // "123"
String(123.456) // "123.456"

```