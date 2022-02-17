# 메세지 큐와 이벤트 루프

## 자바스크립트 동작원리

자바스크립트 엔진은 메모리 할당이 일어나는 영역인 힙영역과 코드가 실행될때 코드를 저장하는 호출 스택, 콜백함수 대기열인 큐로 구성되어있다.

## 자바스크립트 엔진

- Heap: 객체들은 힙 메모리에 할당된다. 크기가 동적으로 변하는 값들의 참조 값을 갖고 있다.
- 콜스택: 함수 호출 시, 실행 컨텍스트가 생성되며, 실행컨텍스트들이 콜스택을 구성한다.

## Web API or Browser API

브라우저 자체에 내장되어있으며 ajax, setTimeout, setInterval 등의 API를제공한다.

## 태스크 큐

콜백 큐는 스택에서 Web API에 의해 보내진 콜백함수들이 대기하는 곳이다. **호출스택이 비었을 경우** 콜백 큐에 위치한 함수들이 호출 스택으로 이동한다.

대표적으로 `setTimeout`, `setInterval` 등과 같은 이벤트 핸들러가 일시적으로 보관되는 영역이다.

## 이벤트 루프

이벤트 루프는 호출 스택과 큐를 주시하며 스택이 비어있는지 주기적으로 체크 하는 역할을 한다. 스택이 비어있으면 큐에서 콜백함수를 꺼내어 호출 스택으로 푸쉬한다.

## 마이크로 태스크 큐

`Promise`를 담는 큐  
마이크로 태스크 큐는 매크로 태스크 큐 보다 더 높은 우선 순위를 갖고있으며 태스크 큐에 대기중인 것이 있다고 하더라도 마이크로 태스크 큐에 있는 함수들이 우선실행된다.

## 더 깊은 이해

```js
function main() {
  console.log('A');
  setTimeout(
    function exec() { console.log('B'); }
  , 0);
  runWhileLoopForNSeconds(3);
  console.log('C');
}

main();

function runWhileLoopForNSeconds(sec) {
  let start = Date.now(), now = start;
  while (now - start < (sec*1000)) {
    now = Date.now();
  }
```

- 함수 `runWhileLoopForNSeconds(sec)`는 함수가 호출된 시간에서 경과된 시간을 측정하여 그 이후에 break 시키는 함수이다. while문이 계속해서 콜스택에 남아있어 브라우저 API가 호출되지 않도록 하는 `blocking statement`라는 것이다.

- 위 코드에서 setTimeout이 0초의 딜레이를 가졌다 해도 콜스택이 비워지지 않아 메세지큐에 갇혀있게된다. while문이 끝나고서야 동작한다(js는 싱글스레드이기 때문)

- setTimeout의 딜레이는 실행이 시작되는 타이밍을 보장해주는것이 아니다. 최소한 얼마정도 있다가 실행되라 정도의 의미로 알아두어야 한다.
