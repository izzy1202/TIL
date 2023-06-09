# <윤성우의 열혈 Java> 강의 내용 정리
>[강의 링크](https://cafe.naver.com/cstudyjava/135782?boardType=L)

> Chapter 01 ~ Chapter 13
> 
>모든 내용을 정리하지는 않음

---

# Chapter 01

## 1. 자바 프로그램과 실행의 원리에 대한 이해

### 1.1. 일반적 프로그램과 자바 프로그램의 차이

#### 일반 프로그램
하드웨어의 운영체제가 프로그램을 실행

#### 자바 프로그램
- 하드웨어의 운영체제가 프로그램을 실행하는 것까지는 일반 프로그램과 동일
- 자바 프로그램이 실행되기 위해서는 Java Virtual Machine 이라는 가상머신이 먼저 실행되어야 함
  (자바 프로그램은 JVM에 완전히 종속되어서 실행되는 구조)
- 자바 런처(java.exe)는 JVM을 실행시키고 그 위에 자바 프로그램을 올려준다.

### 1.2. 운영체제에 따른 자바 가상머신의 차이
- 자바는 한 번 프로그램을 작성하면 운영체제에 상관없이 동작시킬 수 있다.

### 1.3. 자바 컴파일러와 자바 바이트코드

#### 자바 컴파일러(javac.exe)
- 소스파일(소스코드 존재하는 파일) -- 컴파일러 역할 --> 클래스 파일(바이트코드 존재하는 파일)
- 소스파일 : 우리가 알아볼 수 있는 문장
- 클래스 파일 : 소스파일을 JVM이 알아볼 수 있는 문장으로 바꾼 것
- cf. 바이트코드 : 명령문

#### 자바 런처(java.exe)
- 자바 프로그램과 자바 가상머신을 처음 구동하는 소프트웨어
- 클래스 파일을 대상으로 구동을 시작한다.

## 2. 첫 번째 자바 프로그램의 관찰과 응용

### 2.1. 프로그램의 골격과 구성

- 중괄호를 이용해서 클래스와 메소드의 영역을 구분
- 문장(명령문)의 끝에는 세미콜론을 붙여서 문장의 끝 표시
- 프로그램 실행 시 main 메소드 안 문장들 순차적 실행
- System.out.println의 괄호 안에 출력 내용 큰따옴표로 묶어서 표시
- System.out.println 실행 이후 자동 개행


# Chapter 02

## 1. 변수의 이해와 활용

### 1.1. 메모리 공간 할당의 예

#### 1.1.1. 변수 선언을 통해 결정하는 2가지
1) 변수의 이름
2) 변수의 용도

### 1.2. 다양한 자료형 활용의 예
- 자료형은 데이터를 표현, 해석하는 방법
- 두 개의 변수 동시 선언 가능하나, 한 문장에서 하나의 변수를 선언하는 것이 좋다고 여겨짐

### 1.3. 변수 이름 제약사항
1) 자바는 대소문자를 구분한다.
2) 변수의 이름은 숫자로 시작할 수 없다.
3) $와 _이외의 특수문자는 사용할 수 없다.
4) 키워드는 변수의 이름으로 사용할 수 없다.
- 키워드 : 자바의 문법을 구성하는 약속된 예약어
   ex) int, double ...

## 2. 실수의 표현 방식 이해하기
- 정수와 달리 실수는 오차 없이 표현이 불가능

## 3. 자바의 기본 자료형

### 3.1. 정수 자료형

#### 3.1.1. int형 변수를 선택해야 하는 이유
- 기본적으로 자바는 정수형 사칙연산을 할 때 int 자료형으로 진행한다.
-> 규모를 JVM이 각각 판단을 하게 되어버리면 시스템 성능 저하로 이어진다.
- int형으로 설정하게 되면 시스템 성능 저하될 일 없다.
- cf. 데이터의 크기가 너무 많고, 연산이 중심이 되는 게 아니라 저장에 의미가 있는 경우에는 byte나 short를 쓸 수도 있다.

### 3.2. 실수 자료형
- 기본적으로 자바는 실수형 사칙연산을 할 때 double 자료형으로 진행한다.
- float와 double 사이에서의 자료형 선택 기준은 정밀도이다.
-> 바이트가 더 큰 것은 오차없이 표현할 수 있는 값의 크기가 크다는 것

### 3.3. 문자 자료형
- 자바의 문자 자료형은 char
- 자바는 문자를 2바이트 유니코드로 표현한다.
- 작은 따옴표로 묶어서 하나의 문자를 표시한다.
- 문자의 저장은 유니코드 값의 저장으로 이어진다.

### 3.4. 논리 자료형

# Chapter 03

## 1. 상수(Constants)

### 1.1. 자바의 일반적인 상수

#### 1.1.1. 자바에서 말하는 '상수'
- 상수는 변수에 값을 딱 한 번만 할당할 수 있다
- 한 번 할당된 값은 변경이 불가능하다
- 키워드 final 선언이 붙어있는 변수

#### 1.1.2. final 기반의 상수 선언의 예
- 상수의 이름은 모두 대문자로 짓는 것이 관례
- 이름이 둘 이상의 단어로 이뤄질 경우 단어를 언더바로 연결하는 것이 관례

### 1.2. 리터럴(Literals)에 대한 이해
- 리터럴 : 자료형을 기반으로 표현이 되는 상수를 의미한다.
ex) int num1 = 5 + 7;
ex) double num2 = 3.3 + 4.5;
- 정수는 무조건 int형으로 인식하기로 약속되어 있음
- 따라서 5와 7은 '정수형 리터럴'이다.
- 그리고 3.3과 4.5는 '실수형 리터럴'이다.
- '리터럴'이라는 표현은 '상수'라는 표현으로 대신하는 경우가 많다.

### 1.3. 정수형 상수(리터럴)의 표현 방법
~~~java
  int num1 = 123;    // 10진수 표현
  int num2 = 0123;   // 8진수 표현
  int num3 = 0x123;  // 16진수 표현
~~~

### 1.4. long형 상수(리터럴)의 표현 방법
~~~java
  System.out.println(3147483647 + 3147483648);
~~~
- 컴파일시 Integer number too large 라는 오류 메시지를 전달한다.
~~~java
  System.out.println(3147483647L + 3147483648L);
~~~
- l 또는 L을 붙여서 long형 상수로 표현해 달라는 요청을 해야 한다.

### 1.5. 정수형 상수의 이진수 표현방법과 언더바 삽입
~~~java
  byte seven = 0B111;
  int num205 = 0B11001101;
~~~
- 0B 또는 0b를 붙여서 이진수 표현
~~~java
  int num = 100_000_000;
  int num = 12_34_56_78_90;
~~~

### 1.6. 실수형 상수(리터럴)
~~~java
  System.out.println(3.0004999 + 2.0004999);
  System.out.println(3.0004999D + 2.0004999D);
~~~
- 실수는 기본 double형 double형임을 명시하기 위해 d 또는 D 삽입
가능
-> 잘 쓰지는 않음
~~~java
  System.out.println(3.0004999f + 2.0004999f);
~~~
- 실수형 상수를 float형으로 표현하려면 f 또는 F 삽입
-> 메모리 공간은 적게 쓰겠지만 오차의 크기가 커진다.

#### 1.6.1. 실수형 상수의 e 표기법
~~~java
  3.4e3  -> 3.4 x 10^3 = 3400.0
  3.4
~~~

### 1.7. 이스케이프 시퀀스(escape sequences)
- 화면상의 어떠한 상황 또는 상태를 표현하기 위해 약속된
문자
- '\r' : 캐리지 리턴(carriage return) 문자로, 커서가 맨 앞으로 이동

## 2. 형 변환

### 2.1. 자료형 변환의 의미와 필요한 이유는?
- 두 피연산자의 자료형이 일치해야 동일한 방법을 적용하여 연산을 진행할 수 있다.
- 피연산자의 자료형이 일치하지 않을 때 형(Type)의 변환을 통해 일치시켜야 한다.

### 2.2. 자동 형 변환(Implicit Conversion)
- 규칙 1. 자료형의 크기가 큰 방향으로 형 변환이 일어난다.
- 규칙 2. 자료형의 크기에 상관없이 정수 자료형보다 실수 자료형이 우선한다.
- cf. float가 long보다 우선시되는 이유
: 데이터 손실을 최소화하기 위해 정수보다 실수가 우선하는데, float 자료형은 표현할 수 있는 범위가 넓다.
반면, long 자료형은 소수점 이하는 표현 못한다. 따라서 float 자료형을 long 자료형으로 형 변환하게 되면 소수점 이하는 사라진다.

### 2.3. 명시적 형 변환(Explicit Conversion)
- 자동 형 변환 규칙에 부합하지는 않지만, 형 변환이 필요한 상황이면 명시적 형 변환을 진행한다.

# Chapter 04

## 1. 자바에서 제공하는 이항 연산자들
- 하나의 문장 안에 둘 이상의 연산자가 존재할 경우, 연산자의 우선순위를 적용해서 연산 순서를 정한다. 연산자의 우선순위가 같을 경우 결합 방향을 적용하여 연산 순서 결정한다.

### 1.1. 정수형 나눗셈과 실수형 나눗셈
- 피연산자의 자료형이 무엇이냐에 따라서 나눗셈의 형태가 달라진다.

### 1.2. 복합 대입 연산자
- 복합 대입 연산자를 쓸 경우, 자바 프로그램이 그 문장을 해석하는 과정에서 필요로 하는 강제 형변환을 알아서 해주기도 한다.
-> 하지만 좋지 않은 코드. 강제 형변환을 해주는 것이 명확하다.

### 1.3. 관계 연산자
- 관계 연산자의 결과는 true / false 이다.
~~~java
  System.out.println("7.0 == 7 : " + (7.0 == 7)); //7.0 == 7 : true
~~~
-> 원래라면 두 피연산자의 자료형이 달라서 비교 불가지만, 7(int)이 7.0(double)로 자동 형변환된다.

### 1.4. 논리 연산자
- 피연산자도 true / false여야 한다.
- cf. num = 2 + 3 일때, 5가 num에 한번에 들어가는 것이 아니라 연산이 이루어지고 결과가 반환되어서 그 연산문을 대체하게 되고 그 다음 대입이 이루어지게 된다고 생각하는 것이 좋다.

### 1.5. 논리 연산자 사용시 주의점 : SCE
- 하나의 문장에 너무 많은 내용을 담기 보다는 따로 떼어서 쓰는 것이 낫다.
~~~java
  result = ((num1 += 10) < 0) && ((num2 += 10) > 0);
  result = ((num1 += 10) > 0) || ((num2 += 10) > 0);
~~~
-> num1 , num2의 값을 모두 증가시키기 위해서는 독립된 문장으로 쓰는 것이 낫다.

## 2. 자바에서 제공하는 단항 연산자들
- 부호 연산자 –는 변수에 저장된 값의 부호를 바꾸어 반환한다.
- 부호 연산자로서의 + 연산자도 연산자로서의 의미는 갖는다.

## 3. 비트를 대상으로 하는 연산자들
- 비트 연산자를 잘 사용하면 코드를 조금 더 그럴듯 하게 만들 수 있다.
- 잘 안쓰는 연산자로 치부하지 말기

### 3.1. 비트 연산자의 이해
- 비트 연산자의 피연산자는 정수로 제안이 되어있다.

![image](https://user-images.githubusercontent.com/106478906/230700743-f8b57770-ff45-4f61-a2f0-44471e82aabd.png)

-> n1 n2를 byte로 선언했어도 연산하는 과정에서 int형으로 변환되기 때문에 n3에 저장하려면 byte로 강제형변환을 해야한다.

### 3.2. 비트 연산자
- 뒤에서부터 첫 번째 비트
- ^ : 비트 단위로 XOR 연산, 비트 A와 비트 B가 서로 달라야 1
- ~ : 피연산자의 모든 비트를 반전시킴 

### 3.3. 비트 쉬프트 연산자
![image](https://user-images.githubusercontent.com/106478906/230701349-421294f2-7fe7-4e38-8e78-7b4900287807.png)
-> 두 칸 왼쪽으로 이동시키면 제일 오른쪽에 두 칸이 남게되고, 제일 왼쪽의 두 칸의 값은 버려진다.
-> n이 저장하고 있는 값을 미는 것이 아니라, 밀어서 얻어진 결과를 하나의 결과로 만들어 낼 뿐이다.
-> n이 가진 값 자체가 바뀌는 것은 아니다.
- '>>' : 가장 왼쪽 비트가 음수/양수냐에 따라서 결정
- '>>>' : 가장 왼쪽 비트에 상관없이 0으로 채운다.
- 왼쪽으로의 쉬프트는 값의 2배 증가, 오른쪽으로의 쉬프트는 값을 2로 나눈 결과로 이어진다.
- cf. 특정 시스템의 CPU가 떨어지는 경우가 있는데, 곱셈/나눗셈이 덧셈/뺄셈에 비해 CPU를 많이 차지한다. 시스템 성능이 떨어지는 경우에는 프로그래머들이 그런 것도 고려해서 곱셈/나눗셈 대신 이런 비트 연산자를 사용하기도 한다.

# Chapter 05

## 1. if 그리고 else

### 1.1. if문
- if문에 속한 문장이 하나일 경우 중괄호 생략 가능
-> 프로그래머들은 불필요한 것을 최소화하는 것을 좋아하기 때문에 이것에 익숙해지는 것이 낫다.(들여쓰기로 구분)

### 1.2. if ~ else문
- if문과 마찬가지로 if절 또는 else 절에 속한 문장이 하나일 경우 중괄호 생략 가능

### 1.3. if ~ else if ~ else 문
- else if 절, 중간에 얼마든지 추가 가능

### 1.4. if ~ else문과 유사한 성격의 조건 연산자(3항 연산자)
![image](https://user-images.githubusercontent.com/106478906/230704382-b1a50be8-02ff-4752-b5e4-861036f59804.png)
- 값이 와야하는 위치에 상수나 변수만 써야 하는 것이 아니라, 값을 반환하는 연산도 올 수 있다.

## 2. switch와 break

### 2.1. switch문의 기본 구성
- case와 default는 레이블
-> 실행 위치를 표시하는 용도로 사용된다.
- default : 해당하는 case 없으면 실행
- cf. switch문은 들어가는 문장들이 많기 때문에 대부분 중괄호를 사용한다.
- cf. case는 레이블이라는 상징적 의미로 들여쓰기를 하지 않는다.

### 2.2. switch문 + break문
- break문이 실행되면 switch문을 빠져나간다.

![image](https://user-images.githubusercontent.com/106478906/230704932-b177a197-7065-43cd-8cfa-ba229b585171.png)

-> 한 페이지에 여러 개의 인덱스를 붙여놓는 것과 같다.

## 3. for, while 그리고 do~while 
- 서로 바꿔보는 연습 하기
- 반복 
  - 횟수 : for
  - 만족 : while

### 3.1. while문과 do ~ while문의 차이
- while문은 조건 검사를 먼저하고 실행, do ~ while문은 일단 실행하고 조건 검사
![image](https://user-images.githubusercontent.com/106478906/230707171-be9773cf-37a5-4eb8-9067-dc41872bff1a.png)

![image](https://user-images.githubusercontent.com/106478906/230709199-d88c3e22-9553-431a-92ee-5fbb94c4c131.png)
- 1번 시작하고 2-3-4 삼각형 반복된다고 생각하면 쉬움

## 4. break & continue 
![image](https://user-images.githubusercontent.com/106478906/230709635-7dce3a06-6ba1-4d05-aec5-5e976a7e74e4.png)

- break : 빠져나가라
- continue : 계속은 계속인데 위에서부터 계속
  - 남은 거 생략하고 위에부터 다시 시작한다

### 4.1. 무한루프
~~~java
  for( ; ; ) {
      ....
  }
~~~
~~~java
  while(true){
      ....
  }
~~~
~~~java
  do{
      ....
  } while(true)
~~~
- 특정 조건이 만족되었을 때 반복문을 벗어나려면 break문을 실행하면 된다.

## 5. 반복문의 중첩
![image](https://user-images.githubusercontent.com/106478906/230723370-b7414b69-2b9e-488a-af3a-aa828534cf8a.png)
- for문 중첩이 가장 중요
![image](https://user-images.githubusercontent.com/106478906/230726318-11daef6d-9e44-4207-abff-90d4048132d9.png)

# Chapter 06

## 1. 메소드에 대한 이해와 메소드의 정의
- 메소드 = 기능 상자
- 클래스에 여러 기능 상자를 담음

### 1.1. main 메소드
- 자바에서 정한 규칙: 프로그램의 시작은 main에서부터

### 1.2. 매개변수 0개, 2개인 메소드
- 자바의 기능상자는 입/출력이 있을수도 있고 없을수도 있다.
- 매개변수가 없는 메소드의 정의
~~~java
  public static void byEveryone(){
      System.out.println("다음에 뵙겠습니다.");
  }
~~~

### 1.3. 값을 반환하는 메소드
- void: 값을 반환하지 않음을 의미
- return: 값의 반환을 명령
  - 메소드를 호출한 영역으로 전달
  - 메소드 호출문을 그 결과로 대체한다
![image](https://user-images.githubusercontent.com/106478906/230756291-56bb33e6-61bc-4d81-849a-98247addb9c1.png)
- 반환하는 값과 자료형을 일치시켜야 한다.(jvm에게 반환할 자료에 대한 정보 알려주는 것)

### 1.4. return의 두 가지 의미
1) 메소드를 호출한 영역으로 값을 반환
2) 메소드의 종료

## 2. 변수의 스코프  
- 지역 변수 : 지역은 중괄호 안을 의미
![image](https://user-images.githubusercontent.com/106478906/230757112-5e38b416-d845-4aa3-b2e9-56c7bc40279b.png)

-> for문 내에서 유효한 지역변수 num
- 매개 변수 : 지역변수의 범주에 포함된다
  - 속한 영역을 벗어나면 지역변수 소멸
  
### 2.1. 지역변수 선언의 예
- 같은 영역 내에서 동일 이름의 변수 선언 불가

## 3. 메소드의 재귀 호출
- 돌아간다고 생각하지 말고, 사본 메소드를 만들어놓고 그걸 호출한다고 생각하면 쉬움
![image](https://user-images.githubusercontent.com/106478906/230758142-332fec66-772c-4f1a-877e-1d79e4a0ef68.png)
![image](https://user-images.githubusercontent.com/106478906/230758419-4a6f28e3-d916-4413-aac0-1e9a49b4c02b.png)

-> 3단계에서 1이 2단계로 반환되고 2단계에서 2가 1단계로 반환되어 결과가 3*2 = 6 이다.

# Chapter 07

## 1.클래스의 정의와 인스턴스의 생성

### 1.1. 프로그램의 기본 구성
- 클래스는 연관된 데이터와 메소드를 묶는다.
- 하나의 클래스를 만든다는 것은 틀을 만든다는 것이고, 그 자체로 기능을 가진 것은 아니다.
- 그 틀을 기반으로 인스턴스를 만들어내야 실제로 변수도 존재하게 되고 메소드도 호출 가능하게 되는 것이다.

### 1.2. 클래스 = 데이터 + 기능
- new ~ : 인스턴스를 만들어라.
![image](https://user-images.githubusercontent.com/106478906/230759863-c67de628-ab01-44c1-85ee-5b15fe432e27.png)

-> BackAccount라는 틀을 이용해서 인스턴스를 만들어라.

### 1.3. 인스턴스와 참조변수
- 참조 변수 : 인스턴스의 정보를 갖기 위해 필요한 것
  - 인스턴스가 생성될 때 반환되는 주소값을 저장하기 위한 변수
  - 이 참조 변수를 통해서 우리가 호출하고자 하는 메소드(접근하고자 하는 인스턴스)를 결정할 수 있다.
  
### 1.4. 참조변수의 특성
1) 참조변수는 참조하는 인스턴스를 바꿀 수 있다.
2) 서로 다른 참조변수가 같은 인스턴스를 참조할 수 있다. 

### 1.5. 참조변수의 매개변수 선언
![image](https://user-images.githubusercontent.com/106478906/230762260-d1ac9428-1acd-43a8-aefb-0d8fbad6ba80.png)

-> 참조변수 ref 가 참조하는 인스턴스의 주소 값을 참조변수 acc에 전달하는 것
- 주소 값 = 참조 값

### 1.6. 참조변수에 null 대입
- null은 청소부
~~~java
  ref = null; // ref가 참조하는 인스턴스와의 관계를 끊음
  if(ref == null) // ref가 참조하는 인스턴스가 없다면
~~~

## 2. 생성자(Constructor)와 String 클래스의 소개 

### 2.1. String 클래스에 대한 첫 소개
~~~java
  public static void main(String[] args) {
    String str1 = "Happy";
    String str2 = "Birthday";
    System.out.println(str1 + " " + str2);
    
    printString(str1);
    printString(str2);
}
~~~
- 문자열을 메소드의 인자로 전달할 수 있다.
- 코드상에서의 문자열 표현은 String 인스턴스의 생성으로 이어진다.
- String형 참조변수로 문자열을 참조할 수 있다.
~~~java
public static void printString(String str) {
System.out.print(str);
}
~~~
- 매개변수로 String형 참조변수를 선언하여 문자열을 인자로 전달받을 수 있다.
- String형 참조변수이니까 매개변수도 String형으로 선언한다.

### 2.2. 클래스 정의 모델: 인스턴스 구분에 필요한 정보를 갖게 하자.
![image](https://user-images.githubusercontent.com/106478906/230775596-c832a9be-6f6b-4147-bd17-3a5da1cb0e16.png)

### 2.3. 좋은 클래스 정의 후보를 위한 초기화 메소드
![image](https://user-images.githubusercontent.com/106478906/230776013-b3a54c4a-631a-4aab-8012-20552367d320.png)

### 2.4. 초기화 메소드를 대신하는 생성자
1) 생성자의 이름은 클래스의 이름과 동일해야 한다.
2) 생성자는 값을 반환하지 않고 반환형도 표시하지 않는다.

### 2.5. 디폴트 생성자
- 컴파일러에 의해 자동 삽입되는 '디폴트 생성자’
- 무늬만 생성자
- 하지만, 모든 클래스는 기본적으로 생성자를 직접 정의하는 것이 의미가 있다.

## 3. 자바의 이름 규칙(Naming Rule)  

### 3.1. 클래스의 이름 규칙
1) 클래스 이름의 첫 문자는 대문자로 시작한다.
2) 둘 이상의 단어가 묶여서 하나의 이름을 이룰 때, 새로 시작하는 단어는 대문자로 한다.
~~~java
  ex) Circle + Point = CirclePoint  
~~~
- Camel Case(낙타등) 모델

## 3.2. 메소드와 변수의 이름 규칙
1) 메소드 및 변수 이름의 첫 문자는 소문자로 시작한다.
2) 둘 이상의 단어가 묶여서 하나의 이름을 이룰 때, 새로 시작하는 단어는 대문자로 한다.

~~~java
  ex) Add + Your + Money = addYourMoney
      Your + Age = yourAge
~~~
- 변형된 Camel Case 모델

### 3.3. 상수의 이름 규칙
1) 상수의 이름은 모든 문자를 대문자로 구성한다.
2) 둘 이상의 단어가 묶여서 하나의 이름을 이룰 때 단어 사이를 언더바로 연결한다.

~~~java
  ex) final int COLOR_RAINBOW = 7;
~~~

# Chapter 08

## 1. 클래스 패스(Class Path)
- 클래스 패스를 지정하면 다양한 경로에서 JVM 혹은 자바 가상 런처가 클래스 파일을 찾도록 유도할 수 있다.

### 1.1. 현재 디렉토리에 대한 이해
- 현재 디렉토리 : 실행 중인 프로그램의 작업 디렉토리
- 현재 디렉토리 C:\PackageStudy를 기준으로 자바 파일을 찾는다.

![image](https://user-images.githubusercontent.com/106478906/230837718-09164552-4d18-446e-99db-86383e22b919.png)

-> 클래스 패스에 MyClass만 추가시키면, 경로를 바꿀 필요도 없고 실행 방법을 바꿀 필요도 없다.

### 1.2. 클래스 패스란?
- 클래스 패스: 자바 가상머신의 클래스 탐색 경로
- 고정시키는 것보다는 필요할 때마다 설정하는 것이 좋다.(프로그램의 실행이라는 것은 유동적이기 때문)
![image](https://user-images.githubusercontent.com/106478906/230838843-137f9660-cebd-40b1-bc80-6a597acc09b3.png)

-> '.' 은 현재 디렉토리를 의미한다.(여전히 이 경로(C:\PackageStudy)에서 클래스 파일을 찾도록 하기 위해서)
-> ';' 을 찍고 원하는 만큼의 클래스를 추가할 수 있다.

![image](https://user-images.githubusercontent.com/106478906/230844357-c426c589-738d-4d1c-a30a-e4bb67d8bb47.png)

-> 상대경로는 현재 디렉토리가 어디냐에 따라서 실제 의미하는 경로가 달라진다.
-> cf. 실무 개발에서는 절대 경로 쓰지 않는다.(설치 경로를 사람마다 다르게 설정하는데, 절대 경로로 지정해버리면 무조건 거기에다가 넣어야 한다.)

### 1.3. 클래스 패스를 고정시키는 방법

- 변수의 이름으로 classpath, 변수 값으로 경로 정보 전달하면 클래스 패스가 시스템 전체에 적용이 된다.
- But! 좋은 방법이 아니므로, 이렇듯 클래스 패스를 고정시키는 일이 가능하다는 사실 정도만 알고 있자.

## 2. 패키지의 이해
- cf. 실무에서는 기업에서 제공하는 클래스 묶음을 구매해와서 사용하는 경우가 많다.

### 2.1. 패키지 선언이 필요한 상황
1) 공간에서의 충돌
- 동일 이름의 클래스 파일을 같은 위치에 둘 수 없다.(경로)
2) 접근 방법에서의 충돌
- 인스턴스 생성 방법에서 두 클래스에 차이가 없다.

### 2.2. 공간적, 접근적 충돌 해결을 위한 패키지 선언
- 패키지 선언이라는 것은 그 클래스 파일이 있어야 할 곳을 강제하는 것이다.
1) 클래스 접근 방법의 구분
- 서로 다른 패키지의 두 클래스는 인스턴스 생성 시 사용하는 이름이 다르다.
2) 클래스의 공간적인 구분
- 서로 다른 패키지의 두 클래스 파일은 저장되는 위치가 다르다.
- 컴파일 과정에서, 클래스 파일이 저장되어야 하는 위치는 상대적으로 결정이 된다.
그리고 이렇게 결정된 위치는 컴파일 이후에 바꿀 수 없다.

### 2.3. 패키지 선언에 따른 문제 해결
- 패키지 이름은 모두 소문자로 구성
- 인터넷 도메인 이름의 역순으로 이름을 구성
- 이름 끝에 클래스를 정의한 주체 또는 팀의 이름 추가
![image](https://user-images.githubusercontent.com/106478906/230854329-db06d700-6133-4754-9865-2ec078bdff9d.png)

-> 패키지 선언을 했을 경우, JVM은 클래스 패스를 기준으로 com이라는 디렉토리를 찾게 된다.

### 2.4. 패키지 선언이 된 소스파일 컴파일 방법
![image](https://user-images.githubusercontent.com/106478906/230854702-deb5be17-dcb1-4c12-a3c4-ba47ceda836e.png)

- -d 옵션을 주고 컴파일 하면 패키지 디렉토리도 자동 생성
- '-d' 옵션 : 패키지에서 명시하는대로 컴파일, 경로 생성, 클래스 파일을 넣어 놔라.
- '.' : 현재 directory 기준

### 2.5. 클래스 하나에 대한 import 선언
~~~java
  import com.wxfx.smart.Circle;
  import com.fxmx.simple.Circle;
~~~
- 동일 이름의 두 클래스에 대한 import 선언은 컴파일 오류
- cf. import선언은 제한적으로 써야 한다고 하는데, 실제로는 많이 쓰인다.

### 2.6. 패키지 전체에 대한 import 선언
~~~java
  import com.wxfx.smart.*;
~~~
- com.wxfx.smart 패키지로 묶인 전체 클래스에 대한 패키지 선언
-> 이름 충돌 발생 가능성 때문에 대부분 쓰지 않는다.

# Chapter 09

## 1. 정보 은닉 (Information Hiding)
- 클래스에는 데이터, 기능이 있는데 데이터를 숨기고 기능으로 접근하게끔 하는 것이다.
- 은닉의 주체는 클래스
- 클래스 외부에서 데이터에 직접적 접근 못하게 하는 것이다.

### 1.1. 정보를 은닉해야 하는 이유
![image](https://user-images.githubusercontent.com/106478906/230881572-37954a0f-bcc2-41c5-bb81-bbc142243a7e.png)

- 논리적 오류가 생겨도 컴파일 오류가 발생하지 않는다.
-> 정보 은닉을 통해 논리적 오류를 문법적 오류로 바꾸어 컴파일 오류가 발생하게끔 해야 한다.

### 1.2. 정보의 은닉을 위한 private 선언
- Private 선언을 하면 정보를 은닉 할 수 있다.

## 2. 접근 수준 지시자 (Access-level Modifiers)

### 2.1. 네 가지 종류의 접근 수준 지시자

> public > protected > default > private
- 보통 인스턴스 변수는 private, 인스턴스 변수에 접근하기 위한 메소드들은 public으로 선언한다.
- private을 기준으로 두고 private보다 한 군데 허용하는 것이 default이고, 두 군데 허용하는 것이 protected라고 생각하면 쉽다.

![image](https://user-images.githubusercontent.com/106478906/230884720-7b60a12d-d082-4bad-82a5-00393e6fcdfb.png)
- public으로 선언한 클래스는 소스 파일의 이름을 클래스 이름과 같게 해야한다.
왜냐하면 외부에 노출할 클래스이므로, 그 소스 파일안에 어떤 내용이 있는지를 명확히 알 수 있기 때문이다.
-> 하나의 소스파일에 둘 이상의 public 클래스가 들어오면 이 규칙을 만족시키지 못하므로 불가능하다.

### 2.2. 클래스의 public, default 선언 관련 예
- 소스파일이 나눠져 있어도 패키지명이 같으면 동일 패키지로 묶였다고 간주할 수 있다.
- 따라서 패키지명을 같게 바꾸면 default로 선언한 클래스도 오류가 나지 않는다.

### 2.3. 상속에 대한 약간의 설명: protected 선언의 의미 이해를 위한
![image](https://user-images.githubusercontent.com/106478906/230888077-1b57788f-6a34-4d0b-a002-24814a6786f3.png)

- 디폴트 패키지는 패키지 선언이 되어 있지 않은 클래스들을 하나의 패키지로 묶기 위한 개념이다.
  - code레벨에서 내/외부 접근을 생각해야하며, 인스턴스 레벨에서 보면 안된다.
  - 상속관계는 외부이지만, 디폴트 패키지로 묶여있기 때문에 접근을 허용해주는 것이다.

### 2.4. 인스턴스 멤버의 protected 선언이 갖는 의미
![image](https://user-images.githubusercontent.com/106478906/230888280-3a4c131a-65b3-4539-abd8-aac9b4927747.png)
- protected 선언으로 인해 동일 패키지로 묶여있지 않아도 상속 관계에서 접근 가능하다.

### 2.5. 인스턴스 멤버 대상 접근 수준 지시자 정리
![image](https://user-images.githubusercontent.com/106478906/230888660-6aec4b05-336a-4f5f-9bda-3d8ece39d617.png)

## 3. 캡슐화 (Encapsulation)

### 3.1. 포함 관계로 캡슐화 완성하기
![image](https://user-images.githubusercontent.com/106478906/230894917-f6f2484e-725b-410e-bd1c-3889a37a7329.png)

- 클래스간에 가장 많이 갖는 관계

# Chapter 10

## 1. static 선언을 붙여서 선언하는 클래스 변수 

- 전체 프로그램에서 하나의 변수를 선언해서 전체 프로그램에서 모두 공유하고 싶을 때
- 클래스 변수 : static선언을 함으로써 하나만 존재하고, 어디서나 접근 가능한 변수
  - 인스턴스 변수는 인스턴스의 생성했을 때 존재한다는 의미, 클래스 변수는 위치는 인스턴스 내에 존재하지만 인스턴스 변수가 아니라 클래스에 위치하는 변수다.
- cf. static 변수라고 많이 부름

### 1.1. 선언된 클래스의 모든 인스턴스가 공유하는 클래스 변수
- static이 붙을 경우, 속한 클래스와 관계없다
  - 속한 클래스에서 지시하는 접근 수준 지시자의 규칙을 따라야 한다.
  - 속한 클래스가 클래스 변수에게 자리를 빌려 주었으니, 클래스 변수에 직접 접근을 할 수 있는 권한을 획득하겠다.
  - 클래스 변수는 인스턴스 생성과 상관없이 특정한 메모리 공간에 별도로 저장한다.

### 1.2. 클래스 변수의 접근 방법
- 클래스 내부 접근
  - static 변수가 선언된 클래스 내에서는 이름만으로 직접 접근 가능
- 클래스 외부 접근
  - private으로 선언되지 않으면 클래스 외부에서도 접근 가능
  - 접근 수준 지시자가 허용하는 범위에서 접근 가능
  - 클래스 또는 인스턴스의 이름을 통해 접근

![image](https://user-images.githubusercontent.com/106478906/230903280-fba16d82-b3fc-4a2e-b0ca-9b06ce7a97ee.png)

->num이라는 변수가 인스턴스 변수인지 클래스 변수인지 분간이 안되기 때문에 인스턴스 이름보다는 클래스 이름으로 접근하는 것이 권장된다.
  
### 1.3. 클래스 변수의 초기화 시점과 초기화 방법
- 클래스 변수는 생성자 기반으로 초기화 하면 안된다. 이 경우 인스턴스 생성시마다 값이 리셋된다.
- 초기화 시점 : JVM에 읽혀들어갈 때  
  
### 1.4. 클래스 변수의 활용의 예
~~~java
  class Circle {
    static final double PI = 3.1415;
    private double radius;
    Circle(double rad) {
    radius = rad;
    }
    void showPerimeter() {
    double peri = (radius * 2) * PI;
    System.out.println("둘레: " + peri);
    }
    void showArea() {
    double area = (radius * radius) * PI;
    System.out.println("넓이: " + area);
    }
  }
~~~
- 인스턴스 별로 가지고 있을 필요가 없는 변수
  - 값의 참조가 목적인 변수
  - 값의 공유가 목적인 변수
- 그리고 그 값이 외부에서도 참조하는 값이라면 public으로 선언한다.

## 2. static 선언을 붙여서 정의하는 클래스 메소드
- 클래스 메소드의 성격 및 접근 방법이 클래스 변수와 동일하다.

### 2.1. 클래스 메소드로 정의하는 것이 옳은 경우
- 단순 기능 제공이 목적인 메소드들, 인스턴스 변수와 관련 지을 이유가 없는 메소드들은static으로 선언하는 것이 옳다.

![image](https://user-images.githubusercontent.com/106478906/230907754-4102a579-be33-41ed-afe1-54e817085f58.png)
- 유효하지 않은 이유
1) addNum이라는 클래스 메소드는 인스턴스 변수들과 별도로 저장되어 있다.
2) 된다고 쳐도, 여러 개의 num 변수가 있을 수 있으므로 어떤 num을 증가시킬 지 모른다.

## 3. System.out.println() 그리고 public static void main() 
- System.out.println()
  - System : 클래스 이름
  - out : 클래스 변수(뒤에 .을 찍었다는 것은 참조변수임을 의미)
  - println : 인스턴스
- public static void main() 
  - public : 약속(명령 프롬프트, 이클립스 등 외부 툴에서 메인 메소드를 호출하므로 요청 자체가 클래스 외부에서 이루어진다.)
  - static : main메소드는 하나만 존재해야 한다.
  - void : 반환 x
  
### 3.1. System.out.println()에서 out과 println의 정체는?
~~~java
  java.lang.System.out.println(...);
~~~
- System은 java.lang 패키지에 묶여 있는 클래스의 이름
- 그러나 컴파일러가 다음 문장을 삽입해 주므로 java.lang을 생략할 수 있다.
- import java.lang.*;
~~~java
  System.out.println(...)
~~~
- out은 클래스 System의 이름을 통해 접근하므로,
- 이는 System 클래스의 클래스 변수 이름임을 유추할 수 있다.
~~~java
  System.out.println(...);
~~~
- println은 out이 참조하는 인스턴스의 메소드이다.

### 3.2. main 메소드가 public이고 static인 이유는?
~~~java
  public static void main(String[] args) {...}
~~~
- static인 이유! 인스턴스 생성과 관계없이 제일 먼저 호출되는 메소드이다.
~~~java
  public static void main(String[] args) {...}
~~~
- public인 이유! main 메소드의 호출 명령은 외부로부터 시작되는 명령이다.
단순히 일종의 약속으로 이해해도 괜찮다.

### 3.3. main 메소드를 어디에 위치시킬 것인가?
- main 메소드를 위한 클래스를 생성하는 것이 보편적이다.
- 어디에 넣어도 상관 없음 단, 실행 방법이 달라진다.

## 4. 또 다른 용도의 static 선언 

### 4.1. static 초기화 블록
- 값을 얻어올 때 static 변수를 초기화 하기 위해서 쓰는 것이다.

### 4.2. static import 선언
![image](https://user-images.githubusercontent.com/106478906/230918111-9337cd80-4cb1-4d5f-bdd2-05c58bdebf2f.png)

-> 밑처럼 쓸 수 있긴 하지만 출처를 명확하게 밝혀주는 표현이 좋기 때문에 위의 방식을 추천한다.
-> static 변수도 import할 수 있다는 사실은 알아두기.

# Chapter 11 

## 1. 메소드 오버로딩 (Method Overloading)

### 1.1. 메소드 오버로딩
: 호출된 메소드를 찾을 때 참조하게 되는 두 가지 정보
1) 메소드의 이름
2) 메소드의 매개변수 정보

- 따라서 이 둘 중 하나의 형태가 다른 메소드를 정의하는 것이 가능하다.
~~~java
  class MyHome {
    void mySimpleRoom(int n) {...}
    void mySimpleRoom(int n1, int n2) {...}
    void mySimpleRoom(double d1, double d2) {...}
  }
~~~
- 메소드의 이름이 같아도 호출하는 매개변수의 정보가 달라지면 구분이 가능하다.

### 1.2. 메소드 오버로딩의 예
![image](https://user-images.githubusercontent.com/106478906/231054837-1e7a4ffc-0f4b-4712-91bf-f6dfcc22915d.png)

- 매개변수의 자료형이 다르거나
- 매개변수의 수가 다르거나
- 반환형이 다른 것은 메소드 오버로딩의 조건이 아니다.

### 1.3. 오버로딩 관련 피해야할 애매한 상황

![image](https://user-images.githubusercontent.com/106478906/231055536-9260e06e-780a-4f83-8066-e289ceead5dd.png)

- 첫번째거가 호출된다.
  - 가장 가까이 있는 형변환 규칙을 따르기 때문이다.(int 보다 double이 더 가까움)
  - but, 그 전에 강제 형변환을 해주는 것이 더 좋다.

### 1.4. 생성자의 오버로딩
- 생성자의 오버로딩을 통해 생성되는 인스턴스의 유형을 구분할 수 있다.
ex) 여권이 있는 사람과 없는 사람
ex) 운전 면허증을 보유한 사람과 보유하지 않은 사람

### 1.5. 키워드 this를 이용한 다른 생성자의 호출
- this : 이 인스턴스 

![image](https://user-images.githubusercontent.com/106478906/231059983-d38a0709-4a77-4d00-b9e3-6a24ce0aefb1.png)

-> 생성자가 먼저 호출이 되긴 됐는데 이 생성자 안에서 오버로딩된 다른 생성자를 다시 호출하는 것이다.
- 생성자 안에서만 존재할 수 있고, 이 인스턴스의 다른 생성자를 의미한다.

### 1.6. 키워드 this를 이용한 인스턴스 변수의 접근
- 인스턴스 변수/메소드에 접근할 때 '.'을 찍는다.
- 1.5에서 말한 메소드 호출의 성격 this와 인스턴스 변수/메소드에 접근을 의미하는 this 2가지가 존재한다.

![image](https://user-images.githubusercontent.com/106478906/231061839-e6fe1ac1-43a8-4a19-adb5-75a15f23060a.png)

- 매개 변수 이름과 인스턴스 변수의 이름이 중복될 경우 매개 변수를 우선으로 한다.
  - 하지만 이 안에서도 인스턴스 변수를 쓰기 위해서 this 키워드를 사용하는 것이다.
- this.data는 어느 위치에서 건 인스턴스 변수 data를 의미함

## 2. String 클래스                                 

### 2.1. String 인스턴스 생성의 두 가지 방법
- 우리가 알고 있는 문자열도 스트링 클래스의 인스턴스이다.
![image](https://user-images.githubusercontent.com/106478906/231064713-9a2cd148-a36e-4812-964b-d8facc69c20d.png)

-> 둘 다 String 인스턴스의 생성으로 이어지고 그 결과 인스턴스의 참조 값이 반환된다.

### 2.2. String 인스턴스와 println 메소드
- println 메소드가 다양한 인자를 전달받을 수 있는 이유는 메소드 오버로딩 때문이다.
~~~java
  System.out.println("str");
~~~
- JVM이 String 인스턴스 생성하고, 문자열 정보를 저장하고 인스턴스의 참조값을 반환한다.

### 2.3. String 인스턴스는 Immutable 인스턴스
- Immutable 인스턴스 : 가지고 있는 데이터의 변경을 허용하지 않는다.
- 바뀌지 않는 데이터를 참조하는 게 다이기 때문에, 다른 인스턴스 변수가 동시에 참조해도 문제가 생기지 않는다.

### 2.4. String 인스턴스 기반 switch문 구성

![image](https://user-images.githubusercontent.com/106478906/231067658-03a18efe-fe78-4af1-8d85-4c5e31bd2504.png)

-> 이렇게도 구성 가능하다고 알아두기.

## 3. String 클래스의 메소드
- String 인스턴스는 Immutable 인스턴스이므로, 저장된 문자열의 값을 바꾸지 못한다. 
  - 따라서 문자열 반환하는 메소드들은 새 문자열을 생성하는 것을 의미한다.

### 3.1. 문자열 연결시키기
- concat
![image](https://user-images.githubusercontent.com/106478906/231073321-5e39b95d-eca9-46c7-b9d4-4148506e649d.png)

### 3.2. 문자열의 일부 추출
- substring
- 인덱스 : 0을 기준으로 얼마나 떨어져있느냐
~~~java
  String str = "abcdefg";
  str.substring(2);
~~~
-> 인덱스 2 이후의 내용으로 이뤄진 문자열 "cdefg" 반환
~~~java
  String str = "abcdefg";
  str.substring(2, 4);
~~~
-> 인덱스 2 ~ 3에 위치한 내용의 문자열 반환(4까지가 아니라 4 앞까지)

### 3.3 문자열의 내용 비교
- equals
  - 내용이 같으면 true
- compareTo
  - 내용이 같으면 0
  - cmp = st1.compareTo(st2); 일때 stl이 사전편찬 순서상 앞에 오면 0보다 작은 값, 뒤에오면 0보다 큰 값을 반환한다.
- compareToIgnoreCase
  - 대소문자의 구분 하지 않는다.

### 3.4. 기본 자료형의 값을 문자열로 바꾸기
- valueOf
~~~java
  double e = 2.718281;
  String se = String.valueOf(e);
~~~
  - String 인스턴스 "2.718281"를 생성해서 참조값을 반환한다.
  - 호출할 때 인스턴스 생성하고 호출하는 게 아니라 String 클래스의 이름을 대상으로 valueOf를 호출하면 값의 내용을 담고있는 문자열을 얻을 수 있다.

### 3.5. 문자열 대상 + 연산과 += 연산
- '+' 연산
~~~java
  System.out.println("funny" + "camp");
           ↓
  System.out.println("funny".concat("camp"));
~~~
-> 원래 참조값들끼리는 연산 불가한데, 컴파일러에 의해 concat으로 자동 변환되어 연산이 가능해지는 것이다.

- '+=' 연산
~~~java
  String str = "funny";
  str += "camp"; // str = str + "camp"
        ↓
  str = str.concat("camp")
~~~

### 3.6. 문자열과 기본 자료형의 + 연산
![image](https://user-images.githubusercontent.com/106478906/231082338-da3ac750-2da8-4ab2-a223-78bb57e5295b.png)

### 3.7. concat 메소드는 이어서 호출 가능
~~~java
  String str = "AB".concat("CD").concat("EF");
  → String str = ("AB".concat("CD")).concat("EF");
  → String str = "ABCD".concat("EF");
  → String str = "ABCDEF";
~~~

### 3.8. 문자열 결합의 최적화를 하지 않을 경우
![image](https://user-images.githubusercontent.com/106478906/231084030-ea3de4d4-1b28-4379-b386-985d7d8740be.png)

### 3.9. 문자열 결합의 최적화를 진행 할 경우
![image](https://user-images.githubusercontent.com/106478906/231085144-a840eebf-e050-4724-a748-8fa358d3e848.png)
- toString메소드가 호출될 때 가지고 있는 내용을 한번에 문자열 인스턴스로 만든다.
1) StringBuilder
2) "<양>"
3) toString() 
-> 총 3개의 String 인스턴스 생성

### 3.10. StringBuilder
![image](https://user-images.githubusercontent.com/106478906/231087373-931dd2b3-5cf5-4a99-911e-ead5efef5f1e.png)

### 3.11. StringBuffer
![image](https://user-images.githubusercontent.com/106478906/231088950-8c32426a-d91c-4528-8584-83ea92f9f00b.png)

# Chapter 12

## 1. 콘솔 출력 (Console Output)
- 콘솔 : 컴퓨터로 데이터를 입력,확인하는 장치이다.
  - ex) 키보드, 모니터, 마우스

### 1.1. toString 메소드
- StringBuilder와의 공통점
  1. 메소드의 이름
  2. 인자를 전달받지 않는다.
  3. 반환형이 String이다.

~~~java
class Box {
  private String conts;
  
  Box(String cont) {
    this.conts = cont;
  }
  public String toString() {
    return conts; // 문자열 반환
  }
}

public static void main(String[] args) {
  StringBuilder stb = new StringBuilder("12");
  stb.append(34);
  System.out.println(stb.toString());
  System.out.println(stb);
  Box box = new Box("Camera");
  System.out.println(box.toString());
  System.out.println(box);
}
~~~
- stb라는 참조 변수가 참조하고 있는 인스턴스는 StringBuilder이다.
- 이 참조값을 바탕으로 참조값이 가리키는 인스턴스의 toString메소드를 호출한다.
- 이때 반환되는 문자열을 println 메소드가 출력한다.(print 메소드도 마찬가지)
- 자바에서 정의하는 모든 클래스는 toString 메소드를 가지고 있다.
  - 내가 정의를 하지 않아도 존재한다.

### 1.2. 문자열의 조합 printf 메소드
- printf 메소드 : 문자열의 기본 포맷을 지정하고, 내가 원하는 데이터를 원하는 형태로 출력하도록 해준다.
- 첫번째 인자로 무조건 문자열이 전달되어야 한다.
- 서식 지정자 = 틀
![image](https://user-images.githubusercontent.com/106478906/231747241-5080c91e-c5d8-47f6-b21a-9df2266d79c0.png)
  - %g : 간단한 실수는 그냥 표기하는 것이 낫고, 복잡한 실수는 지수(e 표기법)로 표현하는 것이 낫기 때문에 그것을 알아서 결정해줘라.

## 2. 콘솔 입력 (Console Input)   

### 2.1. Scanner 클래스
- 데이터를 스캔하는 클래스이다.
- Scanner 클래스의 인스턴스 생성은 데이터를 뽑아 올 대상과의 연결을 의미한다. 연결 후에는 데이터 스캔이 가능하다.

### 2.2. Scanner 클래스의 키보드 적용
![image](https://user-images.githubusercontent.com/106478906/231755654-eac62f21-56d9-4c2a-b37d-58c370d124ec.png)

- System.in이 참조하고 있는 인스턴스에 키보드 정보가 있어서, Scanner 인스턴스가 키보드와 연결을 시도해서 성공한다.
- nextInt 메소드를 호출 : 정수를 하나 읽어들이겠다.
  - 키보드로부터 입력된 데이터가 없으니 대기 상태가 된다.(콘솔에서의 입력을 기다린다)
  - 입력하고 엔터치면 입력의 완료를 의미한다.
  - 입력된 데이터(숫자)는 스캐너 클래스로 읽혀지고, 스캐너 클래스는 입력된 데이터를 반환한다. 
- cf. Scanner 인스턴스 생성 이후에 데이터를 스캔하는 방법에 있어서는 차이가 없다. 즉 연결 대상에 의존적이지 않은 코드의 작성이 가능하다.

# Chapter 13

## 1. 1차원 배열의 이해와 활용Ⅰ
- 배열 : 동일한 자료형의 둘 이상의 변수를 나란히 할당한 것이다.

### 1.1. 1차원 배열의 이해와 선언 방법
- 1차원 배열 : 타입이 같은 둘 이상의 데이터를 저장할 수 있는 1차원 구조의 메모리 공간이다.
  - 일렬로 나란히 할당된 변수들의 모임이다.
- 1차원 배열의 선언 방법
~~~java
  int[] ref = new int[5]; // 길이가 5인 int형 1차원 배열의 생성문
~~~
-> =을 기준으로 오른쪽은 배열 생성, 왼쪽은 배열을 참조할 수 있는 참조변수 선언
-> ref는 int형 배열을 참조할 수 있는 참조변수이다.
-> int형 변수 5개로 이루어져있는 배열을 생성해라.
=> int형 변수 5개를 저장할 수 있는 메모리 공간의 묶음(배열)이 만들어지고, 이 배열의 참조값이 반환되어서 ref라는 참조변수가 이 배열을 참조하게 된다. 
- 길이 정보는 참조변수 선언에 영향을 미치지 않는다.


### 1.2. 배열 선언문에 대한 세세한 이해와 결과
- new는 인스턴스의 생성을 명령하는 것이므로, 배열도 인스턴스이다.
![image](https://user-images.githubusercontent.com/106478906/231772554-be96e449-f046-45fa-9cd5-97ba917b875b.png)

-> 배열이 인스턴스 안에 존재한다.
- 멤버 변수 length는 배열의 길이 정보 저장
~~~java
public static void main(String[] args) {
  int[] ref;
  ref = new int[5];
  ....
}
~~~
-> 배열의 참조변수와 인스턴스의 선언도 분리 가능하다.

### 1.3. 1차원 배열의 예
~~~java
public static void main(String[] args) {
  // 길이가 5인 int형 1차원 배열의 생성
  int[] ar1 = new int[5];
  
  // 길이가 7인 double형 1차원 배열의 생성
  double[] ar2 = new double[7];
  
  // 배열의 참조변수와 인스턴스 생성 분리
  float[] ar3;
  ar3 = new float[9];
  
  // 배열의 인스턴스 변수 접근
  System.out.println("배열 ar1 길이: " + ar1.length);
  System.out.println("배열 ar2 길이: " + ar2.length);
  System.out.println("배열 ar3 길이: " + ar3.length);
}
~~~
![image](https://user-images.githubusercontent.com/106478906/231774220-bd7ee4b6-ba09-4e86-957b-44eb9d2b5844.png)

-> ar1.length 이렇게 . 찍고 접근한다는 것은 length가 인스턴수 변수임과, 배열이 인스턴스임을 증명한다.

### 1.4. 인스턴스 대상 1차원 배열의 예
![image](https://user-images.githubusercontent.com/106478906/231776180-576b524e-5b7a-4a83-b503-13cdb5ecc7bf.png)

-> 앞에서 소개한 기본 자료형 배열 이외에도, 우리가 정의하는 클래스의 인스턴스를 대상으로도 배열을 선언할 수 있다.

## 2. 1차원 배열의 이해와 활용 Ⅱ

### 2.1. 배열 기반 반복문 활용의 예
- 배열 요소는 반복문을 통해 순차적 접근이 가능하며, 이것은 배열이 가진 큰 장점 중 하나이다.

## 3. 1차원 배열의 이해와 활용 Ⅲ

### 3.1. 배열을 생성과 동시에 초기화
![image](https://user-images.githubusercontent.com/106478906/231972381-c1d3de4d-a6bf-46f9-80c2-3266d27b49d8.png)

-> 배열 생성만 하면 이렇게 배열의 개수를 정해주는데

![image](https://user-images.githubusercontent.com/106478906/231972952-939dcc05-60e1-4bfd-9624-932ec206177a.png)

-> 배열 생성과 동시에 초기화 하려면 초기화 하고자 하는 값을 {} 안에 넣어주고, [] 안을 비워야 한다.
  - 배열의 길이를 컴파일러가 계산해서 넣어주도록 약속되어 있기 때문이다. 

![image](https://user-images.githubusercontent.com/106478906/231973900-e6b3d3f0-1116-4f99-aa85-c2a62ba4396c.png)

-> {} 앞부분을 생략해도 된다.

### 3.2. 배열 대상 참조변수 선언의 두 가지 방법
![image](https://user-images.githubusercontent.com/106478906/231974887-02dba594-d08e-4ae2-b127-58d9ae8d31cf.png)

-> 가급적이면 위의 방법으로 선언하는게 좋다.

### 3.3. 배열의 참조 값과 메소드
![image](https://user-images.githubusercontent.com/106478906/231976233-fc3c0c3d-5ab7-4d1d-b7e8-022de2af9b69.png)

- 참조변수 선언은 매개 변수 선언 자리에도 올 수 있다.
  - 전달 인자로 int형 배열의 참조값이 전달됨을 의미한다.
- 똑같은 ar이지만 위의 ar은 main 메소드 내에서 유효한 ar이고, 밑의 ar은 
sumOfAry라는 메소드 내에서 유효한 ar이다.
  - 지역이 다르면 이름이 같아도 상관없다.

![image](https://user-images.githubusercontent.com/106478906/231978214-214dda90-6a27-4e2d-8957-5864aa11e4a8.png)
  
-> 배열의 참조 값 반환 가능
  - int[len] 배열을 생성하고 ar이라는 참조변수로 이 인스턴스를 참조하고 있다.
  - ar을 반환하므로 반환값에 int[]이 오는 것이다.
- 결론 : 메소드 생성 위치에 상관없이 참조 값만 있으면 누구나 배열에 접근 가능하고, 참조 값은 주거니 받거니가 가능하다.

## 4. 1차원 배열의 이해와 활용 Ⅳ

### 4.1. 배열의 초기화 메소드
- fill 메소드
  - java.util.Arrays 클래스에 정의되어 있는 메소드, 원하는 값으로 배열 전부 또는 일부를 채울 때 사용하는 메소드
  ~~~java
    public static void fill(int[] a, int val)
  ~~~
  → 두 번째 인자로 전달된 값으로 배열 초기화
  ~~~java
  public static void fill(int[] a, int fromIndex, int toIndex, int val)
  ~~~
  → 인덱스 fromIndex ~ (toIndex-1)의 범위까지 val의 값으로 배열 초기화

### 4.2. 배열 복사 메소드
- arraycopy 메소드
  -  java.lang.System 클래스에 정의되어 있는 메소드, 한 배열에 저장된 값을 다른 배열에 복사할 때 사용하는 메소드
  ~~~java
  public static void
    arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
  ~~~
  → 복사 원본의 위치: 배열 src의 인덱스 srcPos
  → 복사 대상의 위치: 배열 dest의 인덱스 destPos
  → 복사할 요소의 수: length
  
### 4.3. 배열 초기화와 복사의 예
![image](https://user-images.githubusercontent.com/106478906/232010271-9d88bac2-28a9-47b1-ab63-0c1541bfb51b.png)

### 4.4. main의 매개변수로 인자를 전달하는 예

![image](https://user-images.githubusercontent.com/106478906/232018565-6516c13c-1aee-4786-8cd1-f9e4180babd4.png)

-> 배열이 생성되고 arr이 갖고 있는 참조 값이 args에 인자로 전달된다.

## 5. enhanced for문

### 5.1. enhanced for문(for-each문) 의 이해

![image](https://user-images.githubusercontent.com/106478906/232021438-a2626889-ff44-4cb1-acb1-f1ad56ec9952.png)

-> ar이 가진 데이터를 e에 하나씩 넣고 데이터가 끝날때까지 실행한다.

## 6. 다차원 배열의 이해와 활용
![image](https://user-images.githubusercontent.com/106478906/232025969-e87c5037-e878-434f-a3fb-9eaa07da0b78.png)

-> 길이가 4인 1차원 배열 3개가 묶였다.
-> 세로가 3, 가로가 4이다.

### 6.1. 2차원 배열의 실제 구조
![image](https://user-images.githubusercontent.com/106478906/232029225-9f506aac-ef5e-4216-af71-4d9e45572b9b.png)

- 다수의 1차원 배열을 엮어서 구성이 되는 2차원 배열
![image](https://user-images.githubusercontent.com/106478906/232030300-047d5bea-1dc2-4b64-94fa-a582ce1d1d75.png)

-> 2차원 배열은 독립된 1차원 배열의 묶음으로 구현되기 때문에 이런 형태로도 만들 수 있다.

![image](https://user-images.githubusercontent.com/106478906/232030740-7ee32aea-4609-43c1-9fed-b691a637b1ed.png)

- 3개의 1차원 배열이 있고, 순서대로 1/2/3/개의 요소를 저장할 수 있다.
- 이 1차원 배열 3개를 묶는 배열이 만들어지며, 길이는 3이다.
  -> 실제 arr이 가리키는 배열은 배열들을 묶는 배열이다.
- 따라서 arr.length의 값은 3이고 arr[i].length은 1,2,3이 된다.











