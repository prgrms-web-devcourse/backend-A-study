# [HTTP의 발전 과정(0.9~2.0)](https://velog.io/@ddkk94/HTTP%EC%9D%98-%EB%B0%9C%EC%A0%84-%EA%B3%BC%EC%A0%950.92.0)

HTTP를 공부하면서 HTTP의 버전(0.9, 1.1, 2.0)별 기능을 조사했습니다.
# HTTP/0.9
- http 요청이 원 라인에 표기되고 요청 가능 메소드는 GET이 유일합니다.
- 그리고 전송 가능한 파일 포맷은 html이 유일했습니다.
### Request
```
GET /mypage.html
```
### Response
```html
<HTML>
A very simple HTML page
</HTML>
```
# HTTP/1.0
클라이언트와 서버 간의 제한적인 전송 해결을 위해 기능이 추가되었습니다.
- get 라인 다음 줄부터 추가 정보들이 붙기 시작했습니다.
### Request - 1
```
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)
```
### Response - 1
```html
200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
```

### Request - 2
```
GET /myimage.gif HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)
```
### Response - 2
```
200 OK
Date: Tue, 15 Nov 1994 08:12:32 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/gif
(image content)
```

# HTTP/1.1
HTTP/1.0 출시 몇 달만에 출간 된 HTTP의 첫번째 표준입니다.
- Connection Keep-Alive(지정한 timeout 동안 커넥션 연결을 유지)
- 청크로 응답 전송 가능
- 언어, 인코딩 혹은 타입을 추가
- Host 헤더 추가(동일 IP 주소에 다른 도메인을 호스팅 가능)
- Pipelining 기능 추가
### Request - 1
```
GET /en-US/docs/Glossary/Simple_header HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/en-US/docs/Glossary/Simple_header
```
### Response - 1
```html
200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Wed, 20 Jul 2016 10:55:30 GMT
Etag: "547fa7e369ef56031dd3bff2ace9fc0832eb251a"
Keep-Alive: timeout=5, max=1000
Last-Modified: Tue, 19 Jul 2016 00:59:33 GMT
Server: Apache
Transfer-Encoding: chunked
Vary: Cookie, Accept-Encoding
..(content)..
```
<details>
  <summary style="font-Weight : bold; font-size : 22px; color : #E43914;" >Pipelining</summary>
  <div>  
    <p>하나의 커넥션의 <strong>요청-응답</strong>이 하나의 사이클로 동작하지 않고, 순차적으로 <strong>요청1-요청2-요청3-응답1-응답2-응답3</strong> 순서대로 응답을 받아 지연 시간을 줄이는 방법입니다.
<img src="https://images.velog.io/images/ddkk94/post/4a0e9fc7-df69-4d9c-bc36-e7c08f677b99/image.png" alt=""></p>
  </div>
</details>
<details>
  <summary style="font-Weight : bold; font-size : 22px; color : #E43914;" >Transfer-Encoding: chunked</summary>
  <div>  
    <h3 id="chunk">Chunk</h3>
    <p>Header와 Data로 구성된 데이터의 묶음입니다.
      <img src="https://images.velog.io/images/ddkk94/post/6843bdd4-c934-4973-955c-04469d00900a/image.png" alt=""></p>
    <h3 id="chunk-encoding">Chunk Encoding</h3>
    <p>Server에서 동적으로 생성하는 데이터는 응답 시 총 데이터의 크기를 알 수 없습니다.</p>
    <ol>
      <li>Server는 보낼 데이터를 버퍼에 담아 하나의 Chunk 단위로 데이터를 묶습니다.</li>
      <li>Response마다 chunk를 데이터의 크기와 함께 전달합니다.</li>
      <li>남은 청크 데이터 크기가 0일때 모든 동적 데이터를 보낸 것으로 판단하여 연결을 종료합니다.</li>
    </ol>
  </div>
</details>

# HTTP/2
HTTP/1.1의 표준의 확장과 성능 향상에 초점을 목적으로 만들어졌습니다.
## 바이너리 프레이밍
  - 헤더와 데이터를 바이너리 데이터화 시켜서 파싱 및 전송 속도를 향상하고 오류 발생 가능성을 낮춥니다.

![](https://images.velog.io/images/ddkk94/post/42815df5-5869-4472-84c7-e53add5c14ab/image.png)
## 스트림, 메시지 및 프레임
- 스트림 : 구성된 연결 내에서 전달되는 바이트의 양방향 흐름
- 메시지 : 논리적 요청 또는 응답 메시지에 매핑되는 프레임의 전체 시퀸스
- 프레임 : HTTP/2의 통신 최소 단위, 각 최소 단위에 하나의 프레임 헤더가 포함
![](https://images.velog.io/images/ddkk94/post/fd58d2ed-cca5-47ef-b7fc-58f60bd0ef6e/image.png)

## 요청/응답 다중화(Request and Response multiflexing)
Head of Line 차단과 기본 TCP 연결의 비효율적인 사용을 막기 위해서 하나의 응답에 처리된 데이터를 묶은 여러 스트림을 모아 전달하는 다중화를 지원합니다.
![](https://images.velog.io/images/ddkk94/post/029c7533-20c0-446e-9cbc-74ec17cca8f4/image.png)
<details>
  <summary style="font-Weight : bold; font-size : 22px; color : #E43914;" >Head of Line이란</summary>
  <div>  
    <p>HTTP/1.1의 Pipelining의 문제점입니다. 이전 요청이 처리되지 않으면 이후 요청들까지 처리가 진행되지 않는 문제를 말합니다.
<img src="https://images.velog.io/images/ddkk94/post/bd3a400e-e6a6-41c3-babe-81558eb6d75e/image.png" alt=""></p>
  </div>
</details>

## 스트림 우선순위 지정
각 스트림의 가중치에 따라서 스트림의 처리에 할당하는 리소스를 추가합니다.
![](https://images.velog.io/images/ddkk94/post/7fcdb70e-1336-4d6d-a402-237e99102b18/image.png)

## 헤더 압축
각 프레임은 스트림에 종속되기 때문에 프레임의 헤더에 이미 존재하는 타입은 다시 표기하지 않음으로써 헤더의 크기를 줄입니다. 
![](https://images.velog.io/images/ddkk94/post/7daff5e1-76af-4841-8ee9-ae778b014bbc/image.png)

## 서버 푸시
클라이언트에서 요청하지 않은 내용을 서버에서 자체적으로 판단하여 추가해서 전달해주는 기능입니다.
![](https://images.velog.io/images/ddkk94/post/d53319b0-7cd6-4553-a76b-0b8bd6f92c17/image.png)

# HTTP/2.0까지의 공통적 특징
HTTP 2.0까지는 **TCP를 전송 계층을 활용하여 전송**됩니다. 하지만 TCP는 느린 전송 속도로 구조적으로 개선할 수 있는 속도의 한계가 있습니다. 이후 HTTP3에서는 UDP를 사용하여 속도를 향상시켰습니다. 다음 글에서는 QUIC와 HTTP 3의 동작 방식을 알아보겠습니다.

# 참고 자료
[쿨라임의 HTTP/1.1, HTTP/2, 그리고 QUIC](https://www.youtube.com/watch?v=xcrjamphIp4&t=623s)
[HTTP/2 소개](https://developers.google.com/web/fundamentals/performance/http2?hl=ko#%EC%8A%A4%ED%8A%B8%EB%A6%BC_%EB%A9%94%EC%8B%9C%EC%A7%80_%EB%B0%8F_%ED%94%84%EB%A0%88%EC%9E%84)
[HTTP의 진화](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP)
[Heap 구조, Chunk란?](https://cyber0946.tistory.com/101)
[청크 인코딩(Chunked transfer encoding)이란](https://blog.naver.com/PostView.nhn?blogId=claude17&logNo=221904720369&parentCategoryNo=&categoryNo=66&viewDate=&isShowPopularPosts=true&from=search)