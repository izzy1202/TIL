# <초보 백엔드 개발자 로드맵> 강의 내용 정리
>[강의 링크](https://www.inflearn.com/course/%EC%B4%88%EB%B3%B4-%EB%B0%B1%EC%97%94%EB%93%9C-%EA%B0%9C%EB%B0%9C%EC%9E%90-%EB%A1%9C%EB%93%9C%EB%A7%B5/dashboard)
>
>모든 내용을 정리하지는 않음

---

![image](https://user-images.githubusercontent.com/106478906/231113329-84a927b2-e022-400a-925d-c29a16543252.png)

## 1. 인터넷과 HTTP
- 네트워크 : '네트' + '워크'
  - 여러 대의 컴퓨터가 서로 통신할 수 있게 해주는 것
- 인터넷 : 네트워크들의 집합체(네트워크의 네트워크)

### 인터넷 작동 원리
[강의 소개 링크 - 인터넷은 어떻게 동작하는가?](https://developer.mozilla.org/ko/docs/Learn/Common_questions/Web_mechanics/How_does_the_Internet_work)
  - 여러 대의 컴퓨터를 연결하기 위해 '라우터'라는 것을 사용한다.
  - 라우터끼리도 연결함으로써 네트워크를 확장시킬 수 있다.
  - 네트워크를 전화 시설과 연결하기 위해 모뎀이 필요하다.
  - ISP(Internet Service Provider) : 인터넷을 제공하는 업체
  - 네트워크에 연결된 모든 컴퓨터에는 IP 주소 (IP는 (Internet Protocol)라는 고유한 주소가 있다. 주소는 점으로 구분 된 네 개의 숫자로 구성된 주소이다 . 예: 192.168.2.10.
    - DNS(도메인) : 사람이 알아보기 쉽게 알파벳이나 한글 등으로 변경한 것
    
### 웹소켓 
- 웹소켓은 데이터를 HTTP로 주고 받는데, HTTP는 클라이언트가 서버에 요청을 해야지만 응답을 줄 수 있다.
    - 웹소켓은 이런 단점을 보강하기 위한 프로토콜로써 HTTP위에서 생성되었다.
    
 ![image](https://user-images.githubusercontent.com/106478906/231121337-f3840129-b553-4221-9d81-1e8b2233389a.png)

 - 실시간 통신이 필요한 채팅, 주식 등에서 사용
 - ex) 업비트
    
## 2. 버전 컨트롤
- Git
  - 분산형 버전 관리 시스템
  - 3가지 영역
    1. 작업 디렉토리(워킹 디렉토리)
    2. 스테이지 에어리어 : commit 하기위해 git add명령어로 추가하면 올라가는 영역
    3. 레포지토리 : git commit하면 올라가는 영역
      - commit 후 push까지 하면 원격 서버에 commit 파일들을 업로드하게 된다.
- GitHub
  - Git 기반의 호스팅 사이트
  - Git에서 git push로 파일을 올린 원격 서버가 Github
  - Pull requests : 관리자가 아닌 사람이 코드의 변경 요청을 할 때 사용하는 메뉴
  - Actions : 코드 저장소에 어떤 이벤트가 일어날 때 특정 작업이 일어나게 하거나, 주기적으로 어떤 작업들을 반복시켜서 실행하고 싶은 경우에 사용한다.
  - Projects : 프로젝트 관리하는 메뉴
  - Wiki : 해당 프로젝트의 위키 문서들을 저장할 수 있는 공간
  - insights : 이 저장소가 어떤 식으로 운영 되고 있는지 통계 수치를 보여준다.
 

## 3. 개발 언어
  - 크게 3가지만 소개
  1) JAVA
    - 정적 타입 언어
    - 클래스가 있다.
    - JVM위에서 돌아간다.
  2) Javascript / Typescript
    - Javascript는 웹 기반 언어였지만, 지금은 Node js로 작성하면 서버에서도 작동한다.  
    - Typescript를 쓰면 타입도 있기 때문에 파워풀한 언어다.
  3) Python
 
 - 개발 언어는 하나는 꼭 마스터해야 한다.
  
 ## 4. 데이터 표현법 (JSON, YAML)
 1) [JSON(JavaScript Object Notation)](https://terms.naver.com/entry.naver?docId=5714735&cid=42346&categoryId=42346)
  - 자바스크립트 오브젝트 표현법에서 온 데이터 표현법이다.
  - 문법 - [ JSON.org](https://www.json.org/json-en.html)
  - 주석을 넣을 수 없다.

 2) YAML
 - 문법 - [Learn X in Y minutes](https://learnxinyminutes.com/docs/yaml/)
 - 주석을 넣을 수 있다.
 
 ## 5. 리눅스 명령어
- pwd(print working directory) : 현재 작업 위치를 출력하는 명령어
- ls(list Segment) : 현재 디렉토리의 파일과 디렉토리를 보여준다.
- cd(change directory) : 디렉토리 이동
- mkdir : make directory
- cp : copy
- mv : move directory
- rm : remove directory
- cat : 파일의 내용 확인
- touch : 빈 파일 생성
- echo : 화면에 글자 표시
- ip addr / ifconfig: 아이피 정보 확인
- ss : 네트워크 상태 확인
- nc(net cat) : 서버의 포트 확인
- which : 어떤 명령어가 어디에 있는지 찾을 때 사용
- tail : 파일의 마지막 부분을 보여주는 명령어
- find : 파일이나 디렉토리 찾는 명령어
- ps : 프로세스 상태를 보여준다
  - ps -aux
- grep : 어떤 파일에서 패턴을 찾아서 파일의 내부에 패턴을 만족하는 문자열이 있는지 확인한다.
- kill : 프로세스를 죽이는 명령어
  - ps -aux해서 두번째줄의 프로세스 아이디로 죽일수 있다.

## 6. 웹서버
- 웹서버 : 애플리케이션 서버 중간에 위치한 서버












    
    
    
    
