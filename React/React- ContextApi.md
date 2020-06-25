## Context-api 사용법

#### Props Driing 현상
* Props Driing 현상이란 부모 컴포넌트에서 하위 컴포넌트에게 props를 전달 하기위해 모든 컴포넌트에게 props를 전달 해야하는 패턴

#### Context-api
* 이러한 Props Driing 현상을 막기위해 전역 state를 선언하도록 해주는 api

사용 예

    import React, { createContext } from 'react' //createContext를 react 에서 받아옴

    // 1. Context를 생성
    const AppContext = createContext();
    class App extends Component{
    state={
        nickname: 'test',
        isAdmin :true
    }

    render(){
    console.log(this.state)
    return(
      <AppContext.Provider value={this.state}>
      <div>
        <Main />
      </div>
    </AppContext.Provider>
     )
    }
    }

    const Main = () => (
    <main>
        <Avatar />
    </main>
    )

    const Avatar = () => (
    <div>
    <User />
    </div>
    )

    // 2. AppContext.Consumer 컴포넌트를 이용해 Context에서 전달한 value를 사용
    const User = () => (
        <AppContext.Consumer>
            {value => {
            let label = 'user'
            if (value.isAdmin) {
            label = 'admin'
         }

      return (
        <div>
          <div>{label}</div>
          <div>{value.nickname}</div>
        </div>
      )
     }}
     </AppContext.Consumer>
    )

끝