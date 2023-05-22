# <디지털기초역량 향상을 위한 웹개발 입문 과정> 강의 내용 정리
>[강의 링크](https://www.e-itwill.com/course/course_view.jsp?id=125)

> 총 41강
> 
>모든 내용을 정리하지는 않음

---
# 1. IO 이해와 응용 학습
## 1.1. Input과 Output
- Input : 저장
- Output : 읽기
- I/O를 최대한 줄여야 컴퓨터의 속도가 빨라진다.
![image](https://github.com/izzy1202/TIL/assets/106478906/ca0a1d0c-b13e-48b0-81ba-6de2be436ccd)
- Input을 모으고 있다가 더티 체킹해서 한번에 Input한다.

## 1.2. I/O가 많이 발생하면 어떻게 해야할까?
1. 메모리 늘리기
2. 필요한 데이터가 최대한 많이 메모리에 존재

### 1.3. 통신을 통한 파일 다운로드
![image](https://github.com/izzy1202/TIL/assets/106478906/f9c9e2d2-3059-49f9-9bac-a61d9d89cfca)
- RAM이 4기가일때, 8기가의 파일을 다운로드 받는다고 하면 RAM의 2기가는 OS용이라서 다운 가능한 데이터는 2기가이다. 다운 받은 2기가를 하드디스크에 I/O 4번 하게된다.
- I/O를 줄이기 위한 가장 좋은 방법은 분산 처리이다.
  - 빅데이터는 데이터를 분산해서 처리한다(하둡, 몽고db 샤딩)
  
# 2. TCP 통신
## 2.1. Protocol
- Protocol : 약속(A-B)
- 인터페이스 : 일방적인 약속(A)

## 2.2. UDP(User Datagram Protocol)

## 2.3. TCP(Transmission Control Protocol)
