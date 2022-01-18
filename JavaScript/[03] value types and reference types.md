## Value types and Reference Types

자바스크립트에서 원시타입(primitive types)인 `Boolen`, `null`, `undefined`, `String`, `Number`,`Symbol` 타입은 **값에 의한 전달**이 일어나며 원시 타입이 아닌 `Object` 타입은 **참조에 의한 전달**이 일어난다.

### Overview

- 자바스크립트에는 2가지 참조 유형이 있다 (Primitives, Reference)
- 모든 변수를 할당한 후에 메모리에 저장된다.
- 변수의 복사가 일어날 때 메모리의 내 값을 복사한다. (변수끼리는 지장이 없다)
- 호출을 통해 변수를 함수에 전달해도 해당 변수의 복사본이 생성된다.

### Primitives Type (원시 타입)

기본 유형의 메모리 내 값은 **실제값**이다. (ex `number` 42 `boolen` true) 기본 유형은 사용 가능한 고정된 양의 메모리에 저장할 수 있다.

- null
- undefined
- Boolean
- Number
- String

기본유형은 스칼라유형 또는 단순유형이라고 표현한다.

### Reference Type (참조 타입)

참조 유형에는 다른 값이 포함될 수 있다. 참조 유형의 내용은 변수에 사용할 수 있는 고정된 메모리 양에 맞지 않으므로 참조 유형의 메모리 내 값은 참조 자체(메모리 주소)이다.

참조유형은 복합유형 또는 컨테이너유형이라고 부른다.

## Code Examples

<hr>

### Copying a primitve

```js
var a = 13;
var b = a;
b = 37;
console.log(a); //13
```

기본 유형이 변수에 할당되면 해당 변수가 기본 값을 포함하는 것으로 생각한다. 따라서 원본은 변경되지 않고 사본만 변경된다.

### Copying a reference

```js
var a = { c: 13 };
var b = a; //  a와 동일한 메모리 주소를 가르킴
b.c = 37;
console.log(a); //{c : 37}
```
