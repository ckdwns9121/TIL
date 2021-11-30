# 타입스크립트 타입

## 1. 기본 타입

- Boolean

```ts
let check: boolean = false;
```

- Number

```ts
let num: number = 3;
```

- String

```ts
let str: string = 'hello';
```

- Array
  - 배열 타입은 두가지 방법으로 쓸 수 있다.

```javascript
let list: number[] = [1, 2, 3]; // 배열요소들을 나타내는 타입뒤에 []를 쓰는것.
```

```javascript
let list: Array<number> = [1, 2, 3]; // 제네릭 배열 타입을 쓰는것 ex Array<elemType>
```

- Tuple
  - 튜플 타입을 사용하면, 요소의 타입과 개수가 고정된 배열을 표현할 수 있다.

```javascript
//튜플 타입
let x: [string, number];
x = ['hello', 10]; // 성공
x = [10, 'hello']; //오류
```

- Enum
  - enum은 0부터 시작하여 멤버들의 번호를 매긴다. 멤버중 하나의 값을 수동적으로 설정하여 번호를 바꿀 수 있다.

```javascript
enum Color {Red,Green,Blue}
let c: Color = Color.Green;
```

또는, 모든 값을 수동적으로 설정 할 수 있다.

```javascript
enum Color {Red=1 ,Green=2,Blue=4}
let c: Color = Color.Green;
```

- Any
  - 알지 못하는 타입을 표현해야 할 때 쓰는 타입
  - any 타입은 기존에 JavaScript로 작업할 수 있는 강력한 방법으로, 컴파일 중에 점진적으로 타입 검사를 하거나 하지 않을 수 있다.

```javascript
let notSure: any = 4;
notSure = 'maybe a string';
notSure = false;
```

- Void
  - void는 어떤 타입도 없음을 나타내기 때문에 any의 반대 타입과 같다. void는 보통 함수에서의 반환값이 없을 때 사용.

```javascript
function warnUser(): void {
  console.log('this function not return');
}
```

- Null and Undefined
  - TypeScript에서 undefined와 null 둘 다 각각 자신의 타입 이름으로 사용한다.

```javascript
let u: undefined = undefined;
let n: null = null;
```

- Never
  - never 타입은 절대 발생할 수 없는 타입을 나타낸다. 예를 들어, never는 함수 표현식이나 화살표 함수 표현식에서 항상 오류를 발생시키거나 절대 반환하지 않는 반환 타입으로 쓰인다.
  - never타입은 모든 타입에 할당 가능한 하위 타입이다. 하지만 어떤 타입도 never에 할당할 수 있거나, 하위 타입이 아님.(never 자신은 제외) 심지어 any 도 never에 할당할 수 없다.

```javascript
function error(message: string): never {
  throw new Error(message);
}

// 반환 타입이 never로 추론된다.
function fail() {
  return error('Something failed');
}

// never를 반환하는 함수는 함수의 마지막에 도달할 수 없다.
function infiniteLoop(): never {
  while (true) {}
}
```

- 객체 (Object)

`object`는 원시자료형이 아닌 참조자료형을 의미한다.

```ts
declare function create(o: object | null): void;

create({ prop: 0 }); // 성공
create(null); // 성공

create(42); // 오류
create('string'); // 오류
create(false); // 오류
create(undefined); // 오류
```

- 타입 단언 (Type assertions)

타입 단언은 컴파일러에게 내가 작성한 타입을 믿어달라고 말해주는 방법이다.
`타입 단언`은 다른언어희 타입 변환과 유사하지만 다른 특별한 검사를 하거나 데이터를 재구성 하지 않는다.

타입단언에는 두가지 문법이 있다.

- angle-bracket

```ts
let someValue: any = 'this is a string';

let strLength: number = (<string>someValue).length;
```

- as

```ts
let someValue: any = 'this is a string';

let strLength: number = (someValue as string).length;
```
