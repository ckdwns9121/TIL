# useState Hook과 클로저

### 1. useState의 작동 방식

useState의 상태 업데이트는 비동기로 진행된다. 첫번째 요소는 상태 값이며 두번째 요소는 상태 업데이트 함수이다.

```javascript
const [state,setState] = useState(initState);
```
여기서 state는 const로 선언되어 있다. 따라서 state가 값이 변할 리 없다.   
그렇다면 어떻게 const값이 내부적으로 변하는지 확인해보자.

리액트 모듈에서 useState를 살펴보면 실행될때 마다 dispatcher를 선언하고 useState 메소드를 실행시켜 그 값을 반환한다.    
할당부를 거슬러 올라가다 보면 dispatcher는 전역 변수 ReactCurrentDispatcher로 부터 가져온다.   
함수가 선언부보다 상위에 있는 값에 접근한 **클로저** 이다.


### 2. setState의 동작방식

```javascript
import {useState} from 'react';

function App(){
    const [state,setState] = useState(0);

    const onClick=()=>{
        console.log('click');
        setState(1);
        if(state===1){
            console.log('실행');
        }
    }

    return(
        <div onClick={onClick}>
        버튼 클릭
        </div>
    )
}

```

```javascript

//클로저로 구현한 간단한 useState
let value;

export useState(initState) {
    if(value ===undefined){
        value =initState;
    }
    
    const setState = (newValue)=>{
        value = newValue;
    }
    return [value,setState]
}
```

해당 코드를 더블클릭 하면 어떤 일이 벌어질까.
콘솔창이 한번밖에 찍히지 않는다.    

1. 최초 첫 렌더링 때 useState가 호출된다.
2. useState는 초기값을 할당한다 (value가 undefined이니까)
3. useState에서 value를 반환한다. (이때 값 0)
4. 반환받은 0을 state에 할당한다.
5. 클릭이벤트 발생한다.
6. console.log('click')이 실행된다.
7. setState가 실행되고 1이 전달된다.

setState 실행 이후
1. setState가 실행되고 value값이 1로 갱신된다.
2. 이후 컴포넌트를 리렌더링 시킨다.
3. 전역변수 value는 값이 1로 할당된 상태이기때문에 상태가 갱신된다.
4. 두번째 클릭이후 현재 상태가 1이기 때문에 console.log('실행')이 찍힌다.

