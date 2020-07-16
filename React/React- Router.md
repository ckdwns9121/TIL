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