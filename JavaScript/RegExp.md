# 정규표현식

## 1. 정규표현식이란?

- 일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어.
- 문자열을 대상으로 **패턴 매칭 기능**을 제공
- 특정 패턴과 일치하는 문자열을 검색하거나 추출 또는 치환할 때 사용
- 정규표현식의 시간복잡도는 2^n으로 백트래킹 기법을 사용한다.

## 2. 정규표현식의 생성

정규표현식은 `패턴`과 `플래그`로 구성된다.

- 정규표현식 리터럴로 생성

```js
const target = 'IS this all there is?';
const regExp = /is/i;
regExp.test(target); //true
```

- RegExp 생성자 함수로 생성

```js
const regExp = new RegExp(/is/i);
```

## 3. RegExp 메서드

### 3-1. RegExp.prototype.exec

- 정규 표현식의 패턴을 검색하여 매칭 결과를 배열로 반환

```js
const target = 'Is this all there is?';
const regExp = /is/;
regExp.exec(target);
//['Is', index:5, input:"Is this all there is?", groups: undefined]
```

### 3-2. RegExp.prototype.test

- 인수로 전달받은 문자열에 대해 정규 표현식 패턴을 검색하여 그 결과를 불리언 값으로 반환하는 함수

```js
const target = 'Is this all there is?';
const regExp = /is/;
regExp.test(target); //true
```

### 3-3. String.prototype.match

- 대상 문자열과 인수로 전달받은 정규 표현식의 매칭 결과를 배열로 반환하는 함수.

```js
const target = 'Is this all there is?';
const regExp = /is/;
target.match(regExp); //['is','is'];
```

## 4. 플래그

패턴과 함께 정규 표현식을 구성하는 플래그는 정규 표현식의 검색 방식을 설정하기 위해 사용

- i: **대소문자 구별하지 않고** 패턴 검색
- g: 대상 문자열 내에서 패턴과 일치하는 모든 문자열을 **전역 검색**
- m: 문자열의 행이 바뀌더라도 패턴을 계속해서 검색

## 5. 자주쓰는 정규 표현식

### 5-1. 특정 단어로 시작하는지 검사

[...] 바깥의 ^는 문자열의 시작을 의미하고, ?은 앞선 패턴이 최대 한번(0번 포함) 이상 반복되는지를 의미한다.

```js
const url = 'https://www.test.com';
const regExp = /^https?:\/\//; //http | https로 시작하는지 검사
regExp.test(url); //true
```

```js
const regExp = /^(http:https):\/\//; //위와 동일
```

### 5-2. 특정 단어로 끝나는지 검사

`$`는 문자열의 끝을 의미한다.

```js
const fileNme = 'index.html';
const regExp = /html$/;
regExp.test(fileName);
```

### 5-3. 숫자로만 이루어진지 검사

처음과 끝이 숫자이고 최소 한 번이상 반복되는 문자열과 매칭

```js
const regExp = /^\d+$/;
```

### 5-4. 하나 이상의 공백으로 시작하는지

`\s`는 여러가지 공백 문자(스페이스, 탭등)를 의미한다. 즉 `\s`는 `[\t\r\n\v\f]와 같은 의미다.

```js
const regExp = /^[\s]+/;
```

### 5-5. 아이디로 사용 가능한지

알파벳 대소문자 또는 숫자로 시작하고 끝나며 4~10자리인지 검사하는 정규식

```js
const regExp = /^[A-Za-z0-9]{4,10}$/;
```

### 5-6. 메일 주소 형식에 맞는지 검사

```js
const regExp = /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z]*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/;
```

### 5-7 핸드폰 번호

```js
const regExp = /^\d{3}-\d{3,4}-\d{4}$/;
```
