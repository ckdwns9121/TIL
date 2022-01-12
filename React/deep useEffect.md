# useEffect 톺아보기

useEffect의 동작원리를 이해하고 정확한 사용방법을 익히기 위함에 useEffect를 톺아보려고 한다.  
hooks를 쉽게 이해하려고 lifeCycle 개념을 가져와 쓰다보니 헷갈리는 부분이 생기는데 lifeCycle은 배제하고 이해해보자.

## 렌더링 마다 고유한 Props와 State가 있다.

```js
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>current count ={count}</p>
      <button onClick={() => setCount(count + 1)}></button>
    </div>
  );
}
```

위 컴포넌트에서 `count`라는 state는 사실상 상수라고 생각해도 된다.  
컴포넌트가 렌더링 될 때 useState()로 부터 리턴된 `0`은 count에 할당되고 그 시점에서의 컴포넌트 상태는 아래와 같다.

```js
function Counter() {
  const count = 0;
  <p>current count ={count}</p>;
}
```

## 모든 렌더링은 고유의 이벤트 핸들러를 가진다.

아래와 같은 소스를 작성해서 count값이 어떻게 출력되는지 생각해보자.  
button을 3번 클릭해서 count를 3으로 만들고 이후에 alert창을 띄우는 `handleAlertClick`함수를 실행시킨뒤 button을 2번 더 클릭해보자.

```js
function Counter() {
  const [count, setCount] = useState(0);
  function handleAlertClick() {
    setTimeout(() => {
      alert('You clicked on: ' + count);
    }, 3000);
  }
  return (
    <div>
      {' '}
      <p>You clicked {count} times</p> <button onClick={() => setCount(count + 1)}> Click me </button> <button onClick={handleAlertClick}>
        {' '}
        Show alert{' '}
      </button>{' '}
    </div>
  );
}
```

결과 값은 **3이 나온다** 그 이유는 `handleAlertClick` 함수를 실행시킨 시점에서의 count 값은 3이기 때문이다.

그 시점에서의 컴포넌트는 아래와 같을 것이다.

```js
function Counter() {
  const count = 3; //(useState로 부터 리턴)
  function handleAlertClick() {
    setTimeout(() => {
      alert('You clicked on: ' + 3);
    }, 3000);
  }
  <button onClick={handleAlertClick} />;
}
```

count 변수가 **상수화** 되었기 때문에 이벤트 핸들러도 상수화된 `3`을 가지고 있다.

> 컴포넌트 내부에 정의된 변수(상태)나 함수는 렌더링 단위로 상수화된다.

## 모든 렌더링은 고유의 이펙트를 가진다.

useEffect안에 넘겨준 함수는 렌더링 될 때마다 새로 생성된다.
그 여러개의 서로 다른 익명함수는 각자가 생성될 당시의 값들을 바라보고 있다.
useEffect에 전달한 익명함수는 리액트가 변경사항을 DOM에 전부 반영하고 난 뒤에 실행해주는 **콜백함수**이다.

## useEffect의 클린업 함수

useEffect의 리턴함수는 componentWillUnmount 이며, 리턴함수는 이펙트를 클린업하기 위해 사용한다.

### 클린업 함수의 실행 순서

1. props나 state 업데이트
2. 컴포넌트 **리렌더링**
3. 이전 이펙트 **클린업**
4. 새로운 이펙트 실행

컴포넌트를 리렌더링 하기 전에 클린업 되는게 아니라 리렌더링 되고나서 클린업 한다.

클린업 함수는 window에 적용된 이벤트 리스너나 setTimeout, setInterval 등과 같은 브라우저 API를 종료하기 위해 많이 사용된다.
