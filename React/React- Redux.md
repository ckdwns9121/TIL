## 리덕스

## 1. 리덕스란

   Redux는 JavaScript 앱을 위한 예측 가능한 상태 컨테이너이다.   
   Flux개념을 바탕으로한 React에서 가장 많이 사용되는 상태관리 라이브러리.




## 2. 리덕스에서 사용되는 키워드

* 액션
 
  상태에 어떠한 변화가 필요하게 될 때 액션타입을 명시해주는것,
  type :INCREMENT


```typescript 
const INCREMENT = 'counter/INCREMENT' as const //액션
```
as const를 액션에 붙여줌으로써 나중에 액션 객체를 만들때 타입을 추론하는 과정에서 action.type이 문자열로 추론되지 않고 **'counter/INCREMENT'**라는 실제 **고정된 문자열 값**으로 추론하기 위함.

* 액션 생성함수

  액션 생성함수는 액션들 만드는 함수, 파라미터를 받아와서 액션 객체 형태로 return

```typescript
export const increment =()=>({
    type : INCREMENT
})
```
* 리듀서

   변화를 일으키는 함수. 현재 상태와 전달받은 액션을 참고해 새로운 상태를 만들어 리턴


* 스토어

    리덕스에서 한 어플리케이션당 하나의 스토어를 만듦,

```javascript
import {createStore} from 'react-redux';
const store = createStore(reducers)
```

### 구독

    스토어의 내장함수중 하나, 그러나 리액트에서 직접적으로 사용하는 경우는 거의 없고
    react-redux의 내장함수인 connect를 통해 구독한다.

 
## 3. 스토어 생성방법

    액션타입 선언 -> 액션생성자 -> 리듀서 구현 -> 스토어에 파라미터로 넘김


## 4. Ducks 패턴

    기본적인 디렉터리 구조는 actions, reducers 등등의 디렉토리로 분리되있지만
    프로젝트가 커지고 관리할 소스코드가 많아지면 액션과 리듀서가 분리되어있는 구조는 매우 불편하다.

    그래서 리듀서와 액션, 액션생성자 등 관련 코드를 하나의 파일에 묶어 작성하는 패턴을 Ducks 패턴이라고 한다.


## 5. connect 함수
    기본적으로 Container 코드에서 작성  

```javascript
import {connect} from 'react-redux';  
import {hello} from '../mudules;  
    
const TestContainer =({test,onHello}){  
    return(  
            <Test  
            test={test}  
            onHello={onHello}  
            />  
        )  
    }  
  
    mapToStateProps = (state) =>({  
        test : state.test  
    })  
    mapToDispatchProps = (dispatch) =>({    
        onHello : () => dispatch(hello())    
    })  
export default connect(mapToStateProps,mapToDispatchProps)(TestContainer);  
```

## 번외. Flux 패턴이란

    Flux 어플리케이션에서의 데이터의 흐름은 단방향으로 흐른다.

![ex_screenshot](../Asset/flux.png)

    단방향 데이터 흐름은 Flux패턴의 핵심.