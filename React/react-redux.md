# react-redux

## 상태 관리 도구(State Management Tools)가 왜 필요할까?

- 자식 컴포넌트들 간의 직접적인 데이터 전달은 불가능
- 자식 컴포넌트들이 데이터를 주고받을 때 부모컴포넌트를 통해 주고 받음
- 자식이 많으면 상태 관리가 매우 복잡

## 상태 관리 도구가 해결해주는 문제

- Props drilling 이슈 해결
- 전역 상태 저장소 제공

## redux란?

redux는 자바스크립트 상태관리 라이브러리이다.

## redux에서 사용되는 키워드

- 액션: 상태에 어떠한 변화가 필요할 때 스토어에 운반할 데이터(주문서)

```typescript
const INCREMENT = 'counter/INCREMENT' as const; //액션
```

as const를 액션에 붙여줌으로써 나중에 액션 객체를 만들때 타입을 추론하는 과정에서 action.type이 문자열로 추론되지 않고 **'counter/INCREMENT'**라는 실제 **고정된 문자열 값**으로 추론하기 위함.

- 액션 생성함수: 액션 생성함수는 액션들 만드는 함수, 파라미터를 받아와서 액션 객체 형태로 return

```typescript
export const increment = () => ({
  type: INCREMENT,
});
```

- 리듀서: 변화를 일으키는 함수. 현재 상태와 전달받은 액션을 참고해 새로운 상태를 만들어 리턴 (순수함수)

- 스토어: 상태가 관리되는 오직 하나의 공간

```javascript
import { createStore } from 'react-redux';
const store = createStore(reducers);
```

## redux에서 스토어를 생성하는 방법

### 1. mapStateToProps()

### 2. Redux hooks

- useDispatch()
- useSelector()

## Ducks 패턴

```
기본적인 디렉터리 구조는 actions, reducers 등등의 디렉토리로 분리되있지만
프로젝트가 커지고 관리할 소스코드가 많아지면 액션과 리듀서가 분리되어있는 구조는 매우 불편하다.

그래서 리듀서와 액션, 액션생성자 등 관련 코드를 하나의 파일에 묶어 작성하는 패턴을 Ducks 패턴이라고 한다.
```

## 번외. Flux 패턴이란

> Flux 어플리케이션에서의 데이터의 흐름은 단방향으로 흐른다.

![ex_screenshot](./asset/flux.png)

단방향 데이터 흐름은 Flux패턴의 핵심.
