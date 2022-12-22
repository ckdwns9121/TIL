# 📒 REST API 정리

## REST란?

REST(Representational State Transfer)는 로이 필딩이 자신의 2000년 박사 학위 논문에 정의한 네트워크 소프트웨어 아키텍쳐이다.

## 조건

- Client-Server
  - 클라이언트와 서버로 분리되어야 하며 서로 의존성이 없어야한다.
  - REST 서버는 API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
- Stateless(무상태성)
  - 상태 정보를 따로 저장하지 않으며, 이용자가 누구인지 혹은 어디서 접근하는지와 관계 없이 결과가 무조건 동일해야 한다.
  - 이전 요청이 다음 요청의 처리에 연관되면 안된다.(이전 요정이 DB를 수정해 바뀌는 것 제외)
- Cache
  - HTTP를 비롯한 네트워크 프로토콜에서 제공하는 캐싱 기능을 적용할 수 있어야 한다.
- Uniform Interface(인터페이스 일관성)
  - URI로 지정한 자원에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 것을 말한다.
  - HTTP 표준인 URL과 응답코드, Request-Response Method 등을 사용한다.
- Layered System(계층화)
  - Client는 REST API Server만 호출한다.
  - REST API Server는 다충 계증으로 구성된다.

## REST API란?

API(Application Programing Interface)란 응용 프로그램 프로그래밍 인터페이스로 프로그래밍에서, 프로그램을 작성하기 위한 일련의 상호작용 할 수 있는 `인터페이스` 사양을 말한다.

REST API는 REST 기반으로 API를 구현한 것이다. 즉, HTTP 요청을 보낼 때 어떤 URL에 어떤 메소드를 사용할 지 개발자들 사이에서 지켜지는 약속이다.

## REST API 설계 규칙

- URI는 정보의 장원을 표현해야 한다.
  - resource는 동사보다는 명사를, 대분자보다는 소문자를 사용한다.
  - resource의 스토어 이름으로 복수 명사를 사용해야 한다.
- 자원에 대한 요청은 GET,POST,PUT,DELETE 등 HTTP Method로 표현한다.
  - HTTP Method나 동사표현이 URI에 들어가면 안된다.
  - `:id`와 같이 변하는 값은 하나의 특정 resource를 나타내는 고유값이어야 한다.

### 잘못된 사례

- URI에 HTTP Method가 들어간 경우

```
GET /chatrooms/get/:id
POST /chatrooms/create
GET /chatrooms/delete/:id
POST /chatrooms/update/:id
```

- 대문자를 사용한 경우

```
GET /users/postComments X
GET /users/post-comments O
```

- 언더바 대신 하이픈

```
GET /users/post_comments X
GET /users/post-comments X
```

- 행위를 포함하지 않는다

```
DELETE /user/1/delete-post/1 X
DELETE /user/1/posts/1 O
```

- 파일 확장자를 URI에 포함시키지 않는다.

```
GET /users/photo.jpg x
GET /users/photo o
```
