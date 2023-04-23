
# <ChatGPT로 10분 만에 웹사이트 만들기> 강의 내용 정리
>[강의 링크](https://spartacodingclub.kr/online/special/chatgpt)

> 모든 내용을 정리하지는 않음

> 총 6강

> 개발 환경 : vscode

---

### index.html
~~~html
<!doctype html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>나만의 중고마켓</title>
    <link rel="stylesheet" href="https://s3.ap-northeast-2.amazonaws.com/materials.spartacodingclub.kr/easygpt/default.css">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65" crossorigin="anonymous">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-kenU1KFdBIe4zVF0s0G1M5b4hcpxyD9F7jL+jjXkk+Q2h455rYXK/7HAuoJl+0I4"
        crossorigin="anonymous"></script>
    <style>
        /* 꾸미기 */

    </style>
</head>

<body>
    <!-- 뼈대 잡기 -->
</body>

</html>
~~~

## 1. GPT에 명령 내리기

![image](https://user-images.githubusercontent.com/106478906/233788570-21783f95-b73c-47e3-83b0-eae84c386719.png)
![image](https://user-images.githubusercontent.com/106478906/233788599-e2866450-0fa1-4634-ab59-02418cb7aedd.png)
> 챗gpt가 만들어 준 버튼을 뼈대 잡기 부분에 추가한다.

![image](https://user-images.githubusercontent.com/106478906/233788674-30796387-461b-4e3f-a1af-6f86ba95bdb0.png)

![image](https://user-images.githubusercontent.com/106478906/233788941-9fdffc7e-96dd-4e10-9434-8506e27baca1.png)
> hero : 대문

### index.html
~~~html
  ...
<body>
    <section class="hero" style="background-color: #1C2331;">
        <div class="container">
            <div class="hero-content">
                <h1 style="color: #FFFFFF;">르탄이의 중고마켓</h1>
                <h2 style="color: #FFFFFF;">집에 있는 물건을 팝니다!</h2>
            </div>
        </div>
    </section>
</body>
~~~
![image](https://user-images.githubusercontent.com/106478906/233789296-38da2fbb-dde9-4378-a893-4bfd354e2d9c.png)
![image](https://user-images.githubusercontent.com/106478906/233789387-ae6dfad2-2287-4a37-bab3-7762ee643ec0.png)

## 2. GPT로 카드 만들기

![image](https://user-images.githubusercontent.com/106478906/233789419-4b388b22-f261-4033-9dae-2df959a9c4e7.png)
![image](https://user-images.githubusercontent.com/106478906/233789556-29405eb4-22ef-4764-a9bd-4078c81692f2.png)

> 코드를 붙여넣고 요청에 대한 답을 하지 말라고 한다.

![image](https://user-images.githubusercontent.com/106478906/233789716-a248479c-3d1c-45d6-8ce1-d3fb30e7ec05.png)

> 내가 이미지를 요청하면 https://source.unsplash.com/1600x900/? 이 주소에서 찾아서 달라는 뜻이다.

![image](https://user-images.githubusercontent.com/106478906/233821495-61b181ec-0ec8-4647-8d2e-ba25b809b4ea.png)
![image](https://user-images.githubusercontent.com/106478906/233821552-26a43792-330c-4434-9f74-0094d3776e92.png)

> 전기밥솥 이미지가 제대로 뜨지 않는다.
> 이미지를 누르면 새 창으로 열리게 요청했는데 반영되지 않았다.

![image](https://user-images.githubusercontent.com/106478906/233821744-5aebb386-df08-47dc-90b2-3aa2fcf17756.png)
![image](https://user-images.githubusercontent.com/106478906/233821752-1de977d7-7996-4665-acc6-545bd4ea7fe8.png)

> 이미지는 변경되었는데, 새 창으로 열리게 해달라는 요청이 반영되지 않았다.

![image](https://user-images.githubusercontent.com/106478906/233822469-5f8973e9-e49a-4c2b-8a5c-1e859ae3da51.png)

> 알려준 대로 <a>태그에 target="_blank" 속성을 추가했더니 새 창으로 열린다.
    
![image](https://user-images.githubusercontent.com/106478906/233823805-2713813e-7a27-413e-8b71-31937921078f.png)

![image](https://user-images.githubusercontent.com/106478906/233823822-7e0ce4de-5c09-40c7-a81b-6852b4c22741.png)

> hero 밑에 공백을 넣어달라고 요청한다.
    
## 3. 카드 꾸미기

![image](https://user-images.githubusercontent.com/106478906/233823885-fcb1ee5f-d749-4f8f-9c6a-2190037162ea.png)

![image](https://user-images.githubusercontent.com/106478906/233823980-c74ee528-376b-4925-b3c0-86f00d3a6e7d.png)

![image](https://user-images.githubusercontent.com/106478906/233823989-596acdf2-38cf-47e7-bc6a-b506fd68cbdb.png)

> 첫 번째 효과
<img width="1260" alt="제목 없음" src="https://user-images.githubusercontent.com/106478906/233824087-2f7b004d-2aff-4f13-9ed2-36463f81ad0b.png">

> 두 번째 효과
    
![image](https://user-images.githubusercontent.com/106478906/233824393-714d71b9-7c89-403e-83fd-5284c1338d23.png)

![image](https://user-images.githubusercontent.com/106478906/233824456-acb82d55-1316-4c56-a7d7-ac3fe4440cef.png)

> 이미지 파일을 소스가 들어있는 폴더에 넣어서 판매 상품을 추가했다.
    
## 4. 배포하기


