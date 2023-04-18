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
~~~java
 <div class="layout">
        <form action="/board/writedo" method="post">
            <input name="title" type="text">
            <textarea name="content"></textarea>
            <button>작성</button>
        </form>
  </div>
~~~
> 전송 버튼을 눌렀을 때 form 안의 두가지 데이터가 이 주소로 넘어가게 된다.
