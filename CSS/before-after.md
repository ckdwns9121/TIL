## before after 활용법.

### 가상요소란?

가상클래스는 별도의 클래스 선언 없이 클래스를 지정한 것 처럼 사용할 수 있는 요소.

### before after?

- before: 실제 내용 바로 앞에서 생성되는 자식요소
- after: 실제 내용 바로 뒤에 생성되는 자식요소

before와 after를 쓸 때 content라는 속성이 반드시 필요하다.

### before after의 활용

1. 구분 bar가 포함된 서브네비게이션에서 따로 div요소를 만들지 않아도 쉽게 구현할 수 있다.

```html
<style>
  .list li {
    float: left;
    margin-left: 5px;
  }
  .list li ::before {
    padding-left: 5px;
    content: '|';
  }
  .list li :first-child::before {
    content: '';
  }
</style>
<div id="content">
  <ul class="list">
    <li>one</li>
    <li>two</li>
    <li>three</li>
  </ul>
</div>
```

2. float 해제 방법

부모요소에게 after를 사용하여 float되어 있는 요소를 clear 해준다.
