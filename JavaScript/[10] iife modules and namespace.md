# IIFE, Modules and Namespace

## IIFE

IIFE (Immediately Invoked Function Expressions)는 **즉시 호출 함수 표현식**의 줄임말이다.

즉시 실행 함수는 **함수 리터럴**을 `()`로 감싼 뒤 바로 실행하는 형태가 일반적이다.

기본적인 형태는 아래와 같다.

```js
(function () {
  //code..
})();
```

이것은 **즉시 호출되는 익명 함수 표현식**이다.
리턴 값이 없을 때는 문법적으로 아래와 같이 표현하기도 한다.

```js
!(function () {
  console.log('hello');
})();
```

자바스크립트 엔진은 코드를 해석할 때 `function`으로 시작하면 함수 선언식으로 인지하시만 위와같이 연산자를 붙여주면 **함수 표현식**으로 인식하기 때문에 위와 같은 문법으로 사용한다.

> 이 함수는 호출과 즉시 바로 없어진다.

## 언제 사용할까?

전역 스코프를 오염시키지 않기 위해 사용하는 경우가 많다.

- 불 필요한 전역 변수와 함수를 생성하지 않는다.
- IIFE에서 생성된 변수와 함수는 전역스코프와 충돌하지 않는다.
- 클로저와 함께 private한 데이터를 사용할 수 있다.

프로그램 초기 실행시 init 함수를 실행한다고 생각해보자.

```js
function init() {
  var test = 'test';
  console.log(test);
}
init();
```

이 함수는 전역스코프에 선언되어 `name collision`이 발생할 확률이 높다. 외부에서 의도치 않게 호출될 가능성이 있기 때문이다.

따라서 외부 코드로부터 사용되지 않는 단 한번 호출하는 코드들, 이 코드에서 사용하는 변수와 함수들은 IIFE를 사용하여 **전역스코프의 오염을 방지시키고 실수로 인한 재호출이 없도록** 한다.

```js
(function init() {
  var test = 'test';
  console.log(test);
})();
```

이렇게 IIFE로 선언된 변수와 함수는 외부에서 접근이 불가능하다.

### Module

모듈은 다른사람의 코드나 내가 잘게 쪼개어 놓은 코드를 재사용하고 싶을 때 쓰는 것.

```js
// 남의 코드들 먼저 불러오기
<script src="jquery.js"></script>
<script src="tweenmax.js"></script>
// 그걸 사용해 내 코드 작성
<script>
window.$
window.TweenMax
</script>
```

이런식으로 불러오고자 하는 코드를 스크립트 태그에 추가한 뒤 내 스크립트에서 사용한다. 문제는 남의 코드들이 같은 변수를 사용할 때 일어난다.

#### 1. AMD

AMD는 Asynchronous Module Definition으로 비동기적 모듈 선언이라는 뜻이다. 이를 구현한 대표적인 스크립트가 **requireJS**이다.

#### 2. CommonJS

이 방식은 노드에서 채택한 방식으로 매우 자주 쓰인다.

```js
const t = require('./test');
module.exports = {
  t,
};
```

require로 불러와 module.export로 내보내기 한다.
