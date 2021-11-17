## 타입스크립트를 공부한 내용을 저장하는 저장소입니다.

> 이 리포지토리는 [TypeScript Handbook](https://typescript-kr.github.io/)를 보고 정리한 문서입니다.

## 타입스크립트 개발환경 설정

### 1. 개발환경 설정

```
$mkdir ts-practice
$cd ts-practice
$yarn init -y // 또는 npm init -y
```

이렇게 하면 ts-practice에 `package.json`파일이 생성된다.

### 2. 타입스크립트 설정파일 생성하기

그 다음에는 타입스크립트 설정파일 `tsconfig.json`을 만들어보자.
다음과 같이 디렉터리에 `tsconfig.json`파일을 생성후 직접 작성하기.

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true
  }
}
```

명령어를 사용해 생성하기

```
npm install -g typescript
```

그 다음 프로젝트에 다음 명령어를 실행한다.

```
tsc --init
```

- target : 컴파일된 코드가 어떤 환경에서 실행될 지 정의한다. 예를들어 화살표 함수를 사용하고 target을 es5로 한다면 일반 funcion함수로 변환해준다.
- module : 컴파일된 코드가 어떤 모듈 시스템을 사용할지 정의한다.
- stric : 모든 타입 체킹 옵션을 활성화한다는 것을 의미.
- esModuleInterop : commonjs 모듈 형태로 이루어진 파일을 es2015모듈 형태로 불러올 수 있게 해준다.

### 3. 타입스크립트 파일 만들기

`src/practice.ts`라는 파일 생성

```ts
const message: string = 'hello';
console.log(message);
```

해당 코드를 작성하고 빌드를 원한다면 `tsc` 명령어를 입력하면 됨.
그러면 dist/practice.js라는 컴파일된 js파일이 생성됨.
