# [__HTTP와 HTTPS에 대하여...__](https://velog.io/@ddkk94/HTTP%EC%99%80-HTTPS%EC%97%90-%EB%8C%80%ED%95%98%EC%97%AC)
# markdown
웹에서 자주 볼 수 있는 http, https에 대하여 https를 쓰는게 안전하다는 정도로만 알고 있어서 이번 기회에 정확하게 차이를 알기 위해서 http, https에 대해서 조사했습니다.
# HTTP(Hyper Text Transfer Protocol)
인터넷에서 클라이언트와 서버가 요청과 응답을 통해서 데이터를 주고받을 수 있도록 해주는 규약입니다.
## 요청 메세지
![](https://images.velog.io/images/ddkk94/post/32626536-1e2e-4403-8ef5-607b55406a8e/image.png)
웹에서 클라이언트의 브라우저에서 url을 통해서 서버에 데이터를 요청 시 전달하는 http 메세지입니다.

#### header
시작 줄에 실행되어야 할 요청(GET,POST 등)이 기록됩니다.
*  <__요청 메소드__> <__url__> <__http버전__>

나머지 header 부분에 요청에 대한 옵션이 들어가게 됩니다.
#### body : POST 등 요청 시 전달할 필요가 있는 데이터를 body를 통하여 전달합니다.
## 응답 메세지
![](https://images.velog.io/images/ddkk94/post/4bfadb1b-3ee5-47ed-b3eb-8a434f3d677f/image.png)
서버에서 클라이언트에게 받은 요청에 대한 응답을 전달하는 http 메세지입니다.

#### header
시작 줄에 요청 수행에 대한 성공/실패가 기록됩니다.
* <__Http버전__> <__상태 코드__> <__상태 메세지__>

나머지 header 부분에 응답에 대한 옵션이 들어가게 됩니다.
#### body : 응답과 관련된 문서(html 등의 데이터)가 들어갑니다.

# HTTPS(Hypertext Transfer Protocol over Secure Socket Layer)
HTTP의 경우 클라이언트와 서버 간에 일반 텍스트 통신 대신에 SSL로 암호화 하여 데이터를 전달하여 보안을 높인 규약입니다.
대칭키와 공개키 방식 모두를 사용하여 데이터를 주고 받습니다.

## SSL(Secure Socket Layer)
대칭키/공개키를 사용하여 웹 브라우저와 서버 간의 전송 보안을 높이기 위해 만들어진 보안 소켓 레이어입니다.


## 대칭키
1개의 key로 데이터를 암호화/복호화할 수 있습니다.
장점
* 암호화/복호화 속도가 빠름
단점
* 안전한 키 교환이 어려움
![](https://images.velog.io/images/ddkk94/post/bb0a541b-867c-4590-9776-14a81fcc15e9/image.png)
## 비대칭키
암호화할 때와 복호화할 때 다른 키를 사용합니다.
공개키로 암호화 시 개인키로 복호화 가능하고, 개인키로 암호화 시 공개키로 복호화가 가능합니다.
![](https://images.velog.io/images/ddkk94/post/c237f3f2-ece6-4d8a-b5d7-fcc941b10f65/image.png)

## HTTPS 암호화 절차(SSL 동작 방식)
### CA와 Server
1. Server는 사이트가 정상적인 사이트임을 CA에게 Server의 정보와 Server의 공개키를 전달하여 심사를 받습니다.
2. CA는 심사한 결과 정상적인 사이트일 때 CA가 가진 개인키로 Server의 정보로를 암호화하여 인증서로 만들어서 전달한다.
![](https://images.velog.io/images/ddkk94/post/0ecd4426-9396-48f5-8bc5-57652dc1aa73/image.png)
### Client와 Server
1. Client의 브라우저에서는 이미 인증기관(CA)들의 공개키가 설치되어 있습니다.
2. Client에서 접속하는 Server(사이트)에 접속 요청 시 Server는 인증기관에서 받은 인증서를 먼저 응답합니다.
3. Client에서 인증서를 CA 공캐기로 복호화합니다.(Server의 공개키 획득)
4. Client에서 대칭키를 생성 후 Server의 공개키로 대칭키를 암호화하여 서버로 전달합니다.
5. Server에서 받은 암호화된 대칭키를 Server의 개인키로 복호화합니다.
6. 이제 서로 같은 대칭키를 가지게 되어 암호화/복호화한 HTTP 통신이 가능해집니다.
![](https://images.velog.io/images/ddkk94/post/d8832ed5-f1c9-4801-bfc4-96abf14f5204/image.png)


> 참고자료 
[MDN HTTP 문서](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages)
[SSL 인증서 구조 이해](https://m.blog.naver.com/alice_k106/221468341565)
