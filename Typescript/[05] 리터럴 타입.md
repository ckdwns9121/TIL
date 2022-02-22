# 리터럴 타입

## 1. 리터럴 타입 좁히기

`var` 또는 `let`으로 변수를 선언할 경우 이 변수의 값이 변경될 가능성이 있음을 컴파일러에게 알리지만 반면 `const`로 선언된 경우 이 객체는 절대 변경되지 않는다.

```ts
const helloWorld = 'Hello World';

// 반면, let은 변경될 수 있으므로 컴파일러는 문자열이라고 선언할 것입니다.
let hiWorld = 'Hi World';
```

const는 절대 변경되지 않기 때문에 `string`타입이지만 리터럴 자체를 하나의 타입으로 인지하고 `Hello World`로 타입을 정한다.

## 2. 문자열 리터럴 타입

문자열 리터럴 타입은 유니언 타입, 타입 가드, 타입 별칭과 잘 결합된다.
이런 기능을 `enum`과 비슷한 형태로 사용할 수 있다.

```ts
// @errors: 2345
type Easing = 'ease-in' | 'ease-out' | 'ease-in-out';

class UIElement {
  animate(dx: number, dy: number, easing: Easing) {
    if (easing === 'ease-in') {
      // ...
    } else if (easing === 'ease-out') {
    } else if (easing === 'ease-in-out') {
    } else {
      // 하지만 누군가가 타입을 무시하게 된다면
      // 이곳에 도달하게 될 수 있습니다.
    }
  }
}

let button = new UIElement();
button.animate(0, 0, 'ease-in');
button.animate(0, 0, 'uneasy');
```

## 3. 숫자형 리터럴 타입

숫자형 리터럴 타입은 고정된 값 을 설정할 때 사용한다.

```ts
/** loc/lat 좌표에 지도를 생성합니다. */
declare function setupMap(config: MapConfig): void;
// ---생략---
interface MapConfig {
  lng: number;
  lat: number;
  tileSize: 8 | 16 | 32;
}

setupMap({ lng: -73.935242, lat: 40.73061, tileSize: 16 });
```
