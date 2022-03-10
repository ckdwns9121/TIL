# react-router-dom v6

## 설치

```
$ npm install react-router-dom@6
```

## Switch 대신 Routes

### 기존코드

```js
<Switch>
  <Route path="/login" component={Login} />
</Switch>
```

### v6코드

```js
<Routes>
  <Route path="/login" element={<Login />} />
</Routes>
```

## Route에 component 대신 element 사용

### 기존코드

```js
<Route path="/" exact component={HomePage} />
<Route path="/login" exact>
    <LoginPage />
</Route>
```

### v6코드

```js
<Route path="/" exact element={<HomePage />} />
<Route path="/login" exact element={<LoginPage />} />
```

## exact는 삭제

### 기존코드

```js
<Route path="/login" exact component={UsersPage} />
```

### v6

```js
<Route path="/login" element={<UsersPage />} />
```

여러 라우팅을 매칭하고 싶은 경우 URL 뒤에 `*`을 사용한다.

```js
<Routes>
  <Route path="member/*" element={<Member />} />
</Routes>
```

## 중첩 라우팅

```js
//v5
<Switch>
  <Route path="/member" />
  <Route path="/member/:memberId" />
</Switch>

//v6
<Routes>
  <Route path="/member">
    <Route path=":memberId" /> // /member/:memberId
  </Route>
</Routes>
```

## 404 Not Found

`path="*"` 경로는 모든 URL과 일치하지만 가장 하위 우선 순위를 가지므로 일치하는 다른 경로가 없을 경우 렌더링 된다.

```js
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="dashboard" element={<Dashboard />} />
  <Route path="*" element={<NotFound />} />
</Routes>
```

## useHistory 대신 useNavigate

### v5코드

```js
const history = useHistory();

history.push('/');
history.goback();
history.go(-2);
history.push(`/user/${user._id}`);
```

### v6코드

```js
const navigate = useNavigate();

navigate('/');
navigate(-1);
navigate(-2);
navigate(`/user/${user._id}`);
```

## Optional URL 파라미터 사라짐. 필요하면 Route 2개 만들어야 함

### 기존코드

```js
<Route path="/optional/:value?" component={Optional} />
```

### v6

```js
<Route path="/optional/:value?" element={<Optional />} />
<Route path="/optional" element={<Optional />} />
```

## :id path 이용하기

```js
import React from 'react';
import { useParams } from 'react-router';

const WebPost = () => {
  const { id } = useParams();
  return <div>#{id}번째 포스트</div>;
};

export default WebPost;
```

## 중첩 라우팅

v5 에서는 하나의 파일에 모든 경로를 지정하고 `path`를 얻어 이를 추가 조합하는 방식으로 구성했다.

### 기존코드

```js
// app.js
<Switch>
  <Route path="/user" component={User} />
</Switch>
```

```js
// user.js
<Switch>
  <Route path={`${path}/detail`}>
    <UserDetail />
  </Route>
</Switch>
```

### v6코드

```js
<Routes>
  <Route path="user" element={<User />}>
    <Route path="detail" element={<UserDetail />} />
  </Route>
</Routes>
```

```js
function User() {
  return (
    <>
      <Outlet />
    </>
  );
}
```

## Outlet
