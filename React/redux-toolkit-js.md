## Redux Toolkit start

### RTK

기존 리덕스를 사용하면 액션 생성, 액션 함수 구현, 리듀서 구현등 코드가 늘어나기 마련이고, 그에 따라 복잡해진다.
또한 비동기 작업을 위해 thunk나 saga를 별도로 설치해야한다.  
그런데 RTK는 redux가 saga를 제외한 모든 기능을 지원한다.

```
$yarn add @reduxjs/toolkit
```

### configureStore

```js
import { configureStore, MiddlewareArray } from "@reduxjs/toolkit";
import logger from "./loggerMiddleware";
import { noticeSlice } from "./noticeSlice";

export const store = configureStore({
  // composeWithDevtools, thunk 자동 활성화
  reducer: {
    // 리듀서 정의
    notice: noticeSlice.reducer,
  },
  middleware: new MiddlewareArray().concat(logger), // logger 미들웨어 추가
  devTools: process.env.NODE_ENV !== "production"
});

// store 스스로 루트상태 정의
export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
export const useAppDispatch = () => useDispatch<AppDispatch>();
```

- `reducer` : store의 리듀서를 정의한다. 기존의 rootReducer의 역할을 한다
- `middleware`: 필요한 미들웨어는 위와같이 추가해준다.
- `middlewareArray`: 는 미들웨어 array에 다른 미들웨어를 type-safe 결함하는데 사용한다
- `devTools`: 실 서비스와 같이 리덕스 개발 도구가 보이면 안되는 상황에서 사용한다

또한 `useAppDispatch`같이 훅을 export한다음 const dispatch = useDispatch() 사용하는것이 더 편리할 수 있다.

### createAction

리덕스에서는 액션을 정의한다.

```javascript
export const increment = createAction("INCREMENT");
let action = increment();

action = increment(3);
function counter(state = 0, action) {
  switch (action.type) {
    case increment.type:
      return state + 1;
    case decrement.type:
      return state - 1;
    default:
      return state;
  }
}
```

위의 코드에서 볼 수 있듯이 **createAction**에는 기본적으로 타입 문자열만 제공하면 된다.  
그리고 만들어진 액션 생성자의 파라미터는 payload에 들어간다.

만약 리턴되는 액션 객체에 더 손을 보고싶으면 콜백함수를 createAction의 두번째 파라미터로 전달하면 된다.

```javascript
const addTodo = createAction("todos/add", function prepare(text) {
  return {
    payload: {
      text,
      createAt: new Date().toISOString(),
    },
  };
});

addTodo("hello world");

/** returns
 * {
 *   type: 'todos/add',
 *   payload: {
 *     text: 'hello world',
 *     createdAt: '2019-10-03T07:53:36.581Z'
 *   }
 * }
 **/
```

### Flux Standard Action

Redux Toolkit에서는 액션 객체의 형태로 FSA를 강제한다.

```javascript
{
    type:'counter/INCREMENT',
    payload:{
        value:1
    }
}
```

객체는 액션을 구분할 고유한 문자열을 가진 **type**필드가 반드시 있으며 **payload**필드에 데이터를 담아서 전달한다.

### reducer

Redux Toolkit에서의 리듀서 작성은 **createReducer** API를 사용한다.

```javascript

const increment = createAction('counter/INCREMENT');
const decrement = createAction('counter/DECREMENT');
const initState={
    value:0
}

const counterReducer = createReducer(initState, {
    [increment] : (state,action) => state.value+=1;
    [decrement] : (state,action) => state.value-=1;
})

```

switch문이 사라졌다. 이제 쓸데없은 **default** 문을 작성하지 않아도 된다.

### immer

리듀서 함수는 내부적으로 immer의 produce를 사용한다. 그래서 리듀서 함수에서 새로운 상태를 리턴할 필요가 없다.

```javascript
const todoReducer = createReducer([],{
    ['addTodo'] : (state,action)=>{
        ...state,
        state.push(action.payload);
    }
})
```

불변성을 유지하기 위해 Object.assign으로 새 객체를 만들거나 map으로 새 배열을 만들 필요가 없다.

### Action + Reducer = Slice

Redux Toolkit의 핵심이다. **createSlice**로 액션, 리듀서를 한번에 만들 수 있다.

```javascript
const initialState={
    todos:[]
}

const todoSlice = createSlice({
    name:'todos',
    initialState,
    reducers:{
        addTodo:(state,action) =>{
            ...state,
            state.todos.push(action.payload)
        }
        deleteTodo(state,action)=>{
            ...state
            state.todos.splice(
                state.todos.findIndex (todo=> todo.id === action.payload),1
            )
        }
    }
})

export const {addTodo, deleteTodo} = todoSlice.action;
export default todoSlice.reducer
```

### Define Typed Hooks

`useSelectore` , `useDispatch` 각각 나의 애플리케이션에 맞게 훅으로 만드는 것이 좋다.

- 매번 `useSelectore`에 `(state:RootState)`로 타입을 지정해주는 것이 번거롭다.
- `useDispatch`는 thunk에 대해 알지 못한다. thunk를 올바르게 dispatch하려면 thunk 미들웨어 유형을 포함하는 저장소에 특정 사용자 지정 `AppDispatch` 유형을 사용하면 좋다.

```javascript
import { TypedUseSelectorHook, useDispatch, useSelector } from 'react-redux'
import type { RootState, AppDispatch } from './store'

// Use throughout your app instead of plain `useDispatch` and `useSelector`
export const useAppDispatch = () => useDispatch<AppDispatch>()
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector
```

```js
import React from "react";
import { useAppSelector, useAppDispatch } from "app/hooks";

import { decrement, increment } from "./counterSlice";

export function Counter() {
  // The `state` arg is correctly typed as `RootState` already
  const count = useAppSelector(state => state.counter.value);
  const dispatch = useAppDispatch();

  // omit rendering logic
}
```
