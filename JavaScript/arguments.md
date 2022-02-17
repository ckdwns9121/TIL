# arguments

## 매개변수(parameter)와 인자(arguments)의 차이

자바스크립트의 함수에서 arguments는 배열은 아니지만 `유사 배열`이라고 부른다.

아래의 코드에서 함수 test의 매개변수는 test이고 인자는 'hello'이다.

```javascript
function test(message) {
  console.log(message);
}
test('hello');
```

## arguments 예제

아래 코드는 인자로 전달된 모든 값을 더해 리턴하는 sum함수이다.  
그런데 sum함수는 정확히 어떤 매개변수를 정의하지 않았다.
그런데도 출력결과는 10이나온다. 그 이유는 arguments라는 유사배열이 있기 때문이다.

arguments.length를 통해 함수로 전달된 인자의 개수를 알 수 있다.

```javascript
function sum() {
  var result = 0;
  for (var i = 0; i < arguments.length; i++) {
    result += arguments[i];
  }
  return result;
}
console.log(sum(1, 2, 3, 4)); //10
```
