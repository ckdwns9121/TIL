# 함수

## 1. 함수

- TypeScript 함수는 JavaScript와 마찬가지로 기명함수와 익명함수로 만들 수 있다.
- 이를 통해 API에서 함수 목록을 작성하든 일회성 함수를 써서 다른 함수로 전달하든 애플리케이션에 가장 적합한 방법을 선택할 수 있다.

```ts
/// 기명함수
function add(x, y) {
  return x + y;
}

/// 익명함수
let myAdd = function (x, y) {
  return x + y;
};
```

## 2. 함수 타입

#### 함수의 타이핑

```ts
function add(x: number, y: number): number {
  return x + y;
}

let myAdd = function (x: number, y: number): number {
  return x + y;
};
```

#### 함수의 타입 작성하기

- 함수의 타입은 매개변수의 타입과 반환 타입이 있다.

- 선택적 매개변수와 기본 매개변수

  - TypeScript에서는 모든 매개변수가 함수에 필요하다고 가정한다.
  - JavaScript에서는 모든 매개변수가 선택적이고 , 사용자는 적합하다고 생각하면 그대로 둘 수 있다. (그 값은 undefined)

- 나머지 매개변수

#### 타입의 추론

```ts
// myAdd는 전체 함수 타입을 가집니다
let myAdd = function (x: number, y: number): number {
  return x + y;
};

// 매개변수 x 와 y는 number 타입을 가집니다
let myAdd: (baseValue: number, increment: number) => number = function (x, y) {
  return x + y;
};
```

TypeScript 컴파일러가 방정식의 한쪽에만 타입이 있더라도 타입을 알아낼 수 있다.
이러한 타입 추론의 형태를 `contextual typing`이라 부른다.

## 3. 선택적 매개변수와 기본 매개변수

타입스크립트에서는 모든 매개변수가 함수에 필요하다고 가정한다. 이것이 `null`이거나 `undefined`를 줄 수 없다는걸 의미하는것은 아니다.  
대신 필요한 인자에 모든 값을 넣어서 함수를 호출해야한다.

```ts
function buildName(firstName: string, lastName: string) {
  return firstName + ' ' + lastName;
}

let result1 = buildName('Bob'); // 오류, 너무 적은 매개변수
let result2 = buildName('Bob', 'Adams', 'Sr.'); // 오류, 너무 많은 매개변수
let result3 = buildName('Bob', 'Adams'); // 정확함
```

타입스크립트에서는 `?`를 붙임으로써 매개변수가 필요할 때만 넘길 수 있다.

```ts
function buildName(firstName: string, lastName?: string) {
  if (lastName) return firstName + ' ' + lastName;
  else return firstName;
}

let result1 = buildName('Bob'); // 지금은 바르게 동작
let result2 = buildName('Bob', 'Adams', 'Sr.'); // 오류, 너무 많은 매개변수
let result3 = buildName('Bob', 'Adams'); // 정확함
```

## 4. 나머지 매개변수

`arguments` 라는 인자배열을 사용해서 작업할 수 있다.

```ts
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + ' ' + restOfName.join(' ');
}

// employeeName 은 "Joseph Samuel Lucas MacKinzie" 가 될것입니다.
let employeeName = buildName('Joseph', 'Samuel', 'Lucas', 'MacKinzie');
```

## 5. 함수 오버로드
