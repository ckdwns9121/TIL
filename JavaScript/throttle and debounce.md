# Throttle 와 Debounce 개념정리

## 개념

- 쓰로들링: 마지막 함수가 호출된 후 일정 시간이 지나기 전에 다시 호출되지 않도록 하는 것 (스크롤링에 주로 사용)
- 디바운싱: 연이어 호출되는 함수들 중 마지막 함수만 호출하도록 하는것 (axios에서 주로 사용)

## 디바운싱

실시간 검색이나 추천 검색어 등을 구현할 때 사용하는 기법

디바운싱을 적용하지 않으면 문자 한글자 한글자마다 api 요청이 일어나기 때문에 성능적인 측면에서 좋지 않다.
만약 유료 API를 사용한다고 하면 비용적인 측면에서도 매우 손해가 크다.

디바운싱을 리액트로 구현해보자.  
주소를 검색하는 api에 실시간으로 보여지게 하고싶다.

```js
import { useState, useEffect } from 'react';

function useDebounced(value: string, delay: number) {
  const [debouncedValue, setDebouncedValue] = useState < string > value;

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);
    return () => {
      clearTimeout(timer);
    };
  }, [value, delay]);

  return debouncedValue;
}

export default useDebounced;
```

우선 값이 변경되는 `temp`값을 하나 만들고 useEffect에서 `디바운싱`을 구현했다.
만약 timer가 없으면 상태를 변경하고 timer가 있으면 새로 만들었다.

```js
...
const debounceSearchTerm = useDebounced(addr, 500);

const onSerchAddr =(async address =>{
   ///api
})
useEffect(() => {
    onSearchAddr(debounceSearchTerm);
}, [debounceSearchTerm]);

```

위와 같이 작성하면 API요청을 최적화 할 수 있다.
![디바운싱](./asset/디바운싱1.png)
