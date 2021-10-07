# [__RESTful API란?__](https://velog.io/@ddkk94/RESTful-API%EB%9E%80)

먼저 REST와 API의 개념을 알아보고 RESTful API의 의미를 확인해보겠습니다.
# REST(Representational State Transfer)
__웹 사이트의 컨텐츠(Text, 이미지, 동영상), DB의 내용__ 등을 전부 하나의 자원으로 파악하여 각 자원의 고유한 __URI(Uniform Resource Identifier)를 부여__하고, 해당 자원에 대한 __CRUD(Create, Read, Update, Delete) 작업__을 HTTP의 기본 명령어인 POST, GET, PUT, DELETE를 통해서 처리

## HTTP에서의 REST
> __자원__ : URL
__상태의 전달(행위)__ : HTTP Method(GET, POST, PUT, DELETE)
__표현__ : 전달하는 데이터의 형식(json, xml, text 등)

## REST 인터페이스의 원칙
1. 요청 내에 개별 자원의 식별
* HTTP에서 URL을 통해서 지키고 있습니다.
2. 메세지로 자원의 조작
* HTTP의 경우 GET, POST, DELETE, PUT으로 자원 조작을 요청할 수 있습니다.
>
메소드, CRUD, SQL 비교
![](https://images.velog.io/images/ddkk94/post/1e06512d-9dcd-40d5-80b1-f0dcde918a48/image.png)

3. 자기서술적 메세지
* 전달하는 메세지가 자신의 자원에 대해서 어떻게 처리하는지 xml, text처럼 파일 형식만으로 표현하는게 아닌 그 형식으로 어떻게 자원을 제어하는지 충분한 내용이 필요합니다.
4. 응답의 구분
* 클라이언트가 관련 리소스에 접근을 요청할 때, 응답하는 메세지에는 요청에 대한 응답인 것을 확인할 수 있는 지시자로 구별되어야 합니다.

## REST의 6가지 제한 조건
1. 클라이언트 - 서버 구조
* 자원이 있는 서버, 자원을 요청하는 Client의 구조를 가집니다.
2. 무상태(Stateless)
* 클라이언트와 서버는 서로의 통신에 대해서 독립적입니다.
3. 인터페이스 일관성
4. 캐시 처리 가능
* 클라이언트는 응답을 캐싱할 수 있어야 합니다.
5. 계층화
* 클라이언트는 API를 제공하는 서버가 어떤 식으로 연결되었는지 알 수 없도록 서버를 유연하게 구축하여 시스템 구모를 확장이 용이해야 합니다.
6. Code on demand(선택 사항)
* javaScript와 같이 서버는 클라이언트에서 실행될 수 있는 코드를 전송하여 기능을 확장시킬 수 있어야 합니다.

## 결국 REST란?
> __자원__을 __표현__해서 __상태를 전달__하는 것!!

# API(Application Programming Interface)
애플리케이션을 사용하여 프로그래밍하기 위해 제공하는 기능으로 볼 수 있습니다.

# REST API
REST의 특징을 기반으로 API를 제공하는 것으로 풀어서 설명하자면
__애플리케이션의 자원을 전달하기 위해서 제공하는 기능의 모음입니다.__

## REST API의 예시
[Kakao REST API](https://developers.kakao.com/docs/latest/ko/kakaologin/rest-api#request-code)
#### Request(URL)
```
GET /oauth/authorize?client_id={REST_API_KEY}&redirect_uri={REDIRECT_URI}&response_type=code HTTP/1.1
Host: kauth.kakao.com
```
#### Response
![](https://images.velog.io/images/ddkk94/post/5e0a26c4-b091-4cd2-a8d5-4fc3abd082e2/image.png)

# RESTful API
REST 아키텍처를 구현하여 기능을 제공하는 웹 서비스를 의미합니다.
## 참고자료
> [wikipedia의 REST](https://ko.wikipedia.org/wiki/REST)
[REST란](https://hckcksrl.medium.com/rest%EB%9E%80-c602c3324196)
[[Network] REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)
[SLiPP 위키](https://www.slipp.net/wiki/pages/viewpage.action?pageId=12878219#id-8%EC%A3%BC%EC%B0%A8-RESTAPI%EC%84%A4%EA%B3%84%EB%B0%8F%EA%B5%AC%ED%98%84-%EC%99%9CREST%EC%97%90%EB%8C%80%ED%95%9C%EA%B4%80%EC%8B%AC%EC%9D%84%EA%B0%80%EC%A7%80%EA%B2%8C%EB%90%98%EC%97%88%EC%9D%84%EA%B9%8C?)
[Kakao REST API](https://developers.kakao.com/docs/latest/ko/kakaologin/rest-api)