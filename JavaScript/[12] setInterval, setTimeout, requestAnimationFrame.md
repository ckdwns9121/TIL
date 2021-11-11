## setTimeout, setInterval and requestAnimationFrame

### 자바스크립트에서 스케쥴링
자바스크립트에서는 스케쥴링을 위한 **타이머 함수**가 존재한다.

- setTimeout : 일정 시간 후 fn으로 받은 함수를 실행한다.
- setInterval : 일정 시간 동안 fn으로 받은 함수를 반복 실행한다.
- clearTimeout(id) : 실행되고 있는 id 값의 timeout을 중지
- clearInterval(id) : 실행되고 있는 id 값의 interval을 중지

타이머 함수는 자바스크립트의 스펙이 아닌 브라우저 API(webAPIs)에서 제공하는 기능이다. (node.js도 제공)

### setTimeout
기본 구성
```js
let timerId = setTimeout(func|code, [delay], [arg1], [arg2], ...);
```
1초뒤 `sayHello()` 함수 실행
```js
function sayHello() {
  alert('Hello!')
}

setTimeout(sayHello, 1000)
```
인자가 있는 경우
```js
function sayHello(name) {
  alert('Hello ' + name + '!')
}

setTimeout(sayHello, 1000, 'Minsu')
```

### clearTimeout
clearTimeout으로 스케쥴링 취소하기
```js
let timerId = setTimeout(...);
clearTimeout(timerId);
```
아래의 코드를 실행시키면 브라우저에서의 timerId는 number이다. node.js에서는 추가적인 메소드를 제공하고 timer object를 반환시킨다.
```js
let timerId = setTimeout(() => alert('Nothing happens...'), 1000)
alert(timerId)

clearTimeout(timerId)
alert(timerId)
```
`1000ms`뒤에 실행시키기로 했던 스케쥴이 clearTimeout으로 인해 취소되었다. alert로 확인한 결과 취소되더라도 timerId는 null이 되지 않는다.

### setInterval

```js
let timerId = setInterval(func|code, [delay], [arg1], [arg2], ...);
```
모든 인자는 `setTimeout`과 똑같은 인자를 갖는다.

```js
let timerId = setInterval(() => console.log('tick'), 2000)

setTimeout(() => {
  clearInterval(timerId)
  console.log('stop')
}, 5000)
```

setTimeout으로 setInterval을 구현하려면 재귀함수로 구현할 수 있다.

```js
let timerId = setTimeout(function tick() {
  console.log('tick')
  timerId = setTimeout(tick, 2000)
}, 2000)
```

### requestAnimationFrame
자바스크립트에서 애니메이션을 구현할때 new Date()를 사용한 타이머를 이용한다. 시작지점과 종료시점을 변수에 저장해 반복실행하는 방법인데 이러한 방법은 호출 스택이 지나치게 많다는 단점이 존재한다.

`requestAnimationFrame`은 `setInterval`의 딜레이를 매우 작게 했을 때 요청이 지연되는 문제를 해결할 수 있는 메소드다.

```js
function repeatOften() {
  // Do whatever
  requestAnimationFrame(repeatOften);
}
requestAnimationFrame(repeatOften);
```

장점은 브라우저에 최적화 할 수 있어 부드러운 애니메이션 효과를 적용할 수 있다.