## immer 을 이용한 불변성 관리

* 리액트는 절대로 상태관리를 직접해선 안됨
  
   immer을 사용하면 상태관리를 직접하는 것 처럼 사용할 수 있음.
```   
   $ yarn add immer 
```

* immer 에서 신경써야할 produce

    produce 함수는 두개의 파라미터를 받아오는데, 첫번째 파라미터는 수정시키고 싶은 객체를 전달
    두번째 파라미터는 업데이트 함수를 전달.
    업데이트 함수에서는 파라미터로 받은 draftstate를 불변성에 대해 신경쓰지 않고 일반 배열 다루듯 업데이트 해주면 immer에서 처리


* 예제 소스

```
    import produce from "immer"
    const baseState = [
    {
        todo: "Learn typescript",
        done: true
    },
    {
        todo: "Try immer",
        done: false
    }
    ]

    const nextState = produce(baseState, draftState => {
        draftState.push({ todo: "Tweet about it" })
        draftState[1].done = true
    })
```

