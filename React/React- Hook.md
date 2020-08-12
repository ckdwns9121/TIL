## 리액트 훅

#### Hooks

    Hooks는 함수형 컴포넌트에서 state를 제공함으로써 상태 관련 로직의 재사용을   
    이전보다 훨씬 쉽게 만들어준다.


* useState

  - 가장 기본적인 Hook이며 함수형 컴포는트에서도 가변적인 상태를 지닐 수 있게 함.   
  - 하나의 상태는 하나의 useState가 사용되어야 함 
  - useState는 함수에 state를 제공한다. initialState를 파라미터로 받고 state와 state를 변경할 setState함수를 반환한다. 

```  
    import React, {usetState} from 'react'
    const Conter = () =>{
        const [value,setValue] = useState(0) //기본 상태값 셋팅
        const [number,setNumver] = useState(0)
    }
``` 
   
* useEffect 

    - 리액트 컴포넌트가 렌더될 때 마다 특정 작업을 수행하도록 설정하는 Hook
    - 클래스형 컴포넌트에서 componentDidMount, componentDidUpdate, componentWillUnmount의 기능을 수행
    - render가 발생할 때 마다 effect가 실행된다. 두번째 파라미터인 inputs를 통해 특정 상태가 update 되었을 때만 실행 가능

```
    useEffect(()=> {   
        console.log("마운트");   
    },[])    
    ...   

    2.특정 값이 업데이트 될때 실행

    useEffect(() => {   
        console.log(name);   
    },[name])   
    ...   
```

* useSelector

    - useSelector는 selector Callback을 전달하여, 리덕스 스토어의 필요한 상태에 접근 가능
    - 이전의 connect를 통해 상태값을 조회하는 것보다 훨씬 간결하게 작성하고 코드 가독성이 상승되는 장점이 있는 함수.

* useDispatch

    - 컴포넌트 내에서 dispatch를 사용하게 하는 함수.


* useReducer

    - 컴포넌트 상황에 따라 여러 상태를 다른 값으로 업데이트 해주고 싶을 때 사용하는 Hook.   
    - 리듀서는 현재 상태, 그리고 업데이트를 위해 필요한 정보를 담은 액션 값을 전달받아 새로운 상태를 return   
    - 어떤 액션인지 선언을 해야함    ex {type : 'INCREMENT'}   
    - 리덕스에서 같이쓰면 효율적   


* useMemo

    - 함수형 컴포넌트 최적화 할 때 씀    
    - 렌더하는 과정에서 특정 값이 바뀌었을 때만 연산을 실행하고, 그렇지 않으면 이전에 연산했던 결과를 재 사용
    - 특정 결과 값을 재 사용할 때 사용하는 반면 useCallback은 특정 함수를 재사용 함   

* useCallback
    함수들은 컴포넌트가 리렌더 될 때 마다 새로 만들어진다.  
    한번 선언한 함수를 렌더 될 때 마다 새로 만드는건 비효율 적이라 재 사용 하는건 중요   

    - 렌더링 성능을 최적화 할 때 사용 (useMemo와 비슷)   
    - 이 Hook을 사용하면 필요할 때만 이벤트 핸들러 함수를 생성 할 수 있음
    - useMemo는 특정 값 재사용 useCallback은 특정 함수를 재사용

* useRef

    - 함수형 컴포넌트에서 ref를 쉽게 사용할 수 있도록 도와줌   

* useHistroy

    - react-router-dom 에서 제공하는 hook
    - useHistory 내장 함수로 푸쉬 , 리다이렉션 ,백 등 라우터처럼 사용




    
