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
  
  ## 1. 제네릭의 심화 문법 (1)
  ### 1.1. 제네릭 클래스와 상속
![image](https://github.com/izzy1202/TIL/assets/106478906/14c0b73e-6046-4497-a4f2-e2b1728679be)
- 단 SteelBox<Integer>가 Box<String>을 상속하는 형태는 불가능하다.
  
  ### 1.2. 타겟 타입
  ![image](https://github.com/izzy1202/TIL/assets/106478906/7c58f9b6-ff25-4059-b172-86fa60c75910)
- 타겟 타입 : T에 전달되는 자료형을 결정짓기 위한 참조변수 자료형
  
### 1.3. 와일드카드의 설명에 앞서(제네릭 메소드 vs. 일반 메소드)
  ![image](https://github.com/izzy1202/TIL/assets/106478906/ece1079d-c633-4105-9d6d-6b7ee44fc4fd)
- T가 다르면 서로 아무 관련이 없다.
 
  ## 2. 제네릭의 심화 문법 (2)
  ### 2.1. 와일드카드
  ~~~java
  public static void peekBox(Box<?> box) {
    System.out.println(box);
  }
  ~~~
  - Box<Integer>의 인스턴스, Box<String>의 인스턴스를 인자로 전달 가능
  - 제네릭 메소드와 인자로 무엇이든 전달받을 수 있다는 점에서 기능적으로는 같다.
    - 그러나 와일드카드 기반 메소드 정의가 더 간결하므로 우선시 해야 한다고 권고하고 있다. 메소드의 정의가 복잡해질수록 와일드카드 기반 메소드 정의가 더 간결해 보인다.
  
  ### 2.2. 와일드 카드의 상한과 하한의 제한: Bounded Wildcards
- 제네릭에서의 제한 방법 : extends 하나 
- 와일드카드에서의 제한 방법 : extends(상한), super(하한)
  
### 2.3. 상한 제한된 와일드카드(Upper-Bounded Wildcards)
~~~java
  public static void peekBox(Box<?> box) {
    System.out.println(box);
}
  public static void peekBox(Box<? extends Number> box) {
    System.out.println(box);
}
~~~  
- box는 Box<T> 인스턴스의 참조 값을 전달받는 매개변수이다.
→ 단 전달되는 인스턴스의 T는 Number 또는 이를 상속하는 하위 클래스이어야 함

### 2.4. 하한 제한된 와일드카드(Lower-Bounded Wildcards)
~~~java
public static void peekBox(Box<? super Integer> box) {
  System.out.println(box);
}
~~~
- box는 Box<T> 인스턴스의 참조 값을 전달받는 매개변수이다.
→ 단 전달되는 인스턴스의 T는 Integer 또는 Integer가 상속하는 클래스이어야 함(최하가 Integer)
즉 위 메소드의 인자로 전달 가능한 인스턴스는 Box<Integer>, Box<Number>, Box<Object>으로 제한됨

  ### 2.5. 와일드카드 제한의 이유 설명을 위한 도입
![image](https://github.com/izzy1202/TIL/assets/106478906/ca90cef8-38a2-4af5-a9b7-501f9fb90d86)
- 컴파일 과정에서 프로그래머의 오류가 발견되지 않는다.

### 2.6. 상한 제한의 목적
![image](https://github.com/izzy1202/TIL/assets/106478906/5a66fec2-df26-49ea-ab32-58cf540c3b0f)
- 왜 와일드 카드를 사용함으로써 box에 넣는 구문에 오류가 발견되는가?
  - ? extends Toy : Toy나 Toy를 상속하는 Box<Car>, Box<Robot>이 올 수 있다.
  - Toy만 오는 게 아니라 상속하는 자식 인스턴스도 올 수 있기 때문에 컴파일러가 오류를 발생시킨다.
  - Toy는 Car,Robot의 상위 클래스이기 때문에 Car를 인자로 전달받을 수 있는 메소드에 부모 클래스의 인스턴스를 인자로 전달할 수 없다(상속)
- extends 이면 넣는 것 불가라고 알아두면 좋다.(꺼내는 것만 가능)

### 2.7. 하한 제한의 목적
![image](https://github.com/izzy1202/TIL/assets/106478906/6ed1b23f-d20e-4966-ae3b-82b13f4fdb84)
- 왜 와일드 카드를 사용함으로써 box에서 꺼내는 구문에 오류가 발견되는가?
  - ? super Toy : Toy나 Toy의 부모 클래스인 Plastic이 올 수 있다.
  - Box<Toy> 또는 Box<Plastic> 인스턴스가 인자로 전달될 수 있기 때문에 컴파일러가 오류를 발생시킨다.
- super 이면 꺼내는 것 불가라고 알아두면 좋다.(넣는 것만 가능)

### 2.8. 상한 제한과 하한 제한의 좋은 예 하나
![image](https://github.com/izzy1202/TIL/assets/106478906/b2e45918-e474-4871-ae2d-30c76c988820)
- to 는 super이니까 넣는것만 하겠다, from은 extends이니까 빼는것만 하겠다.

### 2.9. 다음 형태로 메소드 오버로딩 불가능하다
![image](https://github.com/izzy1202/TIL/assets/106478906/a69e5bfb-765f-437a-b55d-3b8ba5ab8516)
- Type Erasure으로 인해 오버로딩이 안된다.
(레거시 코드 가져가면서 제네릭 기능 추가하며 발생한 것)

### 2.10. 그래서 와일드 카드 선언을 갖는 메소드를 제네릭으로
![image](https://github.com/izzy1202/TIL/assets/106478906/07a6ae12-56d0-4f92-97da-ef66dcb4f548)

### 2.11. 제네릭 인터페이스의 정의와 구현
- 인터페이스도 제네릭으로 정의할 수 있다.

# Chapter 23
## 1. 컬렉션 프레임워크의 이해
- 컬렉션 프레임워크 : 인스턴스 저장,참조,삭제에 대한 방법을 모아 놓은 것이다.

### 1.1. 컬렉션 프레임워크
![image](https://github.com/izzy1202/TIL/assets/106478906/7b1ac413-1215-48db-9857-e74da941b9e5)
- 컬렉션 프레임워크에서 제공하는 클래스들은 Set, List, Queue, Map 중 하나를 구현하게 되어있다.
  - Set, List, Queue, Map : 자료구조의 이름
  - Set을 구현하는 클래스가 있다 : Set이라는 자료구조를 기반으로 인스턴스를 저장,참조,삭제한다.

## 2. List 인터페이스를 구현하는 컬렉션 클래스들
### 2.1. List<E> 인터페이스
• ArrayList<E> 배열 기반 자료구조, 배열을 이용하여 인스턴스 저장
• LinkedList<E> 리스트 기반 자료구조, 리스트를 구성하여 인스턴스 저장

![image](https://github.com/izzy1202/TIL/assets/106478906/a9dc4635-cca9-43b5-8dc8-bc26b56d5a76)
- 배열은 내용을 추가할 때 뒤에 덧붙일 수 있는 구조가 아니라, 더 큰 배열을 만들어서 옮기고 기존의 배열을 삭제하는 방식이다.
- LinkedList는 저장 공간을 추가해서 연결만 해주면 된다.

### 2.2. ArrayList<E> 클래스
![image](https://github.com/izzy1202/TIL/assets/106478906/3f6a2e84-4aa1-45c8-8167-2930179820e3)
- 배열 기반 자료구조이지만 공간의 확보 및 확장은 ArrayList 인스턴스가 스스로 처리한다.

### 2.3. LinkedList<E> 클래스
- List<String> list = new ArrayList<>(); 에서 List<String> list = new LinkedList<>(); 
로 바꿔주기만 하면 된다(둘다 list이기 때문)
- 리스트 기반 자료구조는 열차 칸을 더하고 빼는 형태의 자료구조이다. 
  - 인스턴스 저장 : 열차 칸을 하나 더한다. 
  - 인스턴스 삭제 : 해당 열차 칸을 삭제한다.
- 삭제 과정은 ArrayList보다 LinkedList가 훨씬 효율적인 자료구조이다.

### 2.4. ArrayList<E> vs. LinkedList<E>
![image](https://github.com/izzy1202/TIL/assets/106478906/4a7e23ef-a945-4ad5-8f6b-70e02b97211a)

### 2.5. 저장된 인스턴스의 순차적 접근 방법 1: enhanced for문의 사용
![image](https://github.com/izzy1202/TIL/assets/106478906/444b82bd-0d82-4e1e-9e17-c2a78e9009ea)
- for-each문의 대상이 대기 위한 조건 : Iterable<T> 인터페이스의 구현
- Set, List, Queue는 Collection을 상속하므로 Iterable을 구현, Map은 구현하지 않는다.

### 2.6. 저장된 인스턴스의 순차적 접근 방법 2
![image](https://github.com/izzy1202/TIL/assets/106478906/10c1f14d-c2ad-4add-9e11-3bf921eb6105)
- 반복자(iterator)의 next 메소드가 순차적으로 참조하게 해준다.

### 2.7. Iterator 반복자의 세 가지 메소드
![image](https://github.com/izzy1202/TIL/assets/106478906/d4aafbe9-4f09-4fdf-b058-60818d81d927)
- E next() : 다음 인스턴스의 참조 값을 반환
- boolean hasNext() next : 메소드 호출 시 참조 값 반환 가능 여부 확인
- void remove() next : 메소드 호출을 통해 반환했던 인스턴스 삭제
  - remove는 현재 가리키는 대상을 삭제한다.

### 2.8. 배열보다는 컬렉션 인스턴스가 좋다. : 컬렉션변환
1. 인스턴스의 저장과 삭제가 편하다.(size 걱정 x)
2. 반복자를 쓸 수 있다.
단, 배열처럼 선언과 동시에 초기화가 불가능하다. 그러나 다음 방법을 쓸 수 있다.
> List<String> list = Arrays.asList("Toy", "Robot", "Box");

→ 인자로 전달된 인스턴스들을 저장한 컬렉션 인스턴스의 생성 및 반환
→ 이렇게 생성된 리스트 인스턴스는 Immutable 인스턴스이다.

![image](https://github.com/izzy1202/TIL/assets/106478906/fb5aa0b9-5bcd-4493-8068-a4b2384f99f2)
- collection 인스턴스의 참조값을 인자로 받을 수 있다(collection 인터페이스가 모든 collection 클래스의 최상위 인터페이스니까)
  - 새로운 ArrayList가 생성되는데 인자로 전달된 collection 인스턴스의 값을 그대로 복사한다.
  - 중복 저장이 가능해서 Box가 두번 들어간다.
  - list라는 참조변수는 collection 인스턴스를 참조한다.(Immutable 인스턴스라서 추가,삭제는 불가능)
  - 새로 인스턴스를 생성해서 list를 전달하면 추가, 삭제가 가능해진다.
- 그리고 E는 인스턴스 생성 과정에서 결정되므로 무엇이든 될 수 있다.
- 덧붙여서 매개변수 c로 전달된 컬렉션 인스턴스에서는 참조만(꺼내기만) 가능하다.
(복사해야하는데 넣으면 컴파일 오류가 나니까 extends를 넣어준 것)

### 2.9. 배열 기반 리스트를 연결 기반 리스트로
![image](https://github.com/izzy1202/TIL/assets/106478906/e2e6765b-ea1f-4e52-b48b-5bbff2d86fb6)

### 2.10. 기본 자료형 데이터의 저장과 참조
![image](https://github.com/izzy1202/TIL/assets/106478906/fe2609f0-c514-4c07-ba14-e8b464a74536)

- 오토 박싱과 오토 언박싱 덕분에 컬렉션 인스턴스에기본 자료형의 값도 저장 가능하다.

### 2.11. 리스트만 갖는 양방향 반복자
- 단방향 반복자로 해결될 때 사용할 필요는 없다.(코드의 간결성을 위해 제한적 사용)
![image](https://github.com/izzy1202/TIL/assets/106478906/2bc8c147-0ec8-49fe-82ef-cedd580b6a2f)

### 2.12. 양방향 반복자의 예
![image](https://github.com/izzy1202/TIL/assets/106478906/49de32bf-9ac4-4cb3-99d3-fa958c7e6e18)

## 3. Set 인터페이스를 구현하는 컬렉션 클래스들
> List와 Set의 차이
- list는 중복 허용, 순서대로
- set은 중복 허용x, 순서대로x

### 3.1. Set<E>을 구현하는 클래스의 특성과 HashSet<E>클래스
• 저장 순서가 유지되지 않는다.
• 데이터의 중복 저장을 허용하지 않는다.
![image](https://github.com/izzy1202/TIL/assets/106478906/cce42c93-e9fd-4fe7-b3d3-e46fba72ce9b)
- 동일 인스턴스가 저장되지 않았다.
  - 동일 인스턴스의 기준은?

### 3.2. 동일 인스턴스에 대한 기준은?
public boolean equals(Object obj)
- Object 클래스의 equals 메소드 호출 결과를 근거로 동일 인스턴스를 판단한다.(추가할때마다 하나씩 비교해야하는 단점)

public int hashCode()
- 그런데 그에 앞서 Object 클래스의 hashCode 메소드 호출 결과가 같아야 한다.
- 정리하면,두 인스턴스가 hashCode 메소드 호출 결과로 반환하는 값이 동일해야 한다.
- 그리고 이어서 두 인스턴스를 대상으로 equals 메소드의 호출 결과 true가 반환되면 동일 인스턴스로 간주한다.

### 3.3. 해쉬 알고리즘의 이해(분류 기법 알고리즘)
![image](https://github.com/izzy1202/TIL/assets/106478906/3e5db912-428e-444c-9631-5b0ec4a4ab44)
- 분류를 해 놓으면 탐색의 속도가 매우 빨라진다. 즉 존재 유무 확인이 매우 빠르다
- Object 클래스의 hashCode 메소드는 이렇듯 인스턴스들을 분류하는 역할을 한다.

### 3.4. 해쉬 알고리즘 일일이 정의하기 조금 그렇다면
![image](https://github.com/izzy1202/TIL/assets/106478906/a1f9caf1-9e6b-48c9-bc35-a6eebc7e87b1)
- 적절한 해쉬 값을 만들어준다(전달된 인자를 모두 반영한 해쉬 값을 반환한다.)

### 3.5. TreeSet<E> 클래스의 이해와 활용
> Set<E> 인터페이스를 구현하는 TreeSet<E> 클래스
- 트리(Tree) 자료구조를 기반으로 인스턴스를 저장, 이는 정렬 상태가 유지되면서 인스턴스가 저장됨을 의미
- 반복자의 인스턴스 참조 순서는 오름차순을 기준으로 한다는 특징이 있다.

### 3.6. TreeSet<E> 클래스의 오름차순 출력이란?
![image](https://github.com/izzy1202/TIL/assets/106478906/85822fb9-503c-4b0a-b3b2-b1aefdc17831)
- TreeSet<E> 클래스는 CompareTo 메소드를 통해 크고 작음을 구분한다.
- 제네릭이 추가되면서 Object 대신 T를 쓰는 형태로 발전했다.
- Comparable<T> 인터페이스의 구현 결과를 근거로 저장이 이뤄지고 참조가 진행이 된다.
- 따라서 TreeSet<T>에 저장할 인스턴스들은 모두 Comparable<T> 인터페이스를 구현한 클래스의
인스턴스이어야 함. 아니면 예외 발생!

### 3.7. Comparator<T> 인터페이스 기반으로 TreeSet<E>의 정렬기준 제시하기
> public interface Comparator<T>
- int compare(T o1, T o2) 의 구현을 통해 정렬 기준을 결정할 수 있다.
- 위 인터페이스를 구현한 클래스의 인스턴스를 TreeSet<E>의 다음 생성자를 통해 전달!
public TreeSet(Comparator<? super E> comparator)
- Comparator 구현 인스턴스를 전달하여 새로운 기준을 제공

### 3.8. 중복된 인스턴스의 삭제
![image](https://github.com/izzy1202/TIL/assets/106478906/92228942-6cf5-4555-8339-e94a6718187f)

## 4. Queue<E> 인터페이스를 구현하는 컬렉션 클래스들
### 4.1. 스택과 큐의 이해
![image](https://github.com/izzy1202/TIL/assets/106478906/7a534903-e860-4357-987b-4915146c8f65)
- 스택(밑이 막힌 깡통)
  - LIFO(last-in-first-out) : 먼저 저장된 데이터가 마지막에 빠져나간다.
- 큐(양옆이 뚫린 파이프)
  - FIFO(first-in-first-out) :먼저 저장된 데이터가 먼저 빠져나간다.

### 4.2. 큐 인터페이스
![image](https://github.com/izzy1202/TIL/assets/106478906/d55e7fab-b034-45f4-aef5-13ae9f95b7e1)
- add, remove, element의 경우 예외 처리에 의해 처리된다. 
- offer, poll, peek의 경우 false,null,null을 반환해주므로 이 매소드들이 더 많이 활용된다.

### 4.3. 큐의 구현
![image](https://github.com/izzy1202/TIL/assets/106478906/32414654-b23d-44c9-b18d-5cb35f9398d1)

### 4.4. 스택(Stack)의 구현
- Deque을 기준으로 스택을 구현하는 것이 자바에서의 원칙
(큐와 비슷하나, 큐는 들어오고 나가는 방향이 정해져있다면 덱은 정해져있지 않다)
![image](https://github.com/izzy1202/TIL/assets/106478906/cadbdf3d-73b4-444c-8da7-af02d3860433)
- 덱에서 한 방향만 막으면 스택

### 4.5. 스택의 예
![image](https://github.com/izzy1202/TIL/assets/106478906/908c62d1-c007-406f-ad26-de2cade70fe6)

## 5. Map<K, V> 인터페이스를 구현하는 컬렉션 클래스들   
- Map은 Collection 인터페이스를 상속하지 않으므로 반복자를 얻을 수 없다.

### 5.1. Key-Value 방식의 데이터 저장과 HashMap<K, V> 클래스
![image](https://github.com/izzy1202/TIL/assets/106478906/4bddc29c-72f6-4afa-ac06-b0c626135440)
![image](https://github.com/izzy1202/TIL/assets/106478906/73c7043a-1c12-4b05-b6e8-c277c6f1a4d3)

- key는 중복되지 않는다.(List보다 Set이 어울린다)
  - Map에 key를 달라는 메소드 호출하면 Set을 구현한 인스턴스를 만들고 이 인스턴스는 key를 가지고 있다.
이 인스턴스에 반복자를 통해 key를 받아와서 Map에 순차적 접근해서 value를 받아온다.

### 5.2. HashMap<K, V>의 순차적 접근 방법
- HashMap<K, V> 클래스는 Iterable<T> 인터페이스를 구현하지 않으니 for-each문을 통해서, 혹은 ‘반복자’를 얻어서 순차적 접근을 진행할 수 없다.
- 대신 다음 메소드 호출을 통해서 Key를 따로 모아 놓은 컬렉션 인스턴스를 얻을 수 있다. 그리고 이때 반환된 컬렉션 인스턴스를 대상으로 반복자를 얻을 수 있다.
  - public Set<K> keySet()

### 5.3. HashMap<K, V>의 순차적 접근의 예
![image](https://github.com/izzy1202/TIL/assets/106478906/ac31db31-05d8-4be5-bd49-ca55c537b4f7)

### 5.4. TreeMap<K, V>의 순차적 접근의 예
![image](https://github.com/izzy1202/TIL/assets/106478906/a6607737-bbbb-4d06-abee-829e6d6e01a6)

