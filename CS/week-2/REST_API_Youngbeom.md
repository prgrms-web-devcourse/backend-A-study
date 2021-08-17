[원문 블로그 바로가기](https://velog.io/@youngblue/REST-API%EC%9D%98-%EB%A9%94%EC%86%8C%EB%93%9C%EB%93%A4%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)

# REST API의 메소드와 설계 가이드

---

## REST API란 무엇인가?

Representational state transfer의 약자로, 월드 와이드 웹(www)과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처의 한 형식으로 엄격한 의미로는 네트워크 아키텍처의 모음이며 백엔드와 클라이언트의 커뮤니케이션 방식을 의미한다.
이때 REST API는 REST기반으로 서비스 API를 구현한 것을 의미한다.

REST API에서 HTTP Method를 이용해 리소스에 대한 CRUD를 하게 되는데 __이때 사용하는 Method가 GET, POST, PUT, DELETE__ 등 이다.
* CRUD : Create, Read, Update, Delete 의 약어로 데이터를 생성하고 읽고 수정하고 삭제하는 등의 행위를 뜻한다.


## REST의 구성요소
- 자원(RESOURCE) - URL
자원은 데이터를 의미하고 다른말로는 리소스를 뜻한다.
이러한 리소스는 URI(URL)을 통해서 표현된다.

여러 개의 데이터를 한번에 사용하고 싶다면 데이터를 묶음의 URI로 사용하는데 이를 
Collection이라고 한다.
컬렉션 안에 있는 각각의 데이터를 Element라고 부르며 REST API에서는 슬래시('/')로 구분한다.


- 행위(Verb) - HTTP Method
리소스는 데이터이기 때문에 어떠한 작업을 할 수 없다.
그렇기 때문에 반드시 행위를 통해 데이터를 수정하거나 생성 등의 작업을 해야한다
이 행위를 하는 방법(Method)에는 GET, POST, PUT, DELETE가 존재한다


## HTTP Method
|CRUD|METHOD|Method|
|:---:|:---:|---|
|CREATE|POST|POST를 통해 해당 URI를 요청하면 리소스를 생성|
|READ|GET|GET을 통해 해당 리소스를 조회하며, 조회 후에 해당 도큐먼트에 대한 자세한 정보를 가져옴|
|UPDATE|PUT|PUT을 통해 해당 리소스를 수정|
|DELETE|DELETE|DELETE를 통해 해당 리소스를 삭제|

해당 메소드들을 통해 자원에 대한 행위를 표현하는데 서버에 요청하면 검증 후 유효하면 해당 메소드가 실행된다.

예를 들어 
		
        GET/user/1
        DELETE/user/1

이라고 할 때 이는 GET을 통해 1번 user의 정보를 가져오거나 DELETE를 통해 1번 user의 정보를 삭제하라는 의미가 된다.
하지만 이때 user/1 이라는 대상이 없다면 에러가 발생하고 이는 HTTP 코드를 통해 실행 결과를 알 수 있다.

## URI 설계 가이드
>__URI란? 통합 자원 식별자(Uniform Resource Identifier, URI)__
<br/>

1. 슬래시 구분자(/)를 통해 표현하며 마지막 문자로 슬래시 구분자(/)를 붙이지 않는다
		
        http://restapi.youngvelog.com/cellphones/apple/iphones
         http://restapi.youngvelog.com/cellphones/samsung/galaxys

2. 하이픈(-)은 가독성을 높이는데 사용
3. 밑줄(_)은 사용하지 않는다
	- 밑줄은 보기 어렵거나 다른 글자에 가릴 수 있기 때문에 밑줄 대신 하이픈을 사용한다.
4. URI 경로에는 소문자를 사용한다
	- 대소문자에 따라 다른 리소스로 인식하게 되기 때문에 대문자 사용은 가급적 피하고 RFC3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 한다.
    
5. 파일 확장자는 URI에 포함시키지 않는다
6. 상황에 맞게 리소스 간의 관계를 표현한다
	- 일반적으로는 REST 리소스 간에 계층을 통해 1번의 예시와 같이 사용하며 관계명이 복잡한 경우 서브 리소스에 명시적으로 표현 할 수 있다
    
    
		GET : /users/{userid}/favorite/movies
        
        
        
## HTTP 응답 상태 코드
잘 설계된 REST API는 URI 뿐만 아니라 그 리소스에 대한 응답까지 잘 내어주는 것이 포함도이ㅓ야 한다. 정확한 응답 상태 코드만으로도 많은 정볼르 전달할 수 있기 때문에 응답 상태 코드 값을 명확히 돌려주는 것은 중요하다.

|상태코드| |
|:---:|---|
|200|클라이언트의 요청을 정상적으로 수행함|
|201|클라이언트가 어떠한 리소스 생성을 요청, 해당 리소스가 성공적으로 생성됨(POST)|
|301|클라이언트가 요청한 리소스에 대한 URI가 변경 되었을 때|
|400|클라이언트의 요청이 부적절 할 경우|
|401|클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청했을 때|
|403|유저 인증상태와 관계 없이 응답하고 싶지 않은 리소스를 클라이언트가 요청했을 때|
|405|클라이언트가 요청한 리소스에서는 사용 불가능한 Method를 이용했을 경우 사용하는 응답코드|
|500|서버에 문제가 있을 때|
<br/>

[더 많은 상태 코드 보러가기 : 위키피디아](https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C)

<br/><br/>

출처 : [NHN MeetUp!](https://meetup.toast.com/posts/92)