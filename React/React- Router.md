## 리액트 라우터


- 프로젝트 생성 및 라이브러리 설치

``` react
    $yarn add react-router-dom  //브라우저에서 사용되는 리액트 라우터  
    $yarn add cross-env --dev // NODE_PATH를 사용해 절대경로로 파일 불러올 시 환경변수를 설정하는데 운영체제마다 방식 다르므로 통합해주는 라이브러리  
```


- NODE_ENV 설정 (packge.json)

``` react
    "scripts": {  
    "start": "cross-env NODE_PATH=src react-scripts start",  
    "build": "cross-env NODE_PATH=src react-scripts build",  
    "test": "react-scripts test --env=jsdom",  
    "eject": "react-scripts eject"  
     }  
``` 


- Router에서 제공하는 기본 컴포넌트
    - <BrowserRouter/> HTML5 히스토리 API를 사용해 주소를 관리하는 라우터
    - <Route/> 요청 경로와 렌더할 컴포넌트 설정
    - <Switch/> 하위 라우터중 하나를 선택
    - <Redirect/> 요청 경로를 다른 경로로 리다이렉션.

1. src/client/Root.js 생성

```
    //Root 컴포넌트 생성후 BrowserRouter 적용
    import React from 'react';
    import { BrowserRouter } from 'react-router-dom';
    import App from '../shared/App';

    const Root = () => (
         <BrowserRouter>
            <App/>
        </BrowserRouter>
    );

    export default Root;
```


2. 라우트 설정하기 

```
    import React, { Component } from 'react';
    import { Route } from 'react-router-dom';
    import { Home, About } from 'pages';


    class App extends Component {
        render() {
            return (
                <div>
                <Route exact path="/" component={Home}/>
                <Route path="/about" component={About}/>
                </div>
        );
     }
    }
    

    export default App;
```

  라우트를 설정 할 때에는 Route 컴포넌트를 사용하고 경로에 Path를 준다.  
  exact 는 주어진 경로와 정확히 맞아 덜어져야만 설정한 컴포넌트를 보여준다.  

3. 라우트 파라미터 읽기

라우트의 경로에 특정값을 넣는 방법은 2가지가 있다.   
첫번째는 params를 사용하는 것과    
두번째는 query를 사용하는것이 있다.   

- 라우트로 설정한 컴포넌트는 3가지 props 를 받게 된다.
  - history : 이 객체를 통해 push, replace 를 이용해 다른 경로로 이동하거나 앞 뒤 페이지로 전환 가능.
  - location : 현재 경로에 대한 정보를 지니고 있는 URL 쿼리
  - match : 어떤 라우트에 매칭이 되어있는지에 대한 정보가 있다.

- 특정값이 없어도 link로 이동하게 하려면 params에 ?를 붙이면 된다.


4. 라우터 이동하기

- Link 컴포넌트

페이지 이동시 사용하는 컴포넌트, a태그로 링크를 걸면 새로고침 되기 때문에    
Link 컴포넌트를 이용해 페이지를 이동한다.

```Link

   <Link to "/path"> Path </Link> 

```

- NavLink 컴포넌트

페이지 이동시 (메뉴 탭 과 같은) 활성화 된 link의 스타일을 바꿀 수 있도록 함   
activeStyle로 스타일 선언

```NavLink

    const activeStyle = {
        height: '100%',
        textDecoration: 'none',
        color: 'black',
        borderBottom: '3px solid #000'
    };
    <NavLink to ="/" activeStlye={activeStyle}> 홈 </NavLink>

```


5. 404 페이지 처리

<Switch>로 모든 <Route> 컴포넌트로 묶어줘야 한다.   
<Switch>컴포넌트를 사용하면 그 하위에 있는 <Route>컴포넌트에 매치되더라도 무시된다.

``` 404
    
    <Switch>
     <Route exact path ="/" component={Home}/>
     <Route path ="/about" component={About}/>
     <Route component={NotFound}/>
     </Switch>

```