### 정리글
---
|주차|제목|링크|
|---|---|---|
|3주차|스트림으로 데이터 수집|[링크](https://velog.io/@heoseungyeon/%EC%8A%A4%ED%8A%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%88%98%EC%A7%91)|
| |병렬 데이터 처리와 성능|[링크](https://velog.io/@heoseungyeon/%EB%B3%91%EB%A0%AC-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%B2%98%EB%A6%AC%EC%99%80-%EC%84%B1%EB%8A%A5)|

### 궁금증 및 회고록
---
Collect() 메서드에서 groupby, partition 의 기능을 SQL에서 하면 안되는 건가? 라는 의문이 계속 들었던 것 같습니다. 
또 Java10 버전의 UnmodifiableTo"Collection Type" 메서드의 unmodifiable 특성과 immutable 특성에 대해서 논쟁이 많던데 
이 점도 확실하게 짚고 사용해봐야될 것 같습니다.

Parallel 연산에 대해서 당연히 Parallel하게(병렬적으로) 하는 것이 성능이 좋은 거 아니야? 라고 생각했었던 내게 꿀밤을 놔준 학습이었던 것 같습니다. 🤨
개인적으로 느꼈던 점은 그냥 데이터가 많지 않을 땐 지양하자..
그리고 굳이 사용해본다하면 꼭 실행 속도 테스트를 하고 사용해보자.. 등 이었던 것 같습니다. 그래도 당연시 여겼던 개념에 대한 비판적인?! 고찰을 하게되어 좋았던 것 같습니다 ☺️

