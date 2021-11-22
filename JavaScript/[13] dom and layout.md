## DOM 그리고 레이아웃

### DOM (Document Object Model)

DOM은 웹 브라우저로 부터 HTML,XML을 표현하기 위한 인터페이스를 제공한다. 이러한 인터페이스는 웹의 구조나 스타일을 조작할 수 있게 도와준다.

DOM에 대해 좀더 직관적으로 정의를 내리면 아래와 같다.

> 넓은 의미로는 웹브라우저가 html을 인식하는 방식  
> 좁은 의미로는 document 객체와 관련된 객체 집합

DOM은 자료구조중 트리 형식을 가지고 있으며 이를 DOM Tree라고 부른다.

![ex_screenshot](/asset/dom-tree.png)

### DOM의 문제점

DOM은 동적 UI에 최적화되어 있지 않다. DOM자체를 읽고 쓸 때의 성능은 자바스크립트 객체를 처리할 때 성능과 비교해서 크게 차이가 나지 않는다.
단, 브라우저 단에서 DOM변화가 일어난다면 브라우저가 CSS를 다시 연산한다음 레이아웃을 구성하고 렌더링하는데 시간이 요소된다.

### DOM을 다루는 API

- getElementByTagName()  
   특정 태그를 가진 요소에 바로 접근가능.
- getElementById()  
   특정 아이디를 가진 요소에 바로 접근 가능.
- getElementByClassName()  
   특정 클래스를 가진 요소에 바로 접근 가능.
- createElement()  
   요소 생성
- appendChild()  
   선택된 노드에 자식으로 요소를 추가 가능
- removeChild()  
   특정 요소 삭제 가능
- getAttribute()  
   해당 요소의 속성값을 얻을 수 있음.
- setAttribute()  
   원하는 노드의 속성값을 바꿀 수 있음
