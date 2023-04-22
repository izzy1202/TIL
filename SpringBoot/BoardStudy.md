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
- [@Entity](https://siyoon210.tistory.com/25) : [JPA](https://gmlwjd9405.github.io/2019/08/04/what-is-jpa.html) 용어로, DB의 테이블을 의미한다.
> [JPA의 기본키 매핑](https://choiseonjae.github.io/jpa/jpa-%EA%B8%B0%EB%B3%B8%ED%82%A4%EC%A0%84/)
- @Id : primary key - 직접할당
- @GeneratedValue(strategy = GenerationType.IDENTITY) - 자동생성
    - strategy = GenerationType.IDENTITY : mariaDB, mysql에서 사용
    - strategy = GenerationType.SEQUENCE : oracle에서 사용
    - strategy = GenerationType.AUTO : 자동 지정
- DB의 필드와 타입이 같게 필드를 지정해준다.

### BoardController.java
~~~java
 @PostMapping("/board/writepro")
    public String boardWritePro(String title, String content){
        System.out.println("제목 : "+ title);
        System.out.println("내용 : "+ content);

        return "";
    }
~~~
> 매개변수를 많아지면 하나씩 받아주기 번거롭다.
> Board entity 형식 그대로 받아올 수 있다.

### Board.java
~~~java
@Data  //어노테이션 추가한다.
@Entity
public class Board {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer id;
    private String title;
    private String content;
}
~~~
~~~java
 @PostMapping("/board/writepro")
    public String boardWritePro(Board board){
        System.out.println(board.getTitle());
        return "";
    }
~~~
![image](https://user-images.githubusercontent.com/106478906/233619903-3e617a2c-e459-40f1-8d9a-93a20b83b23c.png)
![image](https://user-images.githubusercontent.com/106478906/233619972-505d7394-b421-4585-8619-fd222baf61ee.png)
> 제목이 잘 넘어온다.

### BoardRepository.java
~~~java
@Repository //레파지토리임을 알려준다.
public interface BoardRepository extends JpaRepository<Board,Integer> {
}
~~~
> Board 엔티티, primary key로 지정한 컬럼의 타입(Integer)

### BoardService.java
~~~java
@Service //서비스라고 알려줌
public class BoardService {

    @Autowired //원래는 자바에서 객체 생성할 때 new~ 이렇게 해야하지만 autowired 어노테이션을 사용하면 스프링 빈이 의존성을 주입해준다.
    private BoardRepository boardRepository;
    public void write(Board board){
        boardRepository.save(board);
    }
}
~~~
> 이 BoardService를 BoardController에서 이용한다.

### BoardController.java
~~~java

     @Autowired
    private BoardService boardService; //의존성 주입

    ...
    
    @PostMapping("/board/writepro")
    public String boardWritePro(Board board){
        boardService.write(board);
        return "";
    }
~~~
![image](https://user-images.githubusercontent.com/106478906/233626057-bfa2e77b-f680-4bbc-b837-ceb6604d8b3d.png)
![image](https://user-images.githubusercontent.com/106478906/233626240-293a2ea4-3d3e-4bd5-b4cf-31715c2c21e9.png)
> DB에 데이터가 잘 들어왔다.

## 5. 게시글 리스트
![image](https://user-images.githubusercontent.com/106478906/233629057-3bd2c35f-d502-41df-8c41-b5969675896b.png)
> 프로시저를 이용하여 테스트 데이터를 넣어준다.
- use board; : board 스키마를 사용하겠다.
- call testDataInsert; : testDataInsert 프로시저를 실행해라.

### BoardController.java
~~~java
   @GetMapping("board/list")
    public String boardList(){
        return "boardlist";
    }
~~~

### boardlist.html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>게시글 리스트 페이지</title>
</head>
<style>
    .layout {
        width : 500px;
        margin : 0 auto;
        margin-top : 40px;
    }
</style>
<body>
    <div class="layout">
        <table>
            <thead>
                <tr>
                    <th>글번호</th>
                    <th>제목</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>제목입니다.</td>
                </tr>
            </tbody>
        </table>

    </div>

</body>
</html>
~~~
![image](https://user-images.githubusercontent.com/106478906/233642549-4e42adac-0403-49c1-86a0-c53ee0563129.png)
> 리스트 페이지를 띄웠다.

### BoardService.java
~~~java
public List<Board> boardList(){
        return boardRepository.findAll();
    }
~~~

> 글을 불러올 메소드

### BoardController.java
~~~java
 @GetMapping("board/list")
    public String boardList(Model model){

        model.addAttribute("list",boardService.boardList());
        return "boardlist";
    }
~~~
> 데이터를 담아서 우리가 볼 페이지로 보내주기 위해 Model을 사용한다.
- boardService.boardList()를 실행하면 반환되는 리스트를 list라는 이름으로 받아서 넘기겠다.

### boardlist.html
~~~html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://thymeleaf.org"> //타임리프(데이터를 받아서 처리해주는 템플릿)를 사용하겠다.
    
    ...
    
             <tbody>
                <tr th:each="board : ${list}">
                    <td th:text="${board.id}">1</td>
                    <td th:text="${board.title}">제목입니다.</td>
                </tr>
            </tbody>
 ~~~
    
> each : 반복문(list에서 board가 없어질 때까지 반복하겠다.

![image](https://user-images.githubusercontent.com/106478906/233661066-779faa6d-6787-44f0-929e-02d2e4ac0d2b.png)
> 게시글 불러오기 성공

## 6. 게시글 상세 페이지
### boardview.html
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>게시글 상세 페이지</title>
</head>
<body>

<h1>제목입니다.</h1>
<p>내용이 들어갈 부분입니다.</p>
</body>
</html>
~~~
### BoardController.java
~~~java
//게시글 상세 페이지 불러오기
    @GetMapping("/board/view")
    public String boardView(){

        return "boardview";
    }
 ~~~
![image](https://user-images.githubusercontent.com/106478906/233753543-0269cba5-0323-4488-8a7a-9170b4264deb.png)
> 내용이 불러와졌다.

> findById로 어떤 게시글을 불러올지 지정해준다.

![image](https://user-images.githubusercontent.com/106478906/233753811-b3ff8540-f989-458e-800e-b1cb37236570.png)
> 오류가 나는 이유는 optional값으로 받아와지기 때문이다.

![image](https://user-images.githubusercontent.com/106478906/233753899-13003130-3201-4a5b-b14e-339aee8e379c.png)
> 뒤에 get()을 붙이면 오류가 사라진다.

### BoardController.java
~~~java
//게시글 상세 페이지 불러오기
    @GetMapping("/board/view") // localhost:8090/board/view?id=1
    public String boardView(Model model, Integer id){

        model.addAttribute("board",boardService.boardView(id));
        return "boardview";
    }
 ~~~
> 주소의 view?id=1 에서 1이 Integer id로 들어가고, 들어간 1이 boardView(id)로 들어간다.
- 파라미터와 get 방식이다.

### boardview.html
~~~html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>게시글 상세 페이지</title>
</head>
<body>

<h1 th:text="${board.title}">제목입니다.</h1>
<p th:text="${board.content}">내용이 들어갈 부분입니다.</p>
</body>
</html>
~~~
![image](https://user-images.githubusercontent.com/106478906/233754267-7a8a08ca-dc1e-40c8-a35e-7137286a08ae.png)
> DB의 첫번째 글이 나온다.

### boardlist.html
~~~html
        <tbody>
            <tr th:each="board : ${list}">
                <td th:text="${board.id}">1</td>
                <td>
                    <a th:text="${board.title}" th:href="@{/board/view(id=${board.id})}"></a>
                </td>
            </tr>
        </tbody>
~~~
> 게시글 제목을 눌렀을 때 글 번호로 해당 게시글을 불러온다.

![image](https://user-images.githubusercontent.com/106478906/233754675-cadfd161-d05c-454f-9a14-1fa4289f6802.png)

## 7. 게시글 삭제
### boardview.html
~~~html
<body>

<h1 th:text="${board.title}">제목입니다.</h1>
<p th:text="${board.content}">내용이 들어갈 부분입니다.</p>
<a href="#">글삭제</a>
</body>
~~~
### boardService.java
~~~java
 //특정 게시글 삭제
    public void boardDelete(Integer id){
        boardRepository.deleteById(id);
    }
~~~
### boardController.java
~~~java
//게시글 삭제
    @GetMapping("/board/delete")
    public String boardDelete(Integer id){
        boardService.boardDelete(id);

        return "redirect:/board/list";
    }
~~~
![image](https://user-images.githubusercontent.com/106478906/233755756-b24bf2f7-2e0d-44f4-ba5e-f423051e6301.png)
![image](https://user-images.githubusercontent.com/106478906/233755764-6c355313-4875-41da-a01c-b247cf675cbb.png)
> 5번 게시글이 삭제됐다.

### boardview.html
~~~html
    <a th:href="@{/board/delete(id=${board.id})}">글삭제</a>
~~~
![image](https://user-images.githubusercontent.com/106478906/233756388-bf867e0a-427a-411c-81a5-1cf322425b39.png)
> 글 삭제가 잘 된다.

## 8. 게시글 수정
- cf. 인텔리제이 : shift 두번 누르면 검색 가능
### boardview.html
~~~html
    <a th:href="@{/board/modify/{id}(id=${board.id})}">글수정</a>
~~~
### BoardController.java
~~~java
 //게시글 수정 페이지 불러오기
    @GetMapping("/board/modify/{id}")
    public String boardModify(@PathVariable("id") Integer id){
        return "boardmodify";
    }
~~~
> @PathVariable : url이 들어왔을 때 / 뒤의 {id}가 인식돼서 Integer 형태의 id로 들어온다.

### boardmodify.html (글 작성폼과 동일)
~~~html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>게시글 수정폼</title>
</head>

<style>
    .layout {
        width : 500px;
        margin : 0 auto;
        margin-top : 40px;
    }

    .layout input {
        width : 100%;
        box-sizing : border-box;
        margin-top : 10px;
    }

    .layout textarea {
        width : 100%;
        margin-top : 10px;
        min-height : 300px;
    }

</style>
<body>
<div class="layout">
  <form action="/board/writepro" method="post">
    <input name="title" type="text">
    <textarea name="content"></textarea>
    <button type="submit">수정</button>
  </form>
</div>
</body>
</html>
~~~
![image](https://user-images.githubusercontent.com/106478906/233757098-cc05c3a0-8487-4843-a7e7-cd7ede654de1.png)
> 수정 버튼을 누르면 수정 폼이 뜬다.

![image](https://user-images.githubusercontent.com/106478906/233757123-91f8a11c-17eb-482b-ae65-3105aa1a4ee6.png)
> 수정 폼에 원래 데이터도 같이 가져와야 한다.

![image](https://user-images.githubusercontent.com/106478906/233757250-a0018187-3426-40a6-acbb-d96f9b6eb4b1.png)

> 쿼리 스트링 방식(view?id=000) 방식보다 PathVariable 방식이 더 깔끔하다.

### BoardController.java
~~~java
//게시글 수정 페이지 불러오기
    @GetMapping("/board/modify/{id}")
    public String boardModify(@PathVariable("id") Integer id,
                              Model model){
        
        //게시글 원본 데이터 불러오기
        model.addAttribute("board",boardService.boardView(id));
        return "boardmodify";
    }
~~~

### boardmodify.html
~~~html
    <form action="/board/writepro" method="post">
        <input name="title" type="text" th:value="${board.title}">
        <textarea name="content" th:text="${board.content}"></textarea>
        <button type="submit">작성</button>
    </form>
~~~
> textarea는 value가 안들어가서 text로 넣어줘야 한다.

![image](https://user-images.githubusercontent.com/106478906/233757814-3fcd5c0e-9757-49f0-9ad1-6da9f5257e22.png)

> 내용이 잘 넘어온다.

### boardmodify.html
~~~html
    <form th:action="@{/board/update/{id}(id=${board.id})}" method="post">
        <input name="title" type="text" th:value="${board.title}">
        <textarea name="content" th:text="${board.content}"></textarea>
        <button type="submit">수정</button>
    </form>
~~~
### BoardController.java
~~~java
//게시글 수정 처리
    @PostMapping("/board/update/{id}")
    public String boardUpdate(@PathVariable("id") Integer id, Board board){
        
        Board boardTemp = boardService.boardView(id); // 기존 글이 boardTemp에 담겨져서 온다.
        boardTemp.setTitle(board.getTitle());  // 새로 입력한 내용을 기존 내용에 덮어쓴다.
        boardTemp.setContent(board.getContent());
        
        return "redirect:/board/list";
    }
~~~
