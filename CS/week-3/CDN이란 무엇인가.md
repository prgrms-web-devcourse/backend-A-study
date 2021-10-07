[원문 링크 가기](https://velog.io/@youngblue/CDN%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)

# CDN

---

## CDN이란 무엇인가?
![](https://images.velog.io/images/youngblue/post/f29d7267-0498-4319-b72d-f17b7944b243/99CE4C415BF2B5FB18.png)
데이터 통신 기술이 발달하면서 전 세계적으로 유튜브, 넷플릭스 등 수 많은 데이터들이 전송되는 세상에 살고 있다. 이렇게 폭발적으로 증가하는 데이터를 최대한 지연 없이 효율적으로 전달하기 위해 CDN이라는 기술이 등장하게 된다.
__CDN은 Content Delivery Network의 약자로서 지리적인 제약 없이 전 세계 사용자에게 빠르고 안전하게 컨텐츠 전송을 할 수 있는 기술을 말한다. 이를 통해서 컨텐츠의 병목현상을 피할 수 있다.__

<br/>

## CDN의 원리
CDN(Content Delivery Network)은 물리적으로 떨어져 있는 사용자에게 컨텐츠를 더 빠르게 제공하기 위해 고안된 기술이다. 만약 우리나라에 있는 사람이 미국에 있는 서버로부터 이미지나 파일 등을 다운받으려고 한다면 시간이 오래 걸릴 것이다. 
__따라서 서버를 분산시켜 캐싱해두고 사용자의 컨텐츠 요청이 들어오면 사용자와 가장 가까운 위치에 존재하는 서버로 매핑시켜 요청된 콘텐츠의 캐싱된 내용을 내어주는 방식으로 빠르게 데이터를 전송할 수 있게 된다. __
만약 서버가 파일을 찾는데 실패하는 경우 CDN 플랫폼의 다른 서버에서 컨텐츠를 찾은다음 응답을 전송한다.




![](https://images.velog.io/images/youngblue/post/3f7b945b-bf84-4f3f-9007-aa9c2f85c7ea/cdn.png)
- 왼쪽 : CDN을 사용하지 않을 경우
- 오른쪽 : CDN을 사용할 경우


이때 CDN의 동작을 살펴보면 다음과 같은 규칙으로 수행된다.

1. 최초 요청은 서버로부터 컨텐츠를 가져와 고객에게 전송하며 동시에 CDN 캐싱장비에 저장한다.
2. 최초 요청 이후로의 요청은 CDN 에서 지정하는 해당 컨텐츠 만료 시점까지 캐싱된 컨텐츠를 전송한다.
3. 자주 사용하는 페이지에 한해서 캐싱되며, 해당 컨텐츠 호출이 없을 경우 주기적으로 삭제된다.
4. 서버가 파일을 찾는데 실패하는 경우 CDN 플랫폼의 다른 서버에서 컨텐츠를 찾은다음 엔드유저에게 응답을 전송한다.
5. 컨텐츠를 사용할 수 없거나 오래된 경우 CDN은 향후 요청에 대해 응답할 수 있도록 새로운 컨텐츠를 저장한다.

<br/>

## CDN 캐싱 방식

### Static Caching
- Origin Server 에 있는 Content를 운영자가 미리 Cache Server에 복사 해두어 사용자가 Cache Server에 Content 요청 시 무조건 Cache Server에 있다
- 대부분의 국내 CDN에서 이 방식을 사용 (게임 클라이언트 다운로드 등)


### Dynamic Caching
- Origin Server에 있는 Content를 운영자가 미리 Cache Server에 복사하지 않음
- 사용자가 Content를 요청 시 해당 Content가 없는 경우 Origin Server로부터 다운로드 받아 전달한다. 있는 경우에는 캐싱된 Content전달
- 각각의 Content는 일정 시간 이후 Cache Server에서 삭제 될 수도 있다.

<br/>

## 활용 사례
- 온라인 게임의 오픈 베타테스트나 정식서비스 시작시점에 클라이언트의 다운로드 수요가 급격하게 증가한다 이럴 경우 병목 현상이 일어나거나 심한 경우 서버가 다운 되기도 하기 때문에 CDN이 필수적으로 사용된다. 또한 대규모 업데이트를 위한 패치가 있을 경우에도 병목 현상을 막기 위해 CDN을 사용한다
- 넷플릭스(Netflix)에서는 온라인 동영상 스트리밍 서비스를 전세계로 제공하는 업체로서 최대한 지연 없이 안정적이고 빠르게 컨텐츠를 제공하기 위해서는 CDN 기술이 필수적이다.

<br/><br/>

---


[출처 : 가비아 라이브러리](https://library.gabia.com/contents/infrahosting/8985/)
[출처 : 티스토리 망나니개발자](https://mangkyu.tistory.com/95)
[출처 : 티스토리 갓대희](https://goddaehee.tistory.com/173)
[출처 : 티스토리 홍구](https://hongku.tistory.com/320)
[참고 : 유튜브 얄팍한 코딩사전 - 웹서비스에 필수! CDN이 뭔가요?](https://www.youtube.com/watch?v=_kcoeK0ITkQ)
