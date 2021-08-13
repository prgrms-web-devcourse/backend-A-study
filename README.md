# 백엔드 A팀 스터디

---

</br>

## 📔 스터디 소개
---


### 📌 JAVA 스터디

Java8 버전 주요 업데이트 기능을 학습하며 자바에 대해 공부한다.


|주차|제목|링크|회의록|
|---|---|---|---|
|1주차|동작 파라미터화 코드 전달하기|[유현호](https://www.notion.so/aeno/0ab365ce7f0248b49de7b0eb7882430a) [이주오](https://velog.io/@ljo_0920/%EB%8F%99%EC%9E%91-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0%ED%99%94) [허승연]([링크](https://velog.io/@heoseungyeon/%EB%8F%99%EC%9E%91-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0%ED%99%94-%EC%BD%94%EB%93%9C-%EC%A0%84%EB%8B%AC%ED%95%98%EA%B8%B0))|[링크](./java/week-1/meeting-log-1.md)
| |람다 표현식|[유현호](https://www.notion.so/aeno/f8291bec1d564b35be976bac4cbd3efc) [이주오](https://velog.io/@ljo_0920/%EB%9E%8C%EB%8B%A4-%ED%91%9C%ED%98%84%EC%8B%9D) [허승연]([링크](https://velog.io/@heoseungyeon/%EB%9E%8C%EB%8B%A4-%ED%91%9C%ED%98%84%EC%8B%9D))|[링크](./java/week-1/meeting-log-2.md)


</br>

### 📌 CS 스터디

|주차|제목|링크|
|---|---|---|
|1주차|HTTP 차이점|v|
|1주차|OSI 7계층|v|
|1주차|GET / POST의 차이점|v|

</br>

## 🗓 기간
---
20201.08.04 ~ 2021.08.31

</br>

## 🧩 진행 방식
---
기술 공유와 팀 전체의 스킬 향상을 위해 발표 시간 참석 가능한 모든 팀원들이 참여하여 발표를 듣고 피드백을 진행한다.
매주 발표가 끝난 뒤 질문 내용 정리 및 간단한 회고록을 작성한다.

</br>

## 📌 JAVA 스터디 & 회의록 작성법
---
### 스터디 방법
- 매주 월요일 팀 스크럼 시간이 끝나고 발표를 진행한다.
- 가능한 모두가 발표를 한다.
- 질문이 없거나 리뷰가 끝나면 자신의 올린 pr 머지하기
- 발표 끝난 후 피드백 및 질문 후 회의록 pr 작성

</br>

## 📌 CS 스터디
---
매주 월요일 팀 스크럼 시간이 끝나고 발표를 진행한다. 매주 각자 주제를 정하여 발표한다.


</br>

## 📜 제출 방법
---

### 💫 과제 pr 작성법
```
1. 원본 레포지토리 fork 하기
2. clone 하기
3. java/week-숫자 디렉터리에 자신의 깃닉네임.md 파일에 스터디 내용 작성(url or 내용은 자유롭게)
    - ex) yhh1056.md
4. [#숫자/깃닉네임] 브랜치으로 브랜치를 생성하고 원본 레포지토리 main 브랜치로 PR를 보낸다.
    - ex) #1(주차수)/yhh1056 -> main

```
</br>

### 🦧 회의록 pr 작성법
- 스터디가 끝난 후 회의록 작성 pr에 본인이 했던 질문 기입 후 commit push
- 질문을 받은 사람은 해당 답변했던 내용을 작성 후 해당 pr에 commit push
- 느낀점이나 새롭게 느낀점 또한 자유롭게 적어도 좋을 것 같습니다.


</br>


## 💥 팀원들이 올린 pr에 커밋 추가하기(참고)
---
### 1. 깃허브 pr에서 직접 수정(edit file) 하거나
### 2. 내 로컬에서 작업하기
```
1. git clone https://github.com/prgrms-web-devcourse/backend-A-study.git (선택 - 폴더명)
    - git clone https://github.com/prgrms-web-devcourse/backend-A-study.git upstream-stduy
2. git remote add <원하는 이름> <Pr 작성한 사람의 repo 주소>
    - git remote add yhh https://github.com/yhh1056/backend-A-study.git
    - git remote -v 로 확인
3. git fetch <이름>
    - git fetch yhh
4. git checkout -t <이름>/<pr 브랜치>
    - git checkout -t yhh/yhh1056
5. 수정 후 commit하고 push
```
- [참고 링크](https://tighten.co/blog/adding-commits-to-a-pull-request/)



