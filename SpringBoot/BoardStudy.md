## 1. 프로젝트 생성 해보기

~~~java
@Controller

public class BoardController {
    @GetMapping("/")
    @ResponseBody
    public String main(){

        return "Hello World!!";
    }
}
~~~
> @Controller 어노테이션을 추가하면 스프링이 여기가 컨트롤러임을 인지한다.

> @GetMapping("/") - 어떤 url로 접근할지 지정해주는 어노테이션이다. 

> localhost:포트번호/ 경로로 들어왔을 때
> @ResponseBody가 글자를 띄워준다.

![image](https://user-images.githubusercontent.com/106478906/232680318-97cdedc2-3945-416d-aedd-80da28712985.png)

## 2. DB에 테이블 생성
![image](https://user-images.githubusercontent.com/106478906/232681787-7e36973a-ffd3-4f68-ba8d-f0efc6b02257.png)

## 3. 게시글 작성폼 생성
### boardwrite.html 
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>게시글 작성폼</title>
</head>
<body>
    <div class="layout">
        <input type="text">
        <textarea></textarea>
        <button>작성</button>
    </div>
</body>
</html>
~~~

### BoardController.java
~~~java
@Controller
public class BoardController {

    @GetMapping("/board/write")
    public String boardWriteForm(){
        return "boardwrite";
    }
}
~~~
> @GetMapping("/board/write") - http://localhost:8090/board/write 이 url로 접속하면 boardwrite 화면단을 보여주겠다.

## 4. 글 작성 처리
### boardwrite.html 
~~~html
    <div class="layout">
        <form action="/board/writepro" method="post">
            <input name="title" type="text">
            <textarea name="content"></textarea>
            <button type="submit">작성</button>
        </form>
    </div>
~~~
> 작성 버튼을 눌렀을 때 form 안의 두 가지 데이터가 action의 주소로 넘어가게 된다.

### BoardController.java
~~~java
 @PostMapping("/board/writepro")
    public String boardWritePro(String title, String content){
        System.out.println("제목 : "+ title);
        System.out.println("내용 : "+ content);

        return "";
    }
~~~
- @PostMapping("") 안의 주소와 화면단의 form태그 action의 주소를 일치시켜야 한다.
- (String title, String content) : 매개변수를 받아준다.
![image](https://user-images.githubusercontent.com/106478906/232717292-4356954f-8471-4983-ba66-28fe04c2c6bf.png)
![image](https://user-images.githubusercontent.com/106478906/232717353-71e0511f-c002-4e57-85d1-001a60f7ae9c.png)

> 페이지가 없기 때문에 500 에러가 뜬다.

![image](https://user-images.githubusercontent.com/106478906/232717119-8451e19a-bdbe-468d-ba0b-7df27a07e9a5.png)
> 값은 잘 넘어왔음을 확인할 수 있다.
- 넘어온 값을 DB에 저장하기 위해서는 repository가 필요하다.

![image](https://user-images.githubusercontent.com/106478906/232718683-c6b90307-e40a-4d07-85ef-c8709e936cd0.png)
> com.example.board 안에 entity 패키지와 repository 패키지를 생성한다.
- entity 패키지 안에 Board 클래스를 만드는데 DB의 테이블명과 일치시키는 것이 좋다.

## Board.java
~~~java
@Entity
public class Board {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;
    private String title;
    private String content;
}
~~~
- [@Entity](https://siyoon210.tistory.com/25) : [JPA](https://gmlwjd9405.github.io/2019/08/04/what-is-jpa.html)에서 테이블을 의미한다.
> [JPA의 기본키 매핑](https://choiseonjae.github.io/jpa/jpa-%EA%B8%B0%EB%B3%B8%ED%82%A4%EC%A0%84/)
- @Id : primary key - 직접할당
- @GeneratedValue(strategy = GenerationType.IDENTITY) - 자동생성
    - strategy = GenerationType.IDENTITY : mariaDB, mysql에서 사용
    - strategy = GenerationType.SEQUENCE : oracle에서 사용
    - strategy = GenerationType.AUTO : 자동 지정
- DB의 필드와 타입이 같게 필드를 지정해준다.






