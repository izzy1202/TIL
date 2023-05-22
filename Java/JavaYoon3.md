# <윤성우의 열혈 Java> 강의 내용 정리
>[강의 링크](https://cafe.naver.com/cstudyjava/135782?boardType=L)

> Chapter 21 ~ Chapter 
> 
>모든 내용을 정리하지는 않음

---

# Chapter 21

## 1. 제네릭의 이해 

### 1.1. 제네릭 이전의 코드
- 명시적 형변환 과정이 필요하다. 그만큼 코드의 안정성이 떨어지고 컴파일러의 오류 발견 가능성을 낮춘다.

cf. 오류 단계
1. 컴파일 과정
2. 실행과정에서 예외로 발견
3. 실행되는데 결과가 이상하다.
- 1단계에서 끝나는게 best

#### 1.1.1. 제네릭 이전 코드가 갖는 문제점
1. 프로그래머의 실수가 컴파일 과정에서 발견되지 않는다.
2. 프로그래머의 실수가 실행 과정에서조차 발견되지 않을 수도 있다. 이건 정말 큰 문제이다.

### 1.2. 제네릭 기반의 클래스 정의하기
> 인스턴스 생성시 결정이 되는 자료형의 정보를 T로 대체한다.

- 인스턴스 생성할 때 필요에 맞게 T를 결정하겠다.
~~~java
class Box<T> {
  private T ob;
  public void set(T o) {
    ob = o;
}
  public T get() {
    return ob;
  }
}
~~~

> Box<Apple> aBox = new Box<Apple>();
- T를 Apple로 결정하여 인스턴스 생성
- 따라서 Apple 또는 Apple을 상속하는 하위 클래스의 인스턴스 저장 가능

> 타입 매개변수 (Type Parameter) 
- Box<T>에서 T
> 타입 인자 (Type Argument)
- Box<Apple>에서 Apple
> 매개변수화 타입 (Parameterized Type) 
- Box<Apple>
  
  
### 1.3. 제네릭 이후의 코드: 개선된 결과
1. object형으로 반환하지 않기 때문에 형변환 하지 않는다.
2. 자료형을 잘못 입력하는 프로그래머의 실수가 컴파일 단계에서 발견된다.

## 2. 제네릭의 기본 문법

### 2.1. 타입 매개변수의 이름 규칙
- 일반적인 관례
  - 한 문자로 이름을 짓는다. 
  - 대문자로 이름을 짓는다.
  
- 보편적인 선택
E Element
K Key
N Number
T Type
V Value
  
### 2.2. 기본 자료형에 대한 제한 그리고 래퍼 클래스
![image](https://github.com/izzy1202/TIL/assets/106478906/6cf39b6b-0472-4573-ae65-77725fdd97f9)

- 오토 박싱, 오토 언박싱으로 기본자료형도 넣을 수 있다.
  
### 2.3. 다이아몬드 기호
> Box<Apple> aBox = new Box<Apple>(); 은 Box<Apple> aBox = new Box<>(); 와 같다.
- 참조변수 선언을 통해서 컴파일러가 사이에 Apple이 와야 함을 유추한다.
- 뒤의 방식을 많이 사용한다.
  
### 2.4. ‘매개변수화 타입’을 ‘타입 인자’로 전달할 수 있다.
~~~java
  Box<Box<String>> wBox = new Box<>();
~~~
  
### 2.5. 제네릭 클래스의 타입 인자 제한하기
> class Box<T extends Number> {...}
- 인스턴스 생성 시 타입 인자로 Number 또는 이를 상속하는 클래스만 올 수 있음
- Number 클래스로 타입 인자를 제한했더니 Number클래스의 메소드를 호출할 수 있는 효과가 생긴다.(이 효과가 타입 인자를 제한하는 실질적인 이유인 경우가 많다.)
  
### 2.6. 제네릭 클래스의 타입 인자를 인터페이스로 제한하기  
~~~java
interface Eatable { public String eat(); }
  
class Apple implements Eatable {
    public String eat() {
    return "It tastes so good!";
    }
  . . . .
}
  
class Box<T extends Eatable> {
  T ob;
  
  public void set(T o) { ob = o; }
    public T get() {
      System.out.println(ob.eat()); // Eatable로 제한하였기에 eat 호출 가능
      return ob;
  }
}
~~~
- 제네릭 클래스의 타입 인자는 인터페이스로도 제한 가능하다.  
  
### 2.7. 하나의 클래스와 하나의 인터페이스에 대해 동시제한
~~~java
  class Box<T extends Number & Eatable> {...}
   //Number는 클래스 이름 Eatable은 인터페이스 이름
~~~ 

  ### 2.8. 제네릭 메소드의 정의
  - 클래스 전부가 아닌 메소드 하나에 대해 제네릭으로 정의 가능하다.
  ![image](https://github.com/izzy1202/TIL/assets/106478906/26590549-f6cb-4f94-962a-4b2c636e61d2)
![image](https://github.com/izzy1202/TIL/assets/106478906/218f6a79-c196-4267-a47a-0da2428d9db8)
-> 전달되는 인자에 따라서 판단 가능하기 때문에 타입 인자 생략 가능하다.

  > 제네릭 클래스와 제네릭 메소드의 차이점
  - 제네릭 클래스는 인스턴스 생성시에 타입이 결정되고 제네릭 메소드는 메소드 호출시에 결정된다.
  
  # Chapter 22
  
  ## 1. 제네릭의 심화 문법

  
  
  
