# 제네릭

1. 함수에서 Generics 사용하기
 A와 B의 타입이 어떤 것이 오는지 모르는 상황에서 any 라는 타입을 쓴다. 하지만 any를 쓰면 타입추론이 깨져버리기 때문에 무엇이 있는지 알 수 없다.   
 이런 상황에서 제네릭을 쓴다.

```
    function merge<A,B> (a: A , b:B) : A & B{
        return{
            ...a,
            ...b
        }
    }
    const merged = merge({foo:1 }, {bar :1});
```

2. interface에서 Generic 사용하기

```
        interface Items<T> {
        list: T[];
        }

        const items: Items<string> = {
        list: ['a', 'b', 'c']
        };
```