# 제네릭

- 제네릭이란 어떠한 클래스 혹은 함수에서 사용할 타입을 그 함수나 클래스를 사용할 때 결정하는 프로그래밍 기법을 말한다.
- TypeSciprt에서 any를 이용하여 구현할 수도 있지만 자료의 타입이 같지않다는 문제점이 생긴다. 따라서 런타임에서 항상 타입검사를 해줘야 한다.

## 1. interface에서 Generic 사용하기

T는 Type의 약자로 다른 언어에서도 제네릭을 선언할 때 관용적으로 많이 사용한다.

```javascript
interface Items<T> {
  list: T[];
}

const items: Items<string> = {
  list: ['a', 'b', 'c'],
};
```

## 2. 클래스에서 Generics 사용하기

제네릭을 유용하게 사용할 수 있는 경우로는 자료구조가 있다. 다음과 같이 스택을 구현한다고 가정하자.

```typescript
class Stack{
    private data: any[]: [];

    constructor(){

    }
    push(item:any): void{
        this.data.push(item);
    }
    pop() :any{
        return this.data.pop();
    }
}
```

스택 자료구조 같은 경우는 대개 범용적인 타입을 수용할 수 있도록 만들어진다. 따라서 TypeScript에서 위와같이 any로 구현할 수 있다.  
하지만 any로 구현하게 되면 저장하고 있는 자료의 타입이 모두 같지않기 때문에 런타임에서 항상 타입검사를 해줘야한다.

```javascript
const stack = new Stack();
stack.push(1);
stack.push('1');
stack.pop().substring(0); //'a';
stack.pop().substring(0); // Throw TypeError;
```

그렇다고 자료형을 보장하기 위해 타입마다 스택을 상속받아 만들기는 코드가 너무 길어진다.  
스택 자료구조를 제네릭을 사용해 구현해보면 다음과 같다

```javascript
class Stack<T>{
    private data: T[]= [];
    constructor(){}

    push(item :T): void{
        this.data.push(item);
    }
    pop():T{
        return this.data.pop()
    }
}
```

<br>

클래스 식별자 선언부에 **<T>**라는 문법이 추가되었다. 제네릭을 사용하겠다는 의미로 타입으로 사용되는 식별자를 넣는다.  
**T**는 Type의 약자로 다른 언어에서도 제네릭을 선언할 때 관용적으로 많이 사용하는 표현이다.
이렇게 해서 클래스에서 제네릭을 사용하겠다고 선언한 경우 T는 해당 클래스에서 사용할 수 있는 특정한 타입이 된다.

사용법은 아래와 같다.

```javascript
const numberStack = new Stack<number>();
const stringStack = new Stack<string>();
numberStack.push(1);
string.push('a');
```

이제 각 스택은 항상 생성할 때 선언한 타입만을 저장하고 리턴한다. 이렇게 하면 컴파일러가 리턴하는 타입을 알 수 있게된다.

React의 useState훅도 제네릭과 같은 원리이다.

```javascript
const [state, setState] = useState < number > 0;
```

## 3. 함수에서 Generics 사용하기

A와 B의 타입이 어떤 것이 오는지 모르는 상황에서 any 라는 타입을 쓴다. 하지만 any를 쓰면 타입추론이 깨져버리기 때문에 무엇이 있는지 알 수 없다.  
 이런 상황에서 제네릭을 쓴다.

배열을 인자로 받아 그 배열의 첫번째 요소를 리턴하는 함수를 구현해보자.

```javascript
function first(arr: any[]): any {
  return arr[0];
}
```

위의 코드는 어떠한 마찬가지로 타입의 배열이라도 받을 수 있기 때문에 리턴하게 되는 타입이 무엇인지 알 수 없다.  
제네릭을 사용하면 간단하게 구현할 수 있다.

```javascript
function first(arr: T[]): T {
  return arr[0];
}
```

함수를 호출할 때 제네릭 문법으로 타입을 정해주기만 하면 된다.

```javascript
first < number > [1, 2, 3]; //1
```