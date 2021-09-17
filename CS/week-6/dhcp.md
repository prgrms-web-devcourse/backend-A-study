# [DHCP 동작 원리](https://velog.io/@ddkk94/DHCP)

# DHCP(Dynamic Host Configuration Protocol)
> * 내 PC에 할당하는 네트워크 정보(**유무선 IP 환경에서 단말의 IP 주소, 서브넷 마스크(Subnet Mask), 디폴트 게이트웨이(Default Gateway) 등**) 관리합니다.
> * 서버/클라이언트 모델을 사용합니다.

# DHCP vs DNS
### DHCP
- DHCP 서버를 통해서 송신처인 자신의 IP를 할당하는 방법
### DNS
- domain name을 통해서 수신처의 IP를 알아내는 방법

# DHCP 동작 방식
![](https://images.velog.io/images/ddkk94/post/bf9344c3-c80d-478a-b080-693cec3d7e51/image.png)

- DISCOVER
  - DHCP 서버를 찾는 요청으로 DHCP DISCOVER를 서버에 전달
- OFFER
  - DHCP에서 IP 주소 Pool에 들어있는 IP 주소를 선택하여 클라이언트들에 브로드캐스트하여 통지
- REQUEST
  - 클라이언트에서 OFFER 받은 IP 주소가 정상적인지 확인하고 서버에 REQUEST 전달
- ACK
  - REQUEST를 받은 서버에서 문제가 없을 때 네트워크의 추가 정보들을 ACK로 응답

# 참고자료
[DHCP 개념 및 동작 이해하기](https://ja-gamma.tistory.com/entry/DHCP%EA%B0%9C%EB%85%90%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC)

[DHCP, DNS란 무엇인가?](https://www.crocus.co.kr/1414)