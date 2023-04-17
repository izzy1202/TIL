# :bread: 빵 부스러기

>개발 관련 학습 중 하나의 글로 작성하기엔 짧고,  
버리기엔 아까운 부스러기 정보들을 모아두는 곳.
-----
## 목차
1. 스냅샷
2. Spring에서 GroupId, ArtifactId




---

## 1. 스냅샷
스프링 부트를 다운받던 중, 버전에 (SNAPSHOT)이 붙어있는 것이 무슨 의미인지 궁금해져서 찾아본 내용 정리

Snapshot이란 특정 시점에 스토리지에 저장된 파일의 상태(현재 파일 시스템의 상태)를 저장한다는 의미이다.   
Spring Boot에서 애플리케이션 생성 시, 개발이 완료된 최종 버전이 아니라 각 진행 단계별로 개발을 하고 빌드를 할 때  
해당 애플리케이션의 현재 상태가 완료 버전이 아닌 중간 단계의 버전이라는 의미로 사용된다. 

- Reference - [Snapshot 은 어떤 의미인가요?](https://www.inflearn.com/questions/268685/snapshot-%EC%9D%80-%EC%96%B4%EB%96%A4-%EC%9D%98%EB%AF%B8%EC%9D%B8%EA%B0%80%EC%9A%94)

## 2. Spring에서 GroupId, ArtifactId

### GroupId
- GroupId는 프로젝트를 정의하는 고유한 식별자 정보이다. 
- GroupId는 Java package name rules을 따라야 한다.

### ArtifactId
- 버전 없는 Jar파일 이름
- 특수문자는 사용할 수 없고, 소문자만 사용되어야 한다.

정리하자면, GroupId는 큰 틀을 의미하고, ArtifactId는 그 안에 작은 틀을 의미한다.  
예를 들어 회사에서 정산시스템을 만든다면, GroupId는 회사명, ArtifactId는 주문정산, 월급정산 등 이런식으로 정의할 수 있다.

- Reference - [[Spring]Group, Artifact이란?](https://developer-han.tistory.com/4)
