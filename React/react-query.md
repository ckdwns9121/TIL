# react-query를 공부하고 정리한 내용

- react-query는 tanstack에서 만든 서버사이드 상태 관리 라이브러리이다.
- React앱에서 비동기 로직을 쉽게 다루게 해주는 라이브러리이다.

> servar state는 client state와 많은 부분에서 차이가 있다. 기존의 상태 관리 라이브러리들은 cient state 관리에 초점을 맞추고 있기 때문에 server state 관리에는 적합하지 않다.

지금껏 대중적으로 사용되었던 `redux-saga` 나 `redux-tuunk` 등이 **서버데이터를 다루는 것**에 적합하지 않다고 주장하며, 서버 데이터를 다루기 위한 아예 새로운 메커니즘을 제안한다.

클라이언트 상태의 대표적인 예시는 `모달의 open여부`, `JWT 값을 가졌는지?`, `input 값의 상태`  
서버 상태의 대표적인 예시는 **서버이서 가져온 데이터** (서버가 response해준 데이터) 이다.

서버 상태는 클라이언트에 의존한 데이터가 아니기 때문에 최신화에 대한 고민이 있으며, 데이터 캐싱 등에 대한 고민도 있다.

## 설치

```
$yarn add react-query
```

## react-query 사용방법

App.js에서 ContextProvider로 이하 컴포넌트를 감싸고 `queryClient`를 내보내 줘야한다. 이 context는 앱에서 비동기 요청을 알아서 처리하는 background 계층이 된다.

devTools를 사용하고 싶다면 `ReactQueryDevtools`를 import 해서 `QueryClientProvider`안에 넣어주면 된다.

```js
import { QueryClient, QueryClientProvider, useQuery } from 'react-query'
import { ReactQueryDevtools } from 'react-query/devtools';


const queryClient = new QueryClient()

export default function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {*/ ...Components */}
          <ReactQueryDevtools initialIsOpen={false} />
    </QueryClientProvider>
  )
}
```

react-query는 api 통신 로직 자체를 직접적으로 다루지는 않는다. 이 훅에서 제공하는 정확한 기능은 **비동기 함수와 그것의 리턴 값**에 대한 데이터 캐싱 등의 기능이다.

이는 각각의 데이터에 `query`라는 이름을 붙인다. 그리고 각각의 `query`마다 unique한 `key`값을 제공해야한다. 이 `key`값을 통해 해당하는 함수와 데이터를 식별하고, 그 데이터를 알아서 잘 처리해주는 것이다. 이를 `queryKey`라고 부른다. 사용법에 대한 자세한 정보는
[문서](https://react-query.tanstack.com/guides/query-keys) 에서 확인할 수 있다.

## 기존 상태관리

기존의 데이터 페칭에는 로딩, 에러, 데이터 관리 등을 위해 여러 훅을 사용해야 했으나 `react-query`를 사용하면 훨씬 간단하게 구현할 수 있다.

```js
// ❌ : 기존의 데이터 페칭 로직 시 사용하는 훅들
const [isLoading, setIsLoading] = useState(false);
const [isError, setIsError] = useState(false);
const [data, setData] = useState();

const fetchData = async () => {
  try {
    setIsError(false);
    setIsLoading(true);
    const response = await axios.get('https://jsonplaceholder.typicode.com/todos');
    setData(response.data);
    setIsLoading(false);
  } catch (err) {
    setIsError(true);
    setIsLoading(false);
    console.error(err);
  }
};

useEffect(() => {
  const tick = setInterval(fetchData, 3000);
  return () => clearInterval(tick);
}, []);
```

## useQuery 훅

```js
// ✅ : react-query를 사용하면 하나의 훅으로 모든 페칭에 연관된 상태를 한번에 제어할 수 있다.
const { status, data, error, isFetching } = useQuery(() => fetch(URL));
```

보통 서버에서 데이터를 불러올 때 useEffect에서 API요청을 하고 로딩상태 및 에러상태 등을 따로따로 직접 관리해야하는 불편함이 있었다.

코드도 복잡하고 가독성도 좋지않다. 여러 state를 페이지마다 반복적으로 사용하게 되고, 비동기 로직에 대한 추상화도 잘 이루어지지 않는다.

이를 `react-query`로 구현해보면 어떨까?

```js
const queryKey = ; // 당연히 보통 이렇게 변수 따로 안 만들고 useQuery 안에 바로 적습니다
const queryFn = ;

const { isLoading, data } = useQuery(
  'todos',
  async () => {
    const response = await axios.get('api/userapi' );
    return response.data;
  },
  {
    refetchInterval: 3000,
  }
);
```

훨씬 더 간결하게 비동기 관련 로직을 다 담을 수 있다.
`useQuery`훅은 더 나아가 `isFetching`, `isError` , `refresh`등의 다양한 상태들을 함수와 함께 제공해준다.

## useMutation

`useMutation` 훅은 서버 데이터의 생성/수정/삭제에 주로 사용된다. 데이터를 업데이트 하기 위한 비동기 함수를 인자로 갖고 뮤테이션을 실행하기위한 뮤테이트 함수를 반환한다.

아래는 todolist에 item을 추가하는 예제코드이다.

```js
function App() {
  const mutation = useMutation(newTodo => {
    return axios.post('/todos', newTodo);
  });

  // 배열 비구조화 할당으로 아래와 같이 mutate함수만 따로 들고올 수도 있다.
  const [mutate] = useMutation(newTodo => axios.post('/todos', newTodo));
  return (
    <div>
      {mutation.isLoading ? (
        'Adding todo...'
      ) : (
        <>
          {mutation.isError ? <div>An error occurred: {mutation.error.message}</div> : null}

          {mutation.isSuccess ? <div>Todo added!</div> : null}

          <button
            onClick={() => {
              mutation.mutate({ id: new Date(), title: 'Do Laundry' });
            }}
          >
            Create Todo
          </button>
        </>
      )}
    </div>
  );
}
```

## useMutation 사이드 이펙트 제어하기

`useMutation`은 라이프 사이클에서 쉽고 빠르게 사이드 이펙트를 제어하는 헬퍼 옵션의 함수를 제공한다.

```js
useMutation(addTodo, {
  onMutate: variables => {
    // A mutation is about to happen!

    // Optionally return a context containing data to use when for example rolling back
    return { id: 1 };
  },
  onError: (error, variables, context) => {
    // An error happened!
    console.log(`rolling back optimistic update with id ${context.id}`);
  },
  onSuccess: (data, variables, context) => {
    // Boom baby!
  },
  onSettled: (data, error, variables, context) => {
    // Error or success... doesn't matter!
  },
});
```

# useInfiniteQuery

`Infinite Scroll` 기법을 사용해서 데이터를 보고싶을 때 사용하는 훅이다. 공식문서에는 내용이 미비해 직접 사용해보고 정리하였다.

우선 공식문서에 나와있는 예제 코드는 아래와 같다.

```js
const { fetchNextPage, fetchPreviousPage, hasNextPage, hasPreviousPage, isFetchingNextPage, isFetchingPreviousPage, ...result } = useInfiniteQuery(
  queryKey,
  ({ pageParam = 1 }) => fetchPage(pageParam),
  {
    ...options,
    getNextPageParam: (lastPage, allPages) => lastPage.nextCursor,
    getPreviousPageParam: (firstPage, allPages) => firstPage.prevCursor,
  }
);
```

실제 영화 API를 받아오는 코드를 작성하고 `page`를 `1`씩 넘겨보겠다.

```js
import { getMoviesAPI } from '../api/movie';

const {
  isLoading,
  error,
  data,
  fetchNextPage,
  fetchPreviousPage,
  hasNextPage,
  hasPreviousPage,
  isFetchingNextPage,
  isFetchingPreviousPage,
  ...result
} = useInfiniteQuery('movies', ({ pageParam = 1 }) => getMoviesAPI(pageParam), {
  getNextPageParam: (lastPage, pages) => {
    return pages.length + 1;
  },
});

if (isLoading) return <>Loading..</>;
if (error) return <>An error has occurred</>;
return (
  <div className={styles['container']}>
    {data?.pages.map((movies, i) => {
      return <MovieList key={i} movies={movies} />;
    })}
    <button onClick={() => fetchNextPage()} disabled={!hasNextPage || isFetchingNextPage}>
      {isFetchingNextPage ? 'Loading more...' : hasNextPage ? 'Load More' : 'Nothing more to load'}
    </button>
  </div>
);
```

정리중
