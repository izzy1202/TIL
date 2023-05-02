# <스프링부트 개념정리 with JPA> 강의 내용 정리
>[강의 링크](https://youtube.com/playlist?list=PL93mKxaRDidG_OIfRQ4nztPQ13y74lCYg)
> 총 14강
> 
>모든 내용을 정리하지는 않음
---

# 1강 - 스프링의 핵심

### 1.1. 스프링은 프레임워크이다.
- Framework : 틀
- 틀을 벗어나지 않고 동작하게끔 해준다.

### 1.2. 스프링은 오픈 소스이다.
- 소스코드가 공개되어 있다.
- 내부를 볼 수 있다 = 뜯어고칠 수 있다.

### 1.3. 스프링은 IoC 컨테이너를 가진다.
- Ioc(Inversion of Controll) : 제어 반전
  - 주도권이 스프링에게 있다.
> 참고
>  - class : 설계도
>  - object : 실체화가 가능한 것
>  - instance : 실체화된 것
>   - 가구는 추상적이므로 object가 아니라 class이다. 
>    - 침대, 의자는 object이고, 실체화되어 나오는 순간 instance가 된다.
- 스프링이 내가 만든 객체를 스캔해서 heap 메모리 공간에 올려주는 것을 Ioc라고 한다.

### 1.4. 스프링은 DI를 지원한다.
- DI(Dependency Injection) : 의존성 주입
- 스프링이 관리하는 객체를 모든 클래스의 메소드에서 가져와서 사용할 수 있는 것을 DI라고 한다.
  - 스프링이 스캔하면 객체가 딱 한번만 메모리에 뜨고(싱글톤) 그 객체를 공유해서 어디서든 사용할 수 있다.
  
# 2강 - 필터
### 2.1. 스프링은 엄청나게 많은 필터를 가지고 있다.
![image](https://user-images.githubusercontent.com/106478906/235582250-522c4b7e-5e06-4db4-9f88-c19b41f84a93.png)
- 필터 : 문지기(권한 없으면 걸러내는 임무)
  - 스프링 자체 필터 / 사용되지 않고 있는 필터를 사용하겠다고 설정 / 직접 필터 생성
- 성 = 톰캣
  - 톰캣의 필터 : web.xml
- 왕의 집 = 스프링 컨테이너
  - 스프링 컨테이너의 필터 : 인터셉터(AOP)
  
### 2.2. 스프링은 엄청나게 많은 어노테이션을 가지고 있다.
> 주석 : 컴파일러가 무시
>
> 어노테이션 : 주석 + 힌트 - 컴파일러가 무시하지 않음
>
> @component : 클래스 메모리에 로딩
>
> @Autowired : 로딩된 객체를 해당 변수에 집어 넣어라

- 스프링에서 어노테이션은 객체를 생성한다.
- 리플렉션 : 한 클래스가 어떤 메소드,필드,어노테이션을 갖고 있는지 분석하는 기법으로, 런타임시 분석한다.

# 3강 - MessageConverter
### 3.1. 스프링은 MessageConverter를 가지고 있다. 기본값은 현재 Json이다.
- Json : 중간 언어
- MessageConverter : JAVA 프로그램에서 파이썬 프로그램에 object를 request할 때 파이썬이 바로 이해하기 힘드니까 JSON이라는 중간 언어로 변환하는 과정을 거치는데 MessageConverter가 그 역할을 한다.

### 3.2. 스프링은 BufferedReader와 BufferedWriter를 쉽게 사용할 수 있다.
> 자바에서는 문자를 InputStream으로 읽어오는데, 이건 Byte로 받아온다.
> 
> InputStreamReader : 바이트를 문자로 바꿔주는데 배열로도 바꿀 수 있다. 그런데 이 경우 작은 데이터를 보내면 용량이 계속 낭비되므로 쓰지 않는다.

- > 가변 길이의 데이터를 받아올 수 있는 BufferReader를 사용한다.
- 스프링에서는 BufferedReader와 BufferedWriter를 어노테이션을 통해 사용할 수 있다.
  - @ResponseBody : BufferedWriter
  - @RequestBody : BufferedReader
 
### 3.3. 스프링은 계속 발전중이다.