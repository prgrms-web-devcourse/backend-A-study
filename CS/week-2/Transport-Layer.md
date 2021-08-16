# Network | 전송 계층 (TCP, UDP)

## 1. 전송 계층(Transport Layer)

> **종단 간(End-To-End) 통신을 다루는 계층으로 종단 간 신뢰성 있고 효율적인 데이터를 전송한다.**
>
> - 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해준다.
> - 프로토콜(TCP, UDP)로 구성되어 오류 제어, 흐름 제어, 혼잡 제어 등을 담당한다.
> - 순차 번호 기반의 오류 제어 방식을 사용한다.
> - 대표적인 전송 계층 장비로는 L4 스위치가 있다.

송신자와 수신자를 연결하여 신뢰성 있는 데이터를 전송할 수 있게 해주는 계층이다. 쉬운 이해를 위해 편지를 보내는 과정에 비유해보겠다. 우체국에 가서 편지를 보낼 때 우리는 다음과 같이 2가지 정보를 작성할 것이다.

1. 편지를 받는 사람의 주소 => IP, MAC
2. **편지를 받는 사람 => Port**

여기서 만약 편지를 받는 사람의 정보가 없다고 생각해보자. 어디 아파트로 가야 하는지는 알지만 누가 받아야 하는지를 모르기 때문에 편지는 제대로 전달될 수가 없을 것이다. 데이터를 전송하는 과정도 이와 동일하다. **데이터를 단지 컴퓨터(아파트)로만 보내는 것이 아닌 특정 애플리케이션(받는 사람)으로 보내는 것이 목적**이기 때문에 받는 사람이 반드시 명시되어야 한다.

**즉, 전송계층은 애플리케이션이라는 최종 목적지까지 데이터를 문제없이(신뢰성, 효율성) 전송하기 위한 계층이다.**



![img](https://raw.githubusercontent.com/soo5717/Typora-image/velog/img/image-20210812192517461.png)





전송 계층에서는 세션 계층에서 전달된 데이터를 받아 실질적인 전송을 위해서 일정 크기로 나눈다. 이렇게 나누어진 데이터에는 **출발지 포트(보낸 이), 목적지 포트(받는 이), 순서 번호, 오류 검출 코드 등**이 **헤더**로 붙게 되는데 이것을 **세그먼트(Segment)**라고 부른다. 이렇게 만들어진 세그먼트들을 네트워크 계층으로 보내면 네트워크 계층의 헤더가 붙어 패킷(Packet)이 되는 것이다.

> [Protocal Data Uni(PDU)](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C_%EB%8D%B0%EC%9D%B4%ED%84%B0_%EB%8B%A8%EC%9C%84) - 데이터 통신에서 상위 계층이 전달한 데이터에 붙이는 제어정보를 뜻한다.

![OSI_Model](https://raw.githubusercontent.com/soo5717/Typora-image/velog/img/OSI_Model.png)

## 2. 전송 계층 프로토콜(TCP, UDP)

> 전송 계층의 대표적인 프로토콜로는 TCP(연결 지향), UDP(비연결 지향)이 있다. 
>
> - `연결 지향` : 상대가 데이터를 받았는지 확인하면서 통신하는 방식
> - `비연결 지향` : 상대가 데이터를 받았는지 확인하지 않고 일방적으로 통신하는 방식

| **기능 및 특성** | **TCP(Transmission Control Protocol)** | **UDP(User Datagram Protocal)** |
| ---------------- | -------------------------------------- | ------------------------------- |
| 연결 방식        | 연결 지향                              | 비연결 지향                     |
| 전달 순서        | 순서 보장                              | 순서 보장하지 않음              |
| 확인 응답        | 확인                                   | 확인하지 않음                   |
| 통신 방식        | 1:1                                    | 1:1, 1:N, N:N                   |
| 속도             | 느림                                   | 빠름                            |
| 신뢰성           | 높다                                   | 낮다                            |

TCP는 등기 우편, UDP는 일반 우편으로 생각하면 이해가 쉽다. 

- TCP(등기 우편)의 경우 상대가 받았는지를 확인할 수 있기 때문에 상대가 받지 못했을 경우 다시 보내줄 수 있다.
- UDP(일반 우편)의 경우 상대가 받았는지 여부를 확인할 수 없기에 상대가 받지 못했을 경우에도 다시 보내지 않는다.

### **TCP(Transmission Control Protocol)**

> 연결 지향 통신으로 신뢰할 수 있으며 데이터를 순서대로 에러 없이 전송한다.
>
> - 패킷의 손실, 중복, 순서 변경이 없음을 보장한다.
> - 오류 제어, 흐름 제어, 혼잡 제어를 담당한다.
>   - 흐름 제어 : 송신 및 수신 속도를 일치시킨다.
>   - 혼잡 제어 : 네트워크 혼잡 시 데이터 전송 속도를 강제로 줄인다.

#### TCP Segment Header Format

![image-20210816022602254](https://raw.githubusercontent.com/soo5717/Typora-image/velog/img/image-20210816022602254.png)

- Source Port : 출발지 포트 번호 
- Destination Port : 목적지 포트 번호
- Sequence Number : 보내는 순서 번호
- Acknowledgment Number(ACK): 받은 순서 번호
- Data Offset : TCP 헤더 길이
- Flags : 제어 비트 (세그먼트 종류 표시)
- Window Size : 확인 메시지 없이 전송할 수 있는 세그먼트 최대 크기
- Chechsum : 헤더와 데이터 에러 검출
- Urgent Pointer : 긴급 데이터 위치
- Option : 추가 옵션

### **UDP(User Datagram Protocal)**

> 비연결 지향 통신으로 신뢰성이 없으며 순서 없이 데이터를 전송한다.
>
> - **신뢰성이나 정확성 보다는 효율을 중시한다.**
> - 빠른 처리가 필요한 실시간 스트리밍 서비스 등에서 활용된다.

#### UDP Datagram Header Format

![image-20210816022614764](https://raw.githubusercontent.com/soo5717/Typora-image/velog/img/image-20210816022614764.png)

- Source Port : 출발지 포트 번호 
- Destination Port : 목적지 포트 번호
- Lenth: 전체 UDP 길이
- Chechsum : 헤더와 데이터 에러 검출

### 참고 자료

- [TCP Segment Vs UDP Datagram Header Format](https://skminhaj.wordpress.com/2016/02/15/tcp-segment-vs-udp-datagram-header-format/)

- [[이해하기] TCP와 UDP (TCP vs UDP)](https://www.stevenjlee.net/2020/06/29/%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-tcp-%EC%99%80-udp-tcp-vs-udp/)