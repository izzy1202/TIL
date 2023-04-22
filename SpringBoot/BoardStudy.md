# <스프링부트 게시판 무작정 따라하기> 강의 내용 정리
>[강의 링크](https://www.youtube.com/watch?v=frI5CoZe-vE&list=PLZzruF3-_clsWF2aULPsUPomgolJ-idGJ&index=1)
> 총 18강
> 
>모든 내용을 정리하지는 않음
---



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

> URL에 파라미터를 넘길 때 쿼리 스트링 방식(view?id=000) 방식보다 PathVariable 방식이 더 깔끔하다.

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

            boardService.write(board); //DB에 저장한다.

            return "redirect:/board/list";
        }
~~~
![image](https://user-images.githubusercontent.com/106478906/233758259-4428425c-2248-476e-962d-167582758091.png)
![image](https://user-images.githubusercontent.com/106478906/233761131-53765a73-f158-466c-98c3-f6f764cf21f3.png)

> 수정이 완료됐다.
> 원래 JPA에서는 수정할때 덮어씌우는 방식을 절대 사용하면 안된다. JPA에는 변경감지(Dirty Checking)이라는 기능이 있어서 트랜잭션 내에서 DB에서 불러온 엔티티(객체)에 수정이 이뤄질경우 트랜잭션이 끝날 때 자동으로 DB에 반영되기 때문에 변경 감지 기능을 이용해서 수정해야 한다. 본 강의는 무작정 따라하기 강의라서 이 방식을 사용했지만 JPA 변경감지, JPA merge, JPA persist 등에 대한 추가적으로 공부가 필요하다.

## 9. 메시지 띄우기
### message.html
~~~html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script th:inline="javascript">

    /*<!CDATA[*/

    var message = [[${message}]];
    alert(message);

    location.replace([[${searchUrl}]]);


    /*]]>*/
</script>

</body>
</html>
~~~
> 컨트롤러에서 받아온 변수를 적용시켜줘야 한다.
- 컨트롤러에서 메세지를 전달해주면 alert가 메세지를 화면에 띄워주고 location.replace가 searchUrl로 경로를 이동시켜 준다.

### BoardController.java
~~~java
  //작성버튼 누르면 데이터 DB에 넘기기
    @PostMapping("/board/writepro")
    public String boardWritePro(Board board,Model model){
        boardService.write(board);

        model.addAttribute("message","글 작성이 완료되었습니다.");
        model.addAttribute("searchUrl","/board/list");
        return "message";
    }
~~~    
> model에 담겨서 message.html의 location.replace([[${searchUrl}]]); 여기로 넘어온다.

![image](https://user-images.githubusercontent.com/106478906/233762498-c5496719-ee50-4002-bba0-998fe3268e87.png)
![image](https://user-images.githubusercontent.com/106478906/233762505-ac8f4be8-35ac-4b16-87bf-db1e560ab87f.png)
> 글 작성 완료 알럿창이 뜨도록 하였다.
> 알럿창이 뜬 후, 리스트를 띄워주었다.

![image](https://user-images.githubusercontent.com/106478906/233762890-686918bb-b389-4da1-868b-ea0cf01b223f.png)
> 게시글 수정도 알럿창으로 뜨게 수정했다.
> 수정은 작성과 다르게 수정 완료 알럿창이 뜬 후, 상세페이지를 다시 띄워주었다.

## 10. 페이징 처리
![KakaoTalk_20230422_142928625](https://user-images.githubusercontent.com/106478906/233764780-50126165-0daf-4655-831e-ed42cd5db4a3.png)

- JPA는 페이지가 0부터 시작한다.
- size : 한 페이지에서 보여줄 게시글의 수

> 최근에 쓴 글이 제일 위에 올라오도록 게시글의 정렬 순서도 바꿔줘야 한다.

### BoardController.java
~~~java
    //리스트 불러오기
    @GetMapping("board/list")
    public String boardList(Model model, @PageableDefault(page = 0, size = 10, sort = "id", direction = Sort.Direction.DESC) Pageable pageable){

        model.addAttribute("list",boardService.boardList(pageable));
        return "boardlist";
    }
~~~
![image](https://user-images.githubusercontent.com/106478906/233764987-342e545a-603a-4899-a931-be413c036b40.png)
> domain 패키지 안에 있는 Pageable 클래스를 사용한다.
> @PageableDefault 어노테이션을 써서 설정해줄 수 있다.
- sort : 정렬 기준
- direction : 정렬을 어떻게 할건지(오름차순, 내림차순)

### BoardService.java
~~~java
    //게시글 리스트 처리
    public Page<Board> boardList(Pageable pageable){
        return boardRepository.findAll(pageable);
    }
~~~
>findAll이라는 메소드를 사용하면 DB의 모든 정보를 가져오게 되는데, pageable이라는 클래스를 넘겨주게 되면 그 안에 페이지가 몇페이지인지, 한번에 보여줄 글의 개수 등의 정보를 담아서 보내줄 수 있다.

![image](https://user-images.githubusercontent.com/106478906/233765375-c64e2f6e-2ab6-45e0-a525-9bda12e2de11.png)
> 매개변수가 없는 경우에는 return값이 리스트로 넘어오는데, 지금의 경우 Page라는 클래스로 return하게 된다.

![image](https://user-images.githubusercontent.com/106478906/233765511-d539877d-957c-4b5e-b145-a771c1ebcf7d.png)
![image](https://user-images.githubusercontent.com/106478906/233765554-c2987867-5f56-410a-93f0-7bd1644204bf.png)

> http://localhost:8090/board/list?page=0 주소를 이렇게 입력해도 같은 결과가 나온다.(0페이지부터 시작하기 때문)

![image](https://user-images.githubusercontent.com/106478906/233765604-f9856363-3a05-4268-8594-32a6318afdd3.png)
> http://localhost:8090/board/list?page=1&size=5 이렇게 한 페이지에 보여줄 글의 개수를 정해줄 수도 있다.

![KakaoTalk_20230422_150452703](https://user-images.githubusercontent.com/106478906/233765925-6ac6a806-981a-43d7-b982-be146c428429.png)
![KakaoTalk_20230422_150452703_01](https://user-images.githubusercontent.com/106478906/233765926-a53e34a5-489e-4b33-a55e-9423d0618ed8.png)

> list.getPageable().getPageNumber() : pageable에서 넘어온 현재 페이지를 가져올 수 있다.

### BoardController.java
~~~java
//리스트 불러오기
    @GetMapping("board/list")
    public String boardList(Model model, @PageableDefault(page = 0, size = 10, sort = "id", direction = Sort.Direction.DESC) Pageable pageable){

        Page<Board> list = boardService.boardList(pageable);

        int nowPage = list.getPageable().getPageNumber() + 1; // pageable이 갖고 있는 페이지는 0부터 시작하기 때문에 1을 더해준다.
        int startPage = Math.max(nowPage - 4, 1); // 매개변수에 들어온 두 값을 비교해서 높은 값을 반환한다.
        int endPage = Math.min(nowPage + 5, list.getTotalPages()); // 매개변수에 들어온 두 값을 비교해서 낮은 값을 반환한다.

        model.addAttribute("list", list);
        model.addAttribute("nowPage", nowPage);
        model.addAttribute("startPage", startPage);
        model.addAttribute("endPage", endPage);
        return "boardlist";
    }
~~~
### boartlist.html
~~~html
...

        <th:block th:each="page : ${#numbers.sequence(startPage, endPage)}">
            <a th:if="${page != nowPage}" th:href="@{/board/list(page = ${page - 1})}" th:text="${page}"></a>
            <strong th:if="${page == nowPage}"  th:text="${page}" style="color : red"></strong>
        </th:block>
    </div>

</body>
</html>
~~~
> <th:block> : 굳이 태그로 감쌀 필요 없는 부분을 타임리프 문법을 이용해서 사용할 때 쓰는 태그이다.

![image](https://user-images.githubusercontent.com/106478906/233767302-89f8d4b4-a8a1-4039-9ec2-abaae6e6df0a.png)

> 페이징 처리 한 결과이다.

## 11. 검색 기능
![KakaoTalk_20230422_155322173](https://user-images.githubusercontent.com/106478906/233768073-df442b50-a48c-4f29-aca6-d67e18366b74.png)
![KakaoTalk_20230422_155322173_01](https://user-images.githubusercontent.com/106478906/233768074-6bc2998b-a93a-409f-9538-5aeccbd10a33.png)
![KakaoTalk_20230422_155322173_02](https://user-images.githubusercontent.com/106478906/233768078-180c0a61-283a-4d7d-ad87-2dda99b16a98.png)

> findByTitleContaining : 대소문자 입력 주의

### BoardRepository.java
~~~java
@Repository
public interface BoardRepository extends JpaRepository<Board,Integer> {

    Page<Board> findByTitleContaining(String searchKeyword, Pageable pageable);
}
~~~
### BoardService.java
~~~java
    //검색
    public Page<Board> boardSearchList(String searchKeyword, Pageable pageable){
        return boardRepository.findByTitleContaining(searchKeyword, pageable);
    }
~~~
### BoardController.java
~~~java
     @GetMapping("board/list")
     public String boardList(Model model,
                            @PageableDefault(page = 0, size = 10, sort = "id", direction = Sort.Direction.DESC) Pageable pageable,
                            String searchKeyword){

        Page<Board> list = null;

        if(searchKeyword == null){
            list = boardService.boardList(pageable);
        }else{
            list = boardService.boardSearchList(searchKeyword, pageable);
        }

    ...
~~~
![image](https://user-images.githubusercontent.com/106478906/233783478-57d8379e-9ada-4b7e-9571-2670b66d26df.png)
> 제목에 '11'을 포함하는 게시글들을 보여준다.

> 2 페이지를 누르면 검색된 리스트가 아닌, 기존 리스트의 2 페이지로 넘어가는 문제가 발생한다.

![image](https://user-images.githubusercontent.com/106478906/233783734-b1a16f21-9e87-4b85-862c-c3213fb9ac2a.png)
> http://localhost:8090/board/list?searchKeyword=11&page=1 이렇게 주소 뒤에 page를 붙여줘야 검색 결과의 2페이지로 이동한다.

### boardlist.html
~~~html
    ...
        <th:block th:each="page : ${#numbers.sequence(startPage, endPage)}">
            <a th:if="${page != nowPage}" th:href="@{/board/list(page = ${page - 1}, searchKeyword = ${param.searchKeyword})}",  th:text="${page}"></a>
            <strong th:if="${page == nowPage}"  th:text="${page}" style="color : red"></strong>
        </th:block>
    </div>
~~~
> searchKeyword = ${param.searchKeyword})}" 이 부분 추가하면 주소에 page 안붙여도 검색 결과 2페이지로 잘 이동한다.
- param이 쿼리 스트링중에 특정 키워드(searchKeyword)를 가져와서 앞의 searchKeyword에 넣어준다.
- searchKeyword라는 파라미터가 url에 있을때 값을 물고가기 때문에 페이징이 유지가 된다.
### boardlist.html
~~~html
    ...
        <form th:action="@{/board/list}" method="get">
            <input type="text" name="searchKeyword">
            <button type="submit">검색</button>
        </form>
~~~
![image](https://user-images.githubusercontent.com/106478906/233787232-c426660b-3864-4518-879b-fe2bcd178f7f.png)
> '메세'라고만 입력해도 제목에 메세가 포함된 글이 나온다.













