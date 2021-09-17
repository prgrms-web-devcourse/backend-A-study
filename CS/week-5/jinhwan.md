# [__DNS 동작 원리__](https://velog.io/@ddkk94/DNS-operation)

# DNS란(Domain Name System)
> 도메인 이름을 네트워크 주소로 변환하거나 반대의 작업을 수행하는 서버입니다.


# DNS가 필요한 이유
> 숫자로 구성된 네트워크 주소는 기억하기 힘들기 때문에 사람이 기억하기 편한 체계로 변경하기 위해서 도메인을 주소로 사용하기 시작했습니다.

# 웹 페이지 로드를 위한 DNS의 종류
### 재귀 확인자(DNS Recursor, Local Name Server)
- 개인이나 기업체에게 인터넷 접속 요청하는 ISP(Internet Service Provider)에서 Domain 이름을 요청하여 받게 됩니다.
- 캐시된 IP 주소가 있으면 그대로 반환하고 없다면 IP 주소를 얻기 위해 다른 DNS 서버와 중개하는 역할을 합니다.
### 루트 네임서버(Root Name Server)
- Local Name Server로부터 Domain 주소를 받아서 네트워크 주소로 변환해 주는 서버입니다.
- Server에 변환할 IP 주소가 없다면 마지막 도메인 네임(.com, net 등)을 반환하여 TLD Server에 요청해야한 데이터를 Local Name Server에 응답합니다.
![](https://images.velog.io/images/ddkk94/post/9c837f30-7479-4211-9c3f-501a92b59e47/image.png)
### TLD 네임서버(Top Level Domain)
- ICANN의 지사인 IANA(Internet Assigned Numbers Authority)가 관리합니다.
- TLD 서버의 종류는 일반 최상위 도메인(.com, .net 등)과 국가 코드 최상위 도메인(.kr, .us, .jp 등)이 있습니다.
- 마지막 도메인 네임 정보(.com, net 등)로 TLD 네임 서버에서 IP 주소를 찾습니다.
- TLD 네임 서버에 IP 주소가 없으면 연결된 Domain 주소의 TLD 서버로 연결시키면서 권한 있는 네임 서버에 보낼 데이터를 Local Name Server로 전달합니다.
### 권한 있는 네임 서버(authoritative name Server)
- TLD 서버로부터 Local Name Server로 응답받은 데이터를 권한 있는 네임 서버로 전달합니다.
- Local Name Server로 IP 주소를 응답 받습니다.
![](https://images.velog.io/images/ddkk94/post/d53d0d9a-6359-48ea-9805-0f6bf0dd10d3/image.png)

# 참고 사이트
> [DNS서버(네임서버)의 이해](https://webdir.tistory.com/161)
> [DNS란 무엇입니까? | DNS 작동 원리](https://www.cloudflare.com/ko-kr/learning/dns/what-is-dns/)
> [DNS 기본 동작 과정](https://effectivesquid.tistory.com/entry/DNS-%EA%B8%B0%EB%B3%B8-%EB%8F%99%EC%9E%91-%EA%B3%BC%EC%A0%95?category=654574)
> [전 세계 루트 DNS 운영 현황](https://xn--3e0bx5euxnjje69i70af08bea817g.xn--3e0b707e/jsp/statboard/dns/dnsRoot/currentWorld.jsp)