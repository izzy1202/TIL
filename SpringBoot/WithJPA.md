# <스프링부트 개념정리 with JPA> 강의 내용 정리
>[강의 링크](https://youtube.com/playlist?list=PL93mKxaRDidG_OIfRQ4nztPQ13y74lCYg)
>
>[강의 내용 블로그](https://getinthere.tistory.com/category/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8%20with%20JPA%20%EA%B0%9C%EB%85%90)
>
> 총 14강
> 
>모든 내용을 정리하지는 않음
---
> # 스프링
# 1강
## 스프링의 핵심

### 1. 스프링은 프레임워크이다.
- Framework : 틀
- 틀을 벗어나지 않고 동작하게끔 해준다.

### 2. 스프링은 오픈 소스이다.
- 소스코드가 공개되어 있다.
- 내부를 볼 수 있다 = 뜯어고칠 수 있다.

### 3. 스프링은 IoC 컨테이너를 가진다.
- Ioc(Inversion of Controll) : 제어 반전
  - 주도권이 스프링에게 있다.
> 참고
>  - class : 설계도
>  - object : 실체화가 가능한 것
>  - instance : 실체화된 것
>   - 가구는 추상적이므로 object가 아니라 class이다. 
>    - 침대, 의자는 object이고, 실체화되어 나오는 순간 instance가 된다.
- 스프링이 내가 만든 객체를 스캔해서 heap 메모리 공간에 올려주는 것을 Ioc라고 한다.

### 4. 스프링은 DI를 지원한다.
- DI(Dependency Injection) : 의존성 주입
- 스프링이 관리하는 객체를 모든 클래스의 메소드에서 가져와서 사용할 수 있는 것을 DI라고 한다.
  - 스프링이 스캔하면 객체가 딱 한번만 메모리에 뜨고(싱글톤) 그 객체를 공유해서 어디서든 사용할 수 있다.
  
# 2강
## 필터
### 5. 스프링은 엄청나게 많은 필터를 가지고 있다.
![image](https://user-images.githubusercontent.com/106478906/235582250-522c4b7e-5e06-4db4-9f88-c19b41f84a93.png)
- 필터 : 문지기(권한 없으면 걸러내는 임무)
  - 스프링 자체 필터 / 사용되지 않고 있는 필터를 사용하겠다고 설정 / 직접 필터 생성
- 성 = 톰캣
  - 톰캣의 필터 : web.xml
- 왕의 집 = 스프링 컨테이너
  - 스프링 컨테이너의 필터 : 인터셉터(AOP)
  
### 6. 스프링은 엄청나게 많은 어노테이션을 가지고 있다.
> 주석 : 컴파일러가 무시
>
> 어노테이션 : 주석 + 힌트 - 컴파일러가 무시하지 않음
>
> @component : 클래스 메모리에 로딩
>
> @Autowired : 로딩된 객체를 해당 변수에 집어 넣어라

- 스프링에서 어노테이션은 객체를 생성한다.
- 리플렉션 : 한 클래스가 어떤 메소드,필드,어노테이션을 갖고 있는지 분석하는 기법으로, 런타임시 분석한다.

# 3강
## MessageConverter
### 7. 스프링은 MessageConverter를 가지고 있다. 기본값은 현재 Json이다.
- Json : 중간 언어
- MessageConverter : JAVA 프로그램에서 파이썬 프로그램에 object를 request할 때 파이썬이 바로 이해하기 힘드니까 JSON이라는 중간 언어로 변환하는 과정을 거치는데 MessageConverter가 그 역할을 한다.

### 8. 스프링은 BufferedReader와 BufferedWriter를 쉽게 사용할 수 있다.
> 자바에서는 문자를 InputStream으로 읽어오는데, 이건 Byte로 받아온다.
> 
> InputStreamReader : 바이트를 문자로 바꿔주는데 배열로도 바꿀 수 있다. 그런데 이 경우 작은 데이터를 보내면 용량이 계속 낭비되므로 쓰지 않는다.

- > 가변 길이의 데이터를 받아올 수 있는 BufferReader를 사용한다.
- 스프링에서는 BufferedReader와 BufferedWriter를 어노테이션을 통해 사용할 수 있다.
  - @ResponseBody : BufferedWriter
  - @RequestBody : BufferedReader
 
### 9. 스프링은 계속 발전중이다.

&nbsp;
> # JPA

# 4강
## JPA
- JPA(Java Persistence API) : JAVA의 데이터를 영구히 기록할 수 있는 환경을 제공하는 API
  - API(Application Programming Interface) : 프로그램으로 프로그래밍하게 해주는 인터페이스
    - Interface : 상하관계가 존재하는 약속 ex) a 데이터를 사용하려면 12시 ~ 6시까지만 사용해라
    - 프로토콜 : 동등한 약속 ex) 이메일로 연락하자

# 5강
### 1. JPA는 ORM 기술이다.
- ORM(Object Relational Mapping)

![image](https://user-images.githubusercontent.com/106478906/235809241-e769c87f-4c38-4dd6-9960-3eb14b58ab48.png)
- 원래 DB에서 테이블을 만들고 그 데이터를 자바에서 모델링 하는 순서인데
![image](https://user-images.githubusercontent.com/106478906/235809431-4dc20284-a59f-4452-b290-1737074267f6.png)
- ORM을 통해 자바에서 모델링을 먼저 하면 DB에서 테이블이 자동 생성된다.
  - 이때 JPA의 인터페이스를 잘 지키는 것이 필요하다.

### 2. JPA는 반복적인 CRUD 작업을 생략하게 해준다.
- JPA의 함수가 자동으로 해준다.

# 6강
### 3. JPA는 영속성 컨테이너를 가지고 있다.
- 영속성 : 데이터를 영구적으로 저장
- 컨텍스트 : 대상에 대한 모든 정보

![image](https://user-images.githubusercontent.com/106478906/235812359-20d4c509-22da-4429-83cb-f107ac04e651.png)

![image](https://user-images.githubusercontent.com/106478906/235812643-5d01bb0c-ab63-47c6-9398-2d3420f1d8e8.png)
> 자바가 DB에 저장해야 하는 모든 데이터의 정보를 영속성 컨텍스트가 가지고 있다.
- 자바는 영속성 컨테이너를 통해 DB에 정보 저장하고 DB도 영속성 컨테이너를 통해 자바에 정보 전달  

### 4. JPA는 DB와 OOP의 불일치성을 해결하기 위한 방법론을 제공한다.(DB는 객체저장 불가능)
![image](https://user-images.githubusercontent.com/106478906/235813393-f32583a4-ee97-4c73-94e5-148d8fe7ba25.png)
> ORM을 통해 자바가 주도권을 쥐고 있게 된다.

# 7강
### 5. JPA는 OOP의 관점에서 모델링을 할 수 있게 해준다.(상속, 콤포지션, 연관관계)
- 콤포지션 : 결합
![image](https://user-images.githubusercontent.com/106478906/235814170-e843b1fc-b490-4f77-a232-f74d29147ed0.png)

### 6. 방언(dialect) 처리가 용이하여 Migration하기 좋고 유지보수에도 좋다.
![image](https://user-images.githubusercontent.com/106478906/235814696-5e506652-77df-4482-a2e4-443d8e01605e.png)

- 다른 db를 사용하고 싶다면 추상화 객체가 다른 db로 변경된다.

&nbsp;
> # 스프링부트 동작원리
# 8강
### 1. 내장 톰캣을 가진다.
- 톰캣을 따로 설치할 필요 없이 바로 실행 가능하다.

> 소켓 : A와 B가 통신하기 위해서 사용하는 것으로 운영체제가 가지고 있다.
- A가 5000번 소켓을 오픈하고 B랑 연결되면 C랑은 연결을 못하게 되므로, 5000번 소켓은 연결의 용도로만 사용한다.
- 5000번 소켓에 연결되는 순간 새로운 소켓이 열리고 5000번 소켓과는 연결이 끊긴다.
- 5001번 소켓에 B가 연결되고 A와 대화하게 되면 다른 사용자가 5000번 소켓을 쓸 수 없게된다.
- 그래서 5000번 소켓이 메인 스레드가 되고 5001번 소켓이 스레드1이 된다
- C가 메인 스레드에 연결하면 5002번 소켓인 스레드2에 연결된다.

> 소켓 통신 - time slice해서 동시 동작
- 단점 : 연결이 지속되기 때문에 부하가 크다.

> HTTP 통신 - Stateless 방식
- html 문서를 전달하는 통신
- 팀버너스리
- 장점 : 연결이 끊기기 때문에 부하가 적다.
- 단점 : 재요청해도 같은 요청인임을 인식하지 못한다.

# 9강
#### 1.1. 톰캣

> HTTP 통신
- 갑 : (웹서버)
- 을이 갑에게 요청(request)
  - ip주소, url 필요
- 갑이 을에게 응답(response)
  - ip주소 알 필요 없음
- static(정적인) 자원 응답

> 톰캣

![image](https://user-images.githubusercontent.com/106478906/236217590-4a8dda1b-b99f-48b4-89d9-0c9827ea68f2.png)

- 아파치 : 웹서버. 요청한 파일을 응답해준다.
  - 아파치가 자기가 이해하지 못하는 JSP에 대한 요청이 오면 톰캣에게 넘긴다.
  - 톰캣이 JSP 파일의 모든 자바 코드를 컴파일 후 html 문서로 만들어서 아파치에 반환한다.
  - 아파치가 html 파일을 요청한 곳에 응답한다.
- 웹브라우저는 html, javascript, css 같은 정적 파일만 이해할 수 있고, jsp 파일을 이해할 수 없다.

# 10강
### 2. 서블릿 객체의 생명주기
![image](https://user-images.githubusercontent.com/106478906/236223467-685aa018-9571-4c29-931f-4214f6cda61c.png)
- 서블릿 컨테이너 : 톰캣

> [URL과 URI](https://www.charlezz.com/?p=44767)
- URL : 자원에 접근(Location)
  - ex) http://naver.com/a.png
- URI : 식별자 접근(Identifier)
  - ex) http://naver.com/picture/a
  - 특정한 파일 요청을 할 수 없다. 요청시에는 무조건 자바를 거쳐야 해서 아파치가 톰캣에 주도권을 넘긴다.

![image](https://user-images.githubusercontent.com/106478906/236362507-fc3a4ce5-1b1d-4d67-abcf-2f8417461cab.png)
- 클라이언트가 자바 관련 요청을 하면 서블릿 컨테이너
  - 서블릿 : 자바 코드로 웹을 할 수 있는 것
  - 서블릿 컨테이너 : 서블릿을 모아서 컨테이너로 만든 것
- 최초의 요청을 받았을 때 스레드를 생성해서 스레드가 서블릿 객체를 만든다.
  - 스레드 : 많은 요청에 대한 동시 처리를 위해서
- 20개의 스레드만 만들어지게 정해놨다고 하면, 21번째 요청이 오면 기다리고 있다.
  - 첫 번째 스레드가 일을 다하고 response를 해주면 할 일이 끝났다.(HTTP 통신은 연결이 지속되는 게 아니라 한번 응답하면 끝이기 때문)
  - 21번째 요청을 첫 번째 스레드를 재사용해서 응답하게 된다.
    -> 속도가 빨라진다.
  
# 11강
## 3. web.xml
> 웹서버에 진입하면 최초에 실행된다.

### 3.1. ServletContext의 초기 파라미터
- 초기 파라미터 : 암구호
  - ex) 문지기가 성에 들어오는 a에게 암구호를 알려주고 누가 암구호 뭐냐고 물어보면 a가 그 암구호를 말하고 그 암구호를 모르는 b는 대답 못한다.

### 3.2. Session의 유효시간 설정
- Session : 인증을 통해 들어오게 해주는 것
  - ex) 문지기가 a가 성에 3일간 있을 수 있는 session을 발급해주고 더 있고 싶다고 하면 다시 session을 발급받는다.

### 3.3. Servlet/JSP에 대한 정의 및 매핑
- 매핑 : a가 요청한 자원이 어디있다는 것을 알려주고 이동할 수 있게 도와주는 것

### 3.4. Mime Type 매핑
- Mime Type : a가 들고올 데이터의 타입을 알려준다.
  - 아무것도 안들고 오는 애들 : get 방식(뭔가 주려고 온게 아니라 가지러 온 것 - select)
  - a가 들고온 데이터를 타입에 맞게 가공한다.
  - Mime Type이 틀리게 되면 에러 발생
  - 추가적인 공부 필요하다.
  
### 3.5. Welcome File list
- Welcome File list : 아무것도 안 달고 온 a를 한 곳으로 보내는 것이다. 
- 설정하기 나름이다.

### 3.6. Error Pages 처리
- Error Page : 이상한 애들이 들어오면(없는 타입을 달고 들어왔다던지) 보내는 곳이다.

### 3.7. 리스너/필터 설정
- 리스너 : 대리인, 관리자가 시킨 것에 맞는 것만 따로 데려가는 것
- 필터 : 문지기가 거르는 것

### 3.8 보안
- 이상한 애들 들어오면 쫓아낸다.

> 여기에서 Servlet/JSP 매핑시(web.xml에 직접 매핑 or @WebServlet 어노테이션 사용)에 모든 클래스에 매핑을 적용시키기에는 코드가 너무 복잡해지기 때문에 Front Controller패턴을 이용한다.

# 12강
## 4. Front Controller 패턴
> 최초 앞단에서 request 요청을 받아서 필요한 클래스에 넘겨준다.
- web.xml에 다 정의하기 힘들기 때문이다.
- 이때 새로운 요청이 생기기 때문에 request와 response가 새롭게 new될 수 있다. 그래서 아래의 RequestDispatcher가 필요하다.

![image](https://user-images.githubusercontent.com/106478906/236378682-6a922937-481c-40eb-a287-b02409f41496.png)

- 특정 주소(ex. .do)로 request가 오면 Front Controller로 보내라는 코드를 web.xml에 써놓는다.
  - Front Controller가 내부에서 자원을 request한다.
  - response가 요청자에게 가는게 아니라 Front Controller에게 간다.
  - 최초의 request / response가 사라지는 게 아니라 그 위에 덮어 씌워진다.
  -> RequestDispatcher

## 5. RequestDispatcher 
> 필요한 클래스 요청이 도달했을 때 FrontController에 도착한 request와 response를 그대로 유지시켜준다.

![image](https://user-images.githubusercontent.com/106478906/236377905-36017aa9-a70f-48ac-a386-fadf80238928.png)
- 요청이 URI 또는 자바파일일때 자원에 직접 접근 못하고 톰캣에 넘기는데 톰캣이 request객체와 response객체를 만들어준다.
- A라는 사람이 a.jsp를 요청하면 a.html을 응답해준다.
  - a.html에 대한 요청과 응답이 만들어진다.
- a.html에서 새로운 버튼을 클릭했을 때 b.jsp로 새로 요청이 들어오고, b.html을 응답한다.
- RequestDispatcher를 이용하면 기존의 request를 재사용하기 때문에 a.html의 request를 b.html에 이어서 가져갈 수 있다.

## 6. DispatchServlet
> 스프링에는 DispatchServlet이 있기 때문에 Front Controller 패턴을 직접 짜거나 RequestDispatcher를 직접 구현할 필요가 없다.
>
> Front Controller 패턴 + RequestDispatcher
- DispatchServlet이 자동 생성되어질 때 수많은 객체가 생성(IoC)된다. 보통 필터들이다. 해당 필터들은 내가 직접 등록할 수도 있고 기본적으로 필요한 필터들을 자동 등록된다.
- 컴포넌트 스캔 후 주소 분배

# 13강
## 7. 스프링 컨테이너
### 7.1. ApplicationContext

> DispatcherServlet에 의해 생성되어지는 수 많은 객체들은 ApplicationContext에서 관리된다. 이것을 IoC라고 한다.
>
> IoC란 제어의 역전을 의미한다. 개발자가 직접 new를 통해 객체를 생성하게 된다면 해당 객체를 가르키는 레퍼런스 변수를 관리하기 어렵다. 그래서 스프링이 직접 해당 객체를 관리한다. 
- 스프링이 객체를 직접 관리하게 하기 위해서 어노테이션을 알아야 한다.
> 이때 우리는 주소를 몰라도 된다. 왜냐하면 필요할 때 DI하면 되기 때문이다.
>
> DI를 의존성 주입이라고 한다. 필요한 곳에서 ApplicationContext에 접근하여 필요한 객체를 가져올 수 있다. 
>
> ApplicationContext는 싱글톤으로 관리되기 때문에 어디에서 접근하든 동일한 객체라는 것을 보장해준다.
>
> ApplicationContext의 종류에는 두가지가 있는데 (root-applicationContext와 servlet-applicationContext) 이다.

#### 7.1.1. servlet-applicationContext
- ViewResolver, Interceptor, MultipartResolver 객체를 생성하고 웹과 관련된 어노테이션 Controller, RestController를 스캔 한다.
  - 해당 파일은 DispatcherServlet에 의해 실행된다.

#### 7.1.2. root-applicationContext
- 해당 어노테이션을 제외한 어노테이션 Service, Repository등을 스캔하고 DB관련 객체를 생성한다. (스캔이란 : 메모리에 로딩한다는 뜻)
  -  해당 파일은 ContextLoaderListener에 의해 실행된다. ContextLoaderListener를 실행해주는 녀석은 web.xml이기 때문에 root-applicationContext는 servlet-applicationContext보다 먼저 로드 된다.
  - 당연히 servlet-applicationContext에서는 root-applicationContext가 로드한 객체를 참조할 수 있지만 그 반대는 불가능하다. 생성 시점이 다르기 때문이다.
  
![image](https://user-images.githubusercontent.com/106478906/236387411-7dae4fa2-7007-4779-aaf1-0b0752b4fae1.png)
  
> static 파일과 자바 파일은 다르다.
- static 파일 : main 메소드가 실행되기 전부터 떠있다.(태초에 존재)
- 자바 파일 : 생성과 소멸이 일어나는 객체
- static 파일은 모든 곳에서 공유해서 사용하는 거라서 new로 메모리에 띄우는 경우가 대부분이다.
- 스프링은 이 객체의 생성을 DispatcherServlet이 해준다.(IoC) 
  - 컴포넌트 스캔을 통해서
  - 스프링 부트 : ALL 스캔
  - DispatcherServlet이 다 스캔해서 필요한 것을 메모리에 올린다.(이때 필요한 것 : 어노테이션으로 알아낸다)
  - 이렇게 메모리에 뜨면 주소를 분배한다. 

![image](https://user-images.githubusercontent.com/106478906/236385106-5f8f8ce8-e2ff-42de-a3af-d0c2cb189325.png)
![image](https://user-images.githubusercontent.com/106478906/236385752-51fc5a98-adee-431f-b616-7ae9ac7abc97.png)

> ContextLoaderListener : 각 스레드에서 관리하는 것이 아닌, DB 커넥션같이 딱 한번 띄워서 모든 스레드들이 공유해서 사용하면 되는 것들을 띄워준다.
- RootApplicationContext 파일을 읽는다.
- DispatcherServlet보다 먼저 실행되므로 DispatcherServlet이 띄우는 클래스들에 접근 못한다.
- 반대로 DispatcherServlet에서 띄우는 클래스들은 ContextLoaderListener에서 띄우는 것에 접근 가능하다.

### 7.2. Bean Factory
- 필요한 객체를 Bean Factory에 등록할 수도 있다. 여기에 등록하면 초기에 메모리에 로드되지 않고 필요할 때 getBean()이라는 메소드를 통하여 호출하여 메모리에 로드할 수 있다. 
이것 또한 IoC이다. 그리고 필요할 때 DI하여 사용할 수 있다. 
- ApplicationContext와 다른 점은 Bean Factory에 로드되는 객체들은 미리 로드되지 않고 필요할 때 호출하여 로드하기 때문에 lazy-loading이 된다는 점이다.

# 14강
### 8. 요청 주소에 따른 적절한 컨트롤로 요청 (Handler Mapping)
- http://localhost:8080/post/1 이런 형태로 GET요청이 오면 적절한 컨트롤러의 함수를 찾아서 실행한다.

### 9. 응답
- html파일을 응답할지 Data를 응답할지 결정해야 하는데 html 파일을 응답하게 되면 ViewResolver가 관여하게 된다.
  - ViewResolver가 리턴값에 [prefix와 suffix](https://developer-rooney.tistory.com/187)를 붙여준다.
- 하지만 Data를 응답하게 되면 MessageConverter가 작동하게 되는데 메시지를 컨버팅할 때 기본전략은 json이다.
  - @ResponseBody를 붙이면 리턴값을 파일이 아니라 데이터로 본다.
  - 리턴값이 객체일경우 그대로 반환하면 클라이언트가 이해 못하므로 MessageConverter가 json으로 바꿔서 응답해준다.

![image](https://user-images.githubusercontent.com/106478906/236385752-51fc5a98-adee-431f-b616-7ae9ac7abc97.png)

- (1) : 톰캣 실행시 web.xml파일이 읽힌다.
- (2) : ContextLoaderListener가 create
- (3) : ApplicationContext가 읽어지면서 root-context가 읽어지는데 
- (4) : 여기서는 DB관련 객체들을 컴포넌트 스캔해서 메모리에 올린다.
- (5) : 클라이언트가 요청
- (6),(7) : DispatcherServlet이 servlet-context에 의해 읽히고 
- (8) : web.xml의 업무를 분담해서 웹 관련된 것들을 메모리에 띄우고 주소 분배한다음 Data로 리턴할지, HTML파일로 리턴할지 정한다.






