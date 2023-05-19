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

>Box<Apple> aBox = new Box<Apple>();
- T를 Apple로 결정하여 인스턴스 생성
- 따라서 Apple 또는 Apple을 상속하는 하위 클래스의 인스턴스 저장 가능

>타입 매개변수 (Type Parameter) 
- Box<T>에서 T
>타입 인자 (Type Argument)
- Box<Apple>에서 Apple
>매개변수화 타입 (Parameterized Type) 
- Box<Apple>
  
  
### 1.3. 제네릭 이후의 코드: 개선된 결과
1. object형으로 반환하지 않기 때문에 형변환 하지 않는다.
2. 자료형을 잘못 입력하는 프로그래머의 실수가 컴파일 단계에서 발견된다.
  
  
  
  
