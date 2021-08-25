# Network | TCP Handshaking

> TCP 3 Way Handshaking, TCP 4 Way Handshaking에 관해 설명한 글입니다. TCP에 관한 내용은 [Network | 전송 계층 (TCP, UDP)](https://velog.io/@soo5717/Transport-Layer)을 참고해주세요.



## 1. TCP Handshaking

> 전송 계층에서 **신뢰성 있는 세그먼트 전송 보장을 위해, 송신 측과 수신 측간 TCP Connection 수립 및 전달, 종료** 되도록 TCP Flags 기반 동작을 수행하는 접속 규약이다.
>
> - 연속적인 데이터 전송의 신뢰성을 위해서 논리적 연결을 만들게 되는데 이때 상대와 연결 상태를 만들거나 해제하기 위해 거치는 특별한 과정을 핸드셰이킹이라고 한다.

TCP 핸드셰이킹에 필요한 Flag부터 먼저 알아보자. 주요한 플래그는 다음과 같다.

- `SYN` - synchronize **sequence numbers**의 약자로 **연결 시작 요청**을 의미한다.
  - 상대방과 연결을 생성할 때 시퀀스 번호를 동기화하기 위한 세그먼트임을 의미한다.
- `ACK` - acknowledgment의 약자로 **응답 확인(승인 번호)**을 의미한다.
- `FIN `- finish의 약자로 **연결 종료 요청**을 의미한다.

![9910A8345BB0B75F2A](https://raw.githubusercontent.com/soo5717/Typora-image/velog/img/9910A8345BB0B75F2A.png)

## 2. TCP 3 Way Handshaking

> TCP 3 방향 핸드셰이킹은 전송 계층에서 송신 측과 수신 측 간 TCP 연결 설정, 수락, 확인의 세 가지 절차를 거치는 **연결 설정 규약**이다.
>
> - 송신 측과 수신 측 모두 데이터를 전송할 준비가 되었다는 것을 보장한다.

![3way](https://raw.githubusercontent.com/soo5717/Typora-image/velog/img/3way.png)



1. 클라이언트는 서버에 접속을 요청하는 `SYN`을 보낸다.
   - 클라이언트는 `SYN`을 보내고 서버가 `SYN/ACK`을 보내올 때까지 기다리는 **SYN-SENT 상태**가 된다.

2. 서버는 클라이언트로부터 `SNY` 요청을 받고 클라이언트에서 요청을 수락한다는 `SYN/ACK`을 보낸다.
   - 요청을 보낸 서버는 클라이언트가 `ACK`을 보내올 때까지 기다리는 **SYN-RECEIVED 상태**가 된다.
   - 실제 데이터를 주고받을 때는 **상대방이 보낸 시퀀스 번호 + 상대방이 보낸 데이터의 byte**를 합쳐서 `ACK`을 만든다.
   - 하지만 핸드셰이킹 과정에서는 데이터를 주고받기 전이기 때문에 byte를 더할 수 없으니 순서 구분을 위해  **시퀀스 번호 + 1**을 한 `ACK`을 클라이언트에게 보낸다.
3. 클라이언트가 서버에게 `ACK`을 보내게 되면 이후로는 연결이 이루어지고 데이터가 오가게 된다.
   - 서버가 클라이언트로부터 `ACK`을 받으면 연결이 성립된 시점부터 서버는 **ESTABLISHED 상태**이다.

## 3. TCP 4 Way Handshaking

> TCP 4 방향 핸드셰이킹은 전송 계층에서 송신 측과 수신 측 간 서로 연결을 종료할 때 수행하는 **접속 종료 규약**이다.
>
> - 종료할 때는 더 예기치 못한 상황이 많아서 확인 과정이 복잡한 4 방향 핸드셰이킹을 사용한다.
>   - 연결을 생성할 때 연결이 실패할 경우는 다시 시도하면 되지만, 이미 생성된 연결을 종료하는 과정에서 문제가 발생한다면 연결이 종료되지 못하고 그대로 남아있는 문제가 생기기 때문이다.

![4way](https://raw.githubusercontent.com/soo5717/Typora-image/velog/img/4way.png)

1. 클라이언트가 연결을 종료를 요청하는 `FIN`을 보낸다. 
   - `FIN`을 보낸 클라이언트는 **FIN-WAIT 상태**가 된다.

2. 서버는 `FIN` 요청을 받고 일단 확인 응답으로 `ACK`을 보낸다. 
   - `ACK`을 보낸 서버는 자신의 통신이 끝날 때까지 **CLOSE-WAIT 상태**를 유지한다.

3. 연결을 종료할 준비가 끝나면 연결 해지를 위한 준비가 되었음을 알리기 위해 서버가 클라이언트에 `FIN`을 보낸다.
   - `FIN`을 보낸 서버는 **LAST-ACK 상태**가 된다. 

4. 클라이언트는 서버로부터 `FIN`을 받고 해지 준비가 되었다는 것을 확인했다는 의미로 `ACK`을 보낸다.
   - 클라이언트의 상태가 FIN-WAIT에서 **TIME-WAIT 상태**로 변경된다.
   - `ACK`를 받은 서버의 상태는 **CLOSED 상태**가 된다.

>  서버에서 전송한 패킷이 라우팅 지연이나 패킷 유실로 인한 재전송 등으로 `FIN` 패킷보다 늦게 도착하는 상황이 발생할 수도 있으므로 클라이언트는 이러한 현상을 대비해 서버로부터 `FIN`을 받은 후 일정 시간(default 240초) 동안 세션을 남겨두고 잉여 패킷을 기다린다.
>
>  - 이때 클라이언트의 상태를 **TIME-WAIT 상태**라고 한다. 일정 시간이 지난 후에야 세션을 만료 및 연결이 종료된 **CLOSE 상태**가 된다.

### 참고 자료

- [TCP Flag 종류 (TCP 제어 플래그 종류와 기능)](https://cezacx2.tistory.com/1256)
- [TCP 통신 과정 및 비정상 종료(TCP 3,4-way handshake)](https://www.crocus.co.kr/1362)

- [[네트워크] 3-way / 4-way Handshake 란?](https://bangu4.tistory.com/74)
- [TCP가 연결을 생성하고 종료하는 방법, 핸드쉐이크](https://evan-moon.github.io/2019/11/17/tcp-handshake/)