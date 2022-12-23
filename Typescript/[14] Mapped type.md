# 맵드타입(Mapped types)

맵드 타입이란 기존에 정의되어 있는 타입을 새로운 타입으로 변환해주는 문법을 의미한다.  
마치 자바스크립트 map() API 함수를 타입에 적용한 것과 같은 효과를 가져서 맵드 타입이라고 불린다.

# 맵드 타입의 기본 문법

```ts
{ [ P in K ] : T }
{ [ P in K ] ? : T }
{ readonly [ P in K ] : T }
{ readonly [ P in K ] ? : T }
```

# 맵드 타입의 예제

```ts
type Mapped<T> = {
  [Key in T]?: T[key];
};
```

위 코드는 키와 값이 있는 객체를 정의하는 타입을 받아 그 객체의 부분집합을 만족하는 타입으로 변환해주는 문법이다.

```ts
interface Person {
  name: string;
  age: number;
}
```

위 interface에 Mapped type을 적용하면 아래와 같은게 가능해진다.

```ts
type Mapped<T> = {
  [Key in T]?: T[key];
};

interface Person {
  name: string;
  age: number;
}

const age: Mapped<Person> = { age: 5 };
const name: Mapped<Person> = { name: 'jone' };
const empty: Mapped<Person> = {};
const man: Mapped<Person> = { age: 20, name: 'jone' };
```

# 맵드 타입 실습

예를 들어 유저의 정보를 가져오는 API 함수를 작성해야할 때 아래와 같은 코드의 형태일 것이다.

```ts
interface User {
  userName: string;
  email: string;
  profileImageURL: string;
}

async function fetchUser(): Promise<User> {
  ///
}
```

만약 이 유저 정보를 수정하는 API는 아래와 같은 코드일 것이다.

```ts
interface UpdateUser {
  name?: string;
  email?: string;
  profileImageURL: string;
}

async function updateUser(params: UpdateUser) {
  ///
}
```

이 코드는 동일한 프로퍼티가 여러번 선언되어 문제점이 있다. 동일한 타입에 대해 반복적으로 선언하는 것은 좋은 코드가 아니다.

```ts
interface User {
  name: string;
  email: string;
  profileImageURL: string;
}

interface UpdateUser {
  name?: string;
  email?: string;
  profileImageURL: string;
}
```

위의 인터페이스에서 반복되는 구조를 아래와 같이 개선할 수 있다.

```ts
type UpdateUser = {
  name?: User['name'];
  email?: User['email'];
  profileImageURL?: User['profileImageURL'];
};
```

혹은 조금 더 줄여서 아래와 같이 선언할 수 있다.

```ts
type UpdateUser = {
  [Property in keyof User]?: User[Property];
};
```
