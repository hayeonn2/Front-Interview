# 💻 TCP 3-way-handshaking & 4-way-handshaking

TCP는 네트워크 계층 중 <b>전송 계층</b>에서 사용하는 프로토콜 중 하나로 <b>신뢰성을 보장하는 연결형 서비스</b>이다.
<br/>
TCP의 3-way-handshaking이란 TCP 통신을 시작하기 전에 논리적인 경로 연결을 수립하는 과정이며, 4-way-handshaking은 논리적인 경로 연결을 해제하는 과정이다.
이런 방식을 Connect Oriented 방식이라고 부르기도 한다.
<br/>

## 🏷️ TCP 3-way-handshaking : Connection Establish

TCP 통신을 이용해 데이터를 전송하기 위해 연결을 설정하는 과정이다.

- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장한다.
  <br/>

<b>A 프로세스(클라이언트)가 B 프로세스(서버)에 연결을 요청</b>

1. A(CLOSED) → B(LISTEN) : SYN(a)
   - 프로세스 A가 연결 요청 메시지 전송 (SYN)
   - 이때 Sequence Number를 임의의 랜덤 숫자(a)로 정하고 SYN 플래그 비트를 1로 설정한 segment를 전송한다.
2. B(SYN_RCV) → A(CLOSEd) : ACK(a+1), SYN(b)
   - 연결 요청 메시지를 받은 프로세스 B는 요청을 수락(ACK)했으며 요청한 A 프로세스도 포트를 열어달라(SYN)는 메시지 전송한다.
   - 받은 메시지 수락에 대해서는 Acknowledgement Number 필드를 (Sequence Number + 1)로 지정해 표현한다.
   - SYN과 ACK 플래그 비트를 1로 설정한 segment를 전송한다.
3. A(ESTABLISHED) → B(SYN_RCV) : ACK(b+1) - 마지막으로 프로세스 A가 수락 확인을 보내 연결을 한다.(ACK) - 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있다.
   최종 포트 상태 : A-ESTABLISHED, B-ESTABLISHED (연결 수립)

<br/>

## 🏷️ TCP 4-way-handshaking : Connection Termination

<b>A 프로세스(클라이언트)가 B 프로세스(서버)에 연결 해제를 요청</b>

1. A(ESTABLISHED) → B(ESTABLISHED) : FIN

   - 프로세스 A가 연결을 종료하겠다는 FIN 플래그를 전송한다.
   - 프로세스 B가 FIN 플래그로 응답하기 전까지 연결을 계속 유지한다.

2. B(CLOSE_WAIT) → A(FIN_WAIT_1) : ACK

   - 프로세스 B는 일단 확인 메시지(ACK)를 보내고 자신의 통신이 끝날 때까지 기다린다.
   - Acknowledgement Number 필드를 (Sequence Number + 1)로 지정하고 ACK 플래그 비트를 1로 설정한 segment를 전송한다.
   - 자신이 전송할 데이터가 남았다면 계속 전송한다. (클라이언트 쪽에서도 서버로부터 받지 못한 데이터가 있을 것을 대비해 일정 시간 세션을 남겨놓고 패킷을 기다린다. → TIME_WAIT 상태)

3. B(CLOSE_WAIT) → A(FIN_WAIT_2) : FIN

   - 프로세스 B의 통신이 끝나면 연결 종료해도 괜찮다는 의미로 프로세스 A에게 FIN 플래그를 전송한다.

4. A(TIME_WAIT) → B(LAST_ACK) : ACK
   - 프로세스 A는 FIN 메시지를 확인했다는 메시지 전송(ACK)
   - 프로세스 A로부터 ACK 메시지를 받은 프로세스 B는 소켓 연결을 해제한다.

최종 포트 상태 : A-CLOSED, B-CLOSED (연결 해제)
<br/>

### 🏷️ 포트(PORT) 상태 정보

- CLOSED : 포트가 닫힌 상태
- LISTEN : 포트가 열린 상태로 연결 요청 대기 중
- SYN_RCV : SYNC 요청을 받고 상대방의 응답을 기다리는 중
- ESTABLISHED : 포트 연결 상태
  <br/>

### 🏷️ TCP Header 안의 플래그 정보

- TCP Header에는 CONTROL BIT(플래그 비트, 6bit)가 존재하며 각각의 비트는 "URG-ACK-PSH-RST-SYN-FIN"의 의미를 가진다.

  - 즉, 해당 위치의 bit가 1이면 해당 패킷이 어떤 내용을 담고 있는 패킷인지를 나타낸다.

- SYN(Synchronize Sequence Number)

  - 연결 설정 / 000010
  - Sequence Number를 랜덤으로 설정해 세션을 연결하는데 사용, 초기에 Sequence Number를 전송한다.

- ACK(Acknowledgement)

  - 응답 확인 / 010000
  - 패킷을 받았다는 것 의미
  - Acknowledgement Number 필드가 유효한지 나타낸다.
  - 양단 프로세스가 쉬지 않고 데이터를 전송한다고 가정하면 최초 연결 설정 과정에서 전송되는 1번째 세그먼트를 제외한 모든 세그먼트의 ACK 비트는 1로 지정된다고 생각할 수 있다.

- FIN(Finish)
  - 연결 해제 / 000001
  - 세션 연결을 종료시킬 때 사용, 더 이상 전송할 데이터가 없음을 의미한다.
