# 💻 CORS란?

- CORS(Cross Origin Resource Sharing)
- 웹 서버에게 보안 cross-domain 데이터 전송을 활성화하는 cross-domain 접근 제어권을 부여한다.
- 추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제이다.

<br/>

- 배경

  - 처음 전송되는 리소스 도메인과 다른 도메인으로부터 리소스가 요청될 경우 해당 리소스는 cross-origin HTTP 요청에 의해 요청된다.
  - 보안 상 이유로 브라우저들은 스크립트 내 초기화되는 cross-origin HTTP 요청을 제한한다.

- 과정
  - CORS 요청 시 미리 OPTIONS 주소로 서버가 CORS를 허용하는지 물어본다.
  - 이때 Access-Control-Request-Method로 실제로 보내고자 하는 메서드를 알린다.
  - Access-Control-Request-Headers로 실제로 보내고자 하는 헤더들을 알린다.
  - Allow 항목들은 Request에 대응되는 것으로 서버가 허용하는 메서드와 헤더를 응답하는데 사용된다.
  - Request랑 Allow가 일치하면 CORS 요청이 이루어진다.
