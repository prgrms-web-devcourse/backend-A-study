### 정리글
---
|주차|제목|링크|
|---|---|---|
|2주차|스트림 소개|[링크](https://velog.io/@ljo_0920/%EC%8A%A4%ED%8A%B8%EB%A6%BC-%EC%86%8C%EA%B0%9C)|
| |스트림 활용|[링크](https://velog.io/@ljo_0920/%EB%AA%A8%EB%8D%98-%EC%9E%90%EB%B0%94-%EC%9D%B8-%EC%95%A1%EC%85%98-%EC%8A%A4%ED%8A%B8%EB%A6%BC-%ED%99%9C%EC%9A%A9)|

</br>

### 궁금증 및 회고록
---
아직 멀었지만 저번주 보다는 확실히 조금씩 람다와 스트림에 익숙해지는 것 같다. 특히 람다와 스트림을 통해 정말 코드가 간결해지는 것
같아 재미있고 좀 더 능숙하게 활용하고 싶다. 예제같은 실습을 좀 더 보완하고 싶고 병렬성에 관해 언급을 많이 했는데 다음 챕터를 통해 파악하고 싶다.
특히 flatMap을 이해하는데 조금 시간이 걸려 이쪽에 대한 부분과 distinct쪽도 좀 살펴보고 싶다.

</br>

(추가) Optional의 메서드들도 스트림 최종 연산인지 갑자기 헷갈렸다
- 답 : 당연히 아니다! 스트림 연산이란 java.util.stream.Stream 인터페이스에 정의되어 있는 메서드들이고 만약 최종 연산이라고 가정하면 아래 코드는 에러가 발생해야 한다.
```
Stream.of("Hong", "Hwang", "Park").filter(s -> s.startsWith("H")).findAny().ifPresent(System.out::println);
```

</br>

(추가) 승연님의 stream이 항상 퍼포먼스가 좋은 건 아닌 것 같고 사용하는 경우를 잘 생각해야 할 것 같다는 말씀을 해주었다.
- forEach는 최종연산 중 기능이 가장 적고 덜 스트림스럽기 때문에 스트림 계산 결과를 print할 때만 사용하고 계산하는데는 쓰지 않는 것이 좋다고 한다.
- 특히 모든 for-loop를 forEach로 변환하는 것은 좋지 않다.
- 즉 forEach에 로직이 들어간다면 forEach 내부가 아닌 stream 연산을 사용하거나 반복문 혹은 forEach말고 다른 최종연산을 사용하는 것이 좋다고 한다.

</br>

[참고출처](https://woowacourse.github.io/tecoble/post/2020-05-14-foreach-vs-forloop/)