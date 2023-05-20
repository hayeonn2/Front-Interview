# 💻 REST API

## REST란?

REprsentational State Transfer의 약자로 전반적인 웹 어플리케이션에서 상호작용하는데 사용되는 웹 아키텍쳐 모델이다. 즉, 자원을 주고받는 웹 상에서의 통신 체계에 있어 범용적인 스타일을 규정한 아키텍쳐라고 할 수 있다.
<br/ >

## API란?

Application Programming Interface의 약자로 구글 맵 API, 카카오 비전 API 등 기존에 있는 응용 프로그램을 통해 데이터를 제공받거나 기능을 사용하고자 할 때 사용하는 인터페이스 및 규격을 말한다. API는 프로그래밍 언어, 운영체제 등에서도 사용되는 범용적인 용어다. 따라서 REST API라는 것은 REST 원칙을 적용해 서비스 API를 설계한 것을 말하며 대부분의 서비스가 REST API를 제공한다.

<br/>

## REST의 특징들

### 균등한 인터페이스 (Uniform Interface)

- REST가 HTTP의 표준만 따른다면 어떤 기술이던 접목해 사용할 수 있다.
- 플랫폼의 언어 제약에 구애받지 않는다.
- 요즘 REST API를 정의할 때 JSON 방식을 가장 많이 사용하지만 XML도 적용할 수 있다.
  <br/>

### 무상태성 (Stateless)

- 서버는 클라이언트 상황을 고려하지 않고 API 요청에 대해 처리하므로 이를 "상태가 없다"라고 표현한다.
- 클라이언트를 고려하지 않아도 되어서 구현이 간결해진다.

<br/>

### 캐싱 가능 (Cacheable)

- REST는 HTTP 표준을 기반으로 만들어졌기 때문에 HTTP의 특징인 캐싱을 사용할 수 없다.
- REST API를 활용해 GET 메소드를 Last-Modified 값과 함께 보낼 경우, 컨텐츠 변화가 없을 때 캐시된 값을 사용하게 된다.
- 이렇게 되면 네트워크 응답시간 뿐만 아니라 API 서버에 요청을 발생시키지 않아 부담이 덜하게 된다.

<br/>

### 자체 표현성 (Self-Descriptiveness)

- REST API의 자원명시 규칙, 메소드는 그 자체로 의미를 지닌다. 따라서 어떠한 요청에 있어 그 요청 자체로 어떤 것을 표현하는지 알아보기 쉽다.
- 물론 API를 규정한 각 서비스들이 문서를 제공하지만 이 특성에 따라서 요청하는 방식만으로 어떤 의미인지 알 수 있어야 좋은 REST API라고 할 수 있다.

<br/>

### 클라이언트-서버 구조 (Client-Server Architecture)

- REST 서버가 API를 제공하는 방식이므로 클라이언트에서 처리하는 부분과 독립적으로 동작한다.
- 따라서, 서로간 의존성 줄어들고 클라이언트와 서버를 최대한 독립적으로 개발할 수 있게 한다.

<br/>

### 계층형 구조 (Layered System)

- 클라이언트는 계층형 구조가 불가능하다.
- REST 서버 경우 보안/로드 밸런싱/암호화 등 추가할 수 있고 Proxy 및 게이트웨이 등 중간매체를 사용할 수 있다.
  <br/>

## REST API의 핵심

### URI는 리소스를 표현해야 한다.

- 리소스 명은 동사가 아닌 명사를 사용해야 한다.

```
/students/1
```

- 리소스는 Collection과 Document로 표현할 수 있다.

```
/locations/seoul/schools/3
```

여기서 locations는 Collection이고 seoul은 Document를 표현한다.

<br/>

### 그 리소스에 대한 행위는 HTTP의 Method로 표현해야 한다.

- GET은 리소스를 조회한다. (학생 목록 조회)

```
GET /students
```

- POST는 리소스를 생성한다. (학생 생성)

```
POST /students
```

- PUT은 리소스를 업데이트 한다. (1번 학생 정보 업데이트)

```
PUT /students/1
```

- DELETE는 리소스를 삭제한다. (1번 학생 삭제)

```
DELETE /students/1
```

<br/>

## HTTP 상태코드

요청에 대한 응답의 상태코드 또한 명확하게 돌려주는 것이 잘 설계된 REST API이다.

- 2xx: 성공 관련 (200 ok, 201 created)
- 3xx: 리다이렉션 관련 (304 Not Modified)
- 4xx: 클라이언트 에러 관련 (400 Bad Request, 401 Unauthorized)
- 5xx: 서버 에러 관련 (500 Internal Server Error)
  <br/>

## 잘못된 REST 사용

- GET/POST의 부적합한 사용: 기존 조회/생성 기능이 아닌 다른 방식으로 사용할 때
- 자체 표현적이지 않음: REST 특징 중 하나인 자체표현성에서 떨어지는 경우로 이해하기 힘듬
- HTTP 응답 코드 미사용: 위에서 정리한 응답에 관한 상태코드를 명확하게 정의하지 않은 경우
- 그 외 리소스 표현 가이드 및 REST 특징을 위반한 경우
