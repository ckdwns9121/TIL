# useEffect

## useEffect란?

`useEffect`함수는 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행할 수 있도록 도와주는 `Hook`이다.

클래스형 컴포넌트에서 사용할 수 있었던 생명주기 메소드를 함수형 컴포넌트에서도 사용할 수 있게 된다.

## useEffect 사용법

```js
useEffect(function, deps);
```

### mount될 때 실행

deps 배열에 빈 값을 넣으면 마운트 될 때만 실행된다.  
페이지가 렌더링 되기전 API를 호출하거나 초기 값을 설정할 때 사용

```js
useEffect(() => {
  //function
}, []);
```

만약 배열을 생략한다면 렌더링 될 때 마다 실행되므로 성능측면에서 비효율 적이다.

## update될 때 실행

특정 값이 업데이트 되었을 때 실행하고 싶으면 deps 배열에 업데이트 되었을 때 검사하고 싶은 `state`를 넣어주면 된다.

```js
useEffect(() => {
  console.log(state + '변경');
}, [state]);
```

## unmount될 때 실행

컴포넌트가 사라질 때 혹은 업데이트 되기 직전에 실행된다.

뒤에 return 함수는 **cleanup** 함수라고 부르며 뒷정리 함수라고도 한다.

```js
useEffet(() => {
  console.log('mount');
  return () => {
    console.log('unmount');
  };
}, []);
```
