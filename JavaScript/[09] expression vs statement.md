# 표현식과 문

## 값(value)

값은 표현식이 평가되어 생성된 결과를 말한다.

```js
var x = 10 + 20;
```

위 코드에서 `x`라는 변수에 할당되는것은 10+20이 아니라 `계산된 결과인 30이다.` 즉 x가 가르키고있는 메모리 공간에 저장되는것은 10+20이 아닌 **평가된 값 30이다.**

## 리터럴

리터럴은 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용해 값을 생성하는 표기법이다.

```js
100 //정수 리터럴
10.5 //부동 소수점 리터럴
'hello' //문자열 리터럴
true //불리언 리터럴
{name : 'hello'} //객체 리터럴
[1,2,3] //배열 리터럴
function(){} //함수 리터럴
```

이 처럼 리터럴은 데이터를 표현하는 방식이다.

## 표현식

표현식(expression)은 **값으로 평가될 수 있는 문**이다.  
즉 표현식이 평가되면 새로운 값을 생성하거나 기존 값을 참조한다.
(리터럴도 값으로 표현되기 때문에 표현식이다.)

```js
2 + (2 * 3) / 2(Math.random() * (100 - 20)) + 20;

functionCall();

window.history ? useHistory() : noHistoryFallback();

1 + 1, 2 + 2, 3 + 3;

declaredVariable;

true && functionCall();

true && declaredVariable;
```

위의 코드들은 모두 표현식이다. 그리고 표현식은 자바스크립트 코드 중 값이 들어가는 곳이면 어디에나 넣을 수 있다.

## 표현식은 반드시 상태(state)를 바꿀 필요가 없다.

```js
const assignedVariable = 2; // 이건 문장(Statement)입니다. assignedVariable은 상태입니다.

assignedVariable * 4; // 표현식(Expression)입니다.

assignedVariable * 10; // 표현식(Expression)입니다.

assignedVariable - 10; // 표현식(Expression)입니다.

console.log(assignedVariable); // 2
```

## 문

문(statement)은 프로그램을 구성하는 기본 단위이자 최소 실행단위이다.
문의 집합으로 이루어진 것이 프로그램이며, 문을 작성하고 순서에 맞게 나열하는 것이 프로그래밍이다.

```js
//문을 명령문이라고도 부른다
var x ; //변수 선언문
x = 5; //표현식 문(할당문)
function foo(){} //함수 선언문
if(x >1) console.log(x) //조건문
for(){} //반복문
}
```

세미콜론 `;`는 문의 종료를 나타낸다.

### 표현식인 문과 표현식이 아닌 문

```js
var x; //변수 선언문이지만 값이 할당되지 않았기 때문에 표현식이 아니다.

x = 100; // 할당문이면서 표현식이다.
```
