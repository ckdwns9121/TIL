# typeof 연산자

객체 데이터를 객체 타입으로 변환해주는 연산자이다. 즉 객체의 구조를 그대로 가져와 독립적인 타입으로 쓰고 싶을 때 사용한다.

```ts
const obj = {
  red: 'apple',
  yellow: 'banana',
  green: 'cucumber',
};

// type Fruit = obj; // error

type Fruit = typeof obj; // ok

/*
type Fruit ={
    red: string,
    yellow: string,
    green : string
}
*/

const obj2: Fruit = {
  red: 'apple',
  yellow: 'orange',
  green: 'melon',
};
```

# keyof 연산자

객체 형태의 타입을, `프로퍼티`만 모아 유니온 타입으로 만들어주는 문법

```ts
interface User = {
  name: string;
  age: number;
  email: string;
};

type T = keyof User;

const a : T = "name";
const b: T = "age";
const c: T= "email"

```

# keyof typeof 활용하기

```ts
const obj = { red: 'apple', yellow: 'banana', green: 'cucumber' } as const; // 상수 타입을 구성하기 위해서는 타입 단언을 해준다.

// 위의 객체에서 red, yellow, green 부분만 꺼내와 타입으로서 사용하고 싶을떄
type Color = keyof typeof obj; // 객체의 key들만 가져와 상수 타입으로

let ob2: Color = 'red';
let ob3: Color = 'yellow';
let ob4: Color = 'green';
```
