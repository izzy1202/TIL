# <윤성우의 열혈 Java> 강의 내용 정리
>[강의 링크](https://cafe.naver.com/cstudyjava/135782?boardType=L)

> Chapter 14 ~ 
> 
>모든 내용을 정리하지는 않음

---

# Chapter 14

## 1. 상속의 기본 문법 이해Ⅰ

### 1.1. 상속의 매우 치명적인 오해
- “코드의 재활용을 위한 문법입니다.” ( X )
- “연관된 일련의 클래스들에 대해 공통적인 규약을 정의할 수 있습니다.“ ( O )

## 2. 상속의 기본 문법 이해 Ⅱ
![image](https://user-images.githubusercontent.com/106478906/232043175-ff2c267b-058f-49c2-9661-6bb8b2832234.png)

- BusinessMan 클래스가 Man을 상속받을때, BusinessMan 인스턴스 안에는 Man의 멤버들도 존재하게 된다.
- 주의할 점 : private으로 선언하면 같은 인스턴스 내에 존재함에도 Man class에 접근할 수 없다.

### 2.1. 상속 관련 용어의 정리와 상속의 UML 표현
![image](https://user-images.githubusercontent.com/106478906/232043754-b1f5f632-9101-4e20-8da6-c30ce082fc22.png)
- 상속의 UML 표현 : 화살표가 하위 클래스에서 상위 클래스 방향으로 향한다.

### 2.2. 상속과 생성자 1
- 생성자는 그 클래스 안에 존재하는 인스턴스 변수를 초기화하는 것이 목적이다.
![image](https://user-images.githubusercontent.com/106478906/232048924-2f180d05-632a-497f-ad29-ed51d25c9ffa.png)

-> BusinessMan 인스턴스 안에는 Man의 인스턴스 변수인 name도 존재하게 되는데, BusinessMan 생성자에서 BusinessMan의 인스턴스 변수인 company,position은 초기화 되지만 name이 초기화 되지 않는 문제가 발생한다.

![image](https://user-images.githubusercontent.com/106478906/232050406-81f992e5-f807-4b97-8089-ac1eceaa08ea.png)

- BusinessMan 생성자에서 Man의 name을 초기화할 수 있는 인자를 하나 추가로 받는다.

-> 모든 멤버의 초기화는 이루어진다. 그러나 생성자를 통한 초기화 원칙에는 어긋난다.(동작하는 코드 O, 좋은 코드 X)
  - 클래스가 정의될 때 멤버 변수는 해당 클래스의 생성자에서 초기화해주는 것이 가장 이상적이다.
  
## 3. 상속의 기본 문법 이해 Ⅲ

### 3.1. 상속과 생성자: 생성자 호출 관계 파악하기
- 상위 클래스의 생성자 실행 후 하위 클래스의 생성자 실행 됨
  - 하위 클래스의 생성자에서는 반드시 상위 클래스의 생성자를 호출하게 되어있다. 
  - 없으면 컴파일러가 대신 넣어준다.

### 3.2. 상속과 생성자: 상위 클래스의 생성자 호출 지정
- 키워드 super를 통해 상위 클래스의 생성자 호출을 명시할 수 있다.
  - 생성자 안에서만 사용해야 한다.
  - 컴파일러가 대신 넣어주는 문장 : super(); <- 인자값 받지 않는 생성자가 호출되는 문장
 
### 3.3. 적절한 생성자 정의의 예
![image](https://user-images.githubusercontent.com/106478906/232062628-9e5a4c40-c2e5-4e28-befa-32cb7f0c21f1.png)

### 3.4. 단일 상속만 지원하는 자바
- 다중 상속 : 하나의 클래스가 둘 이상의 클래스를 상속하는 것이다.
-자바는 다중 상속을 지원하지 않는다.
- 한 클래스에서 상속할 수 있는 최대 클래스의 수는 한 개이다.

## 4. 클래스 변수, 클래스 메소드와 상속

### 4.1. 클래스 변수, 메소드는 상속이 되는가?
- 답은 NO
- 프로그램 전체에서 딱 하나만 존재하는데 상속의 대상이 되겠는가?
- 그러나 접근 수준 지시자에서 허용한다면, 하위 클래스에서 이름만으로 접근 가능하다.

# Chapter 15

## 1. 상속을 위한 두 클래스의 관계  

- 객체지향 언어(JAVA)는 현실 세계를 모델링해서 만든 언어이다.

### 1.1. 상속 관계에 놓은 두 대상의 관찰

#### 1.1.1. 상속의 특성
- 하위 클래스는 상위 클래스의 모든 특성을 지닌다.
- 거기에 더하여 하위 클래스는 자신만의 추가적인 특성을 더하게 된다.
- 상속 관계에 있는 두 대상은 IS-A 관계를 가져야 한다.
  - A(스마트폰)은 일종의 B(모바일폰)이다.

### 1.2. 상속과 IS-A 관계
- IS-A 관계 : .. 은 .. 이다. 의 관계
- ex) 노트북은 컴퓨터이다. 전기자동차는 자동차이다.
- IS-A 관계를 갖지 않는 두 클래스가 상속으로 연결되어 있다면, 적절한 상속인지 의심해야 한다.
- 자식클래스는 부모클래스 + 알파이다.

## 2. 메소드 오버라이딩Ⅰ
- 자식 클래스의 인스턴스는 자식 클래스의 참조변수와 부모 클래스의 참조변수로 모두 참조 가능하다.

![image](https://user-images.githubusercontent.com/106478906/234558225-d780faac-e85b-4e5f-a6a6-2885658548a7.png)
- 자식 클래스의 인스턴스에 자식 클래스(스마트폰)의 참조 변수로 접근하면 모든 메소드를 다 호출할 수 있지만 부모 클래스(모바일폰)의 참조 변수로 접근하면 부모 클래스안의 메소드만 호출 가능하다.

## 3. 메소드 오버라이딩 Ⅱ
![image](https://user-images.githubusercontent.com/106478906/234561310-383dd35a-f8e5-40e9-a697-17d3ef7f94a9.png)
- 가리키는 인스턴스는 StrawberryCheeseCake인스턴스로 동일하지만, 접근 권한은 다르다.

~~~java
class Cake {
public void sweet() {...}
}

class CheeseCake extends Cake {
public void milky() {...}
}

CheeseCake ca1 = new CheeseCake();
Cake ca2 = ca1; // 가능!

Cake ca3 = new CheeseCake();
CheeseCake ca4 = ca3; // 불가능!
~~~

- 컴파일러가 치즈케이크가 참조하는 대상을 케이크가 참조가 가능하다는 것을 알고 위의 대입을 허용해준다. 
- 컴파일러는 문장단위로 기억하기 때문에 이 시점에 컴파일러 및 가상머신은 ca3가 참조하는 대상을 Cake 인스턴스로 판단한다.
  - ca3가 참조하는 인스턴스의 정확한 클래스 정보는 유지하지 않는다.
~~~java
class Cake {
public void sweet() {...}
}

class CheeseCake extends Cake {
public void milky() {...}
}
  
Cake cake = new CheeseCake(); // 가능
CheeseCake[] cakes = new CheeseCake[10]; // 가능
Cake[] cakes = new CheeseCake[10]; // 가능
~~~
  
- 상속의 관계가 배열 인스턴스의 참조 관계까지 이어진다.
  - 치즈케이크형 배열 인스턴스는 치즈케이크형 배열의 참조변수로도 참조가 가능하지만, 상속관계에 있는 케이크형 배열의 참조변수로도 참조가 가능하다.

## 4. 메소드 오버라이딩 Ⅲ
~~~java
class Cake {
public void yummy() {
System.out.println("Yummy Cake");
  }
}

class CheeseCake extends Cake {
public void yummy() {
System.out.println("Yummy Cheese Cake");
  }
}
~~~
- 오버라이딩 관계
  - CheeseCake의 yummy 메소드가 Cake의 yummy 메소드를 오버라이딩한 것이다.
  - 오버라이딩 = 가린다고 생각하면 됨
- 반환형, 메소드 이름, 매개변수 선언이 같을 때 
- 부모 클래스의 참조변수로 인스턴스를 참조하더라도 오버라이딩 때문에 부모 클래스의 yummy 메소드를 가려버려서 자식 클래스의 yummy가 대신 호출된다.

### 4.1. 오버라이딩 된 메소드 호출하는 방법
~~~java
class Cake {
public void yummy() {
System.out.println("Yummy Cake");
  }
}

class CheeseCake extends Cake {
public void yummy() {
super.yummy();
System.out.println("Yummy Cheese Cake");
}

public void tasty() {
super.yummy();
System.out.println("Yummy Tasty Cake");
  }
}
~~~
- 오버라이딩 된 메소드를 인스턴스 외부에서 호출하는 방법은 없다. 그러나 인스턴스 내부에서는 키워드 super를 이용해 호출 가능하다.

### 4.2. 인스턴스 변수와 클래스 변수도 오버라이딩이 되는가?
~~~java
class Cake {
public int size;
....
}

class CheeseCake extends Cake {
public int size;
....
}

CheeseCake c1 = new CheeseCake();
c1.size = ... // CheeseCake의 size에 접근

Cake c2 = new CheeseCake();
C2.size = ... // Cake의 size에 접근
~~~
- 인스턴스 변수는 오버라이딩 되지 않는다. 따라서 참조변수의 형에 따라 접근하는 멤버가 결정된다.
- 하지만 이런 식으로 같게 변수 선언은 하지 않는 것이 좋다.

## 5. instanceof 연산자 
- 참조가능성을 묻는 것이다.
~~~java
  if(ref instanceof ClassName)
~~~
> ref가 ClassName 클래스의 인스턴스를 참조하면 true 반환

>ref가 ClassName를 상속하는 클래스의 인스턴스이면 true 반환

### 5.1. instanceof 연산자의 활용
![image](https://user-images.githubusercontent.com/106478906/234596192-634f2953-494b-4fb4-9a93-6fa2ef6dd768.png)

- 상속은 연관된 일련의 클래스들에 대해 공통적인 규약을 정의할 수 있다.

# Chapter 16

## 1. 상속이 도움이 되는 상황의 소개
> 상속에 대해 이정도는 설명할 수 있어야 한다
- UML 다이어그램으로 A(부모클래스) <- B(자식클래스)
- A a = new B(); : 자식 클래스의 인스턴스를 생성해서 부모 클래스의 참조변수로 참조할 수 있다.
- A 클래스의 fct()라는 메소드와 B클래스에서 메소드명,반환타입,매개변수 선언이 같다면 그게 오버라이딩이고, A의 참조변수 a가 참조하는 인스턴스는 B의 인스턴스이지만 a를 통해 접근할때는 A클래스 영역만 접근 가능하다. 하지만 a.fct()가 오버라이딩 되었기 때문에 a.fct(); 호출하면 B클래스의 fct()가 호출된다. 

### 1.1. 단순한 인맥 관리 프로그램: 관리 대상이 둘!
> 프로그램
1. 안정적
2. 확장성
- 관리 대상이 둘이므로 두 개의 클래스가 정의된다.
- 배열이 나눠지고 저장하는 방법도 나눠지고 참조하는 방법도 나눠지는 등 코드가 복잡해진다.
- 이러한 클래스 디자인 기반에서 관리 대상이 넷, 다섯으로 늘어난다면? 늘어나는 수 만큼 코드 복잡해짐

### 1.2. 상속 기반의 문제 해결: 두 클래스 상속 관계로 묶기
![image](https://user-images.githubusercontent.com/106478906/234754834-77fa8920-5b69-40fe-bc9c-1d0334777312.png)

- 연관된 일련의 클래스들에 대해 공통적인 규약(Friend)을 정의 및 적용할 수 있다.
- CompFriend와 UnivFriend 클래스에 대해 Friend 클래스라는 규약을 정의하고 적용할 수 있다.

### 1.3. 상속으로 묶은 결과
~~~java
public static void main(String[] args) {
  Friend[] frns = new Friend[10]; // 배열이 하나니까
  int cnt = 0;
  frns[cnt++] = new UnivFriend("LEE", "Computer", "010-333-555"); // 저장하는 방법도 하나
  frns[cnt++] = new UnivFriend("SEO", "Electronics", "010-222-444");
  frns[cnt++] = new CompFriend("YOON", "R&D 1", "02-123-999");
  frns[cnt++] = new CompFriend("PARK", "R&D 2", "02-321-777");
  
  // 모든 동창 및 동료의 정보 전체 출력
  for(int i = 0; i < cnt; i++) { // 하나의 for문으로 전체 정보 출력 가능
  frns[i].showInfo(); // 오버라이딩 한 메소드가 호출된다.
  System.out.println();
  }
} 
~~~
> 이러한 클래스 디자인 기반에서 관리 대상이 넷, 다섯으로 늘어 난다고 해도, 인스턴스 관리와 관련해서 코드가 복잡해지지 않는다.
- Friend 인스턴스를 저장할 수 있는 하나의 배열에 저장했음에도, 오버라이딩으로 인해 UnivFriend, CompFriend ...의 메소드가 호출될 수 있다. (확장성)

## 2. Object 클래스와 final 선언 그리고 @Override

### 2.1. 모든 클래스는 Object 클래스를 상속합니다.
~~~java
// System.out.println
public void println(Object x) {
. . .
String s = x.toString();
. . .
}
~~~
- 모든 클래스는 Object를 상속하므로 위 메소드의 인자로 전달이 가능하다.
- toString 메소드는 Object 클래스의 메소드였음을 알 수 있다.

### 2.2. 프로그래머가 정의하는 toString은 메소드 오버라이딩
- 그 클래스의 인스턴스가 가지고 있는 정보를 잘 표현할 수 있도록 디자인하는 것이 권고된다.

### 2.3. 클래스와 메소드의 final 선언
~~~java
public final class MyLastCLS {...}
→ MyLastCLS 클래스는 다른 클래스가 상속할 수 없음

class Simple {
  // 아래의 메소드는 다른 클래스에서 오버라이딩 할 수 없음
  public final void func(int n) {...}
}
~~~

### 2.4. @Override
~~~java
class ParentAdder {
  public int add(int a, int b) {
  return a + b;
  }
}

class ChildAdder extends ParentAdder {
@Override
public double add(double a, double b) {
  System.out.println("덧셈을 진행합니다.");
  return a + b;
  }
}
-> 오버라이딩이 아니라 상속으로 두 클래스에 걸쳐서 형성된 메소드 오버로딩이다. 따라서 컴파일 오류가 발생한다.
~~~
> 상위 클래스의 메소드를 오버라이딩 하는 것이 목적이라는 선언이다.

> 오버라이딩을 하는 형태가 아니면 컴파일러가 오류 메시지 전달.
- 매개변수 선언이 다르므로 오버라이딩 성립이 안된다.
- 특별한 기능을 더해주지는 않지만, 컴파일러에게 오버라이딩이라는 정보를 전달함으로써 오버라이딩을 하고자 했지만 오버로딩이 되는 상황을 막을 수가 있다.
  - 기능 제공이 아니라 안전성을 높이기 위한 문법이다.

# Chapter 17

## 1. 인터페이스의 기본과 그 의미
- 인터페이스 : 기능 활용 방법, 통신 도구/수단
- ex) 커피 머신에서 커피를 뽑아 먹기 위해서 커피 머신의 모든 기능을 알 필요 없고 커피 머신 버튼을 누르고 컵을 빼면 된다. 이런 과정이 인터페이스이다.
- implements : 구현하겠다(완성하겠다)
  - 프린터 클래스는 프린터블 인터페이스를 구현한 것이다.
  - 추상 클래스는 인스턴스를  생성할 수는 없지만, 프린터 클래스의 인스턴스를 참조할 수 있다.
- 클래스의 인스턴스를 생성해서 접근할때는 인터페이스의 메소드를 통해서 접근해라


## 2. 인터페이스의 문법 구성과 추상 클래스
- 인터페이스는 외부에서 해당 클래스의 사용 방법을 명시한 것이다.
  - 사용 방법을 노출시켜야 하기 때문에 인터페이스 안의 추상 메소드는 public이 기본값이다.
  - public 선언을 하지 않더라도 기본적으로 public 선언을 한 것으로 간주된다.(인터페이스는 default 선언이 없음)
- 인터페이스는 인스턴스 변수를 가질 수 없다.
- 인터페이스 안에 static final로 상수를 선언할 수 있다.
  - 인터페이스명.상수명 이렇게 접근 가능하다.
  - 즉, 선언하지 않아도 public static final로 간주된다.

### 2.1. 인터페이스간 상속: 문제 상황의 제시
![image](https://user-images.githubusercontent.com/106478906/235305660-ac363af4-1ce6-403c-8f67-2af2a2f72e32.png)

- 컬러 출력 위한 메소드 추가되면 시스템 전체에 문제 발생한다.
- 인터페이스를 구현하는 클래스는 해당 인터페이스의 모든 추상 메소드를 구현해야 한다. 그래야 인스턴스를 생성할 수 있기 때문이다.

### 2.2. 제시한 문제의 해결책: 인터페이스의 상속
- 새로운 메소드를 기존 인터페이스에 넣는 것이 아니라, 기존 인터페이스를 상속하는 새로운 인터페이스를 만들어서 새 메소드를 넣는다.
  - extends 키워드 사용
  - 기존 클래스를 수정할 필요 없다.
  
### 2.3. 인터페이스의 디폴트 메소드: 문제 상황의 제시
- 실무에서 직접 쓸 일은 거의 없고 그냥 이해하기.
- 총 256개의 인터페이스가 존재하는 상황에서 모든 인터페이스에 다음 추상 메소드를 추가해야 한다면?
- 인터페이스간 상속? 물론 인터페이스간 상속으로 문제 해결 가능하다. 다만 인터페이스의 수가 256개 늘어날 뿐이다.(문제다)

### 2.4. 문제 상황의 해결책: 인터페이스의 디폴트 메소드
- 다음 디폴트 메소드로 이 문제를 해결하면 인터페이스의 수가 늘어나지 않는다.
~~~java
  default void printCMYK(String doc) { } // 디폴트 메소드
~~~

### 2.5. 인터페이스의 static 메소드
~~~java
interface Printable {
  static void printLine(String str) {
  System.out.println(str);
  }
default void print(String doc) {
  printLine(doc); // 인터페이스의 static 메소드 호출
  }
}
~~~
- 인터페이스에도 static 메소드를 정의할 수 있다.
  - default 메소드인 경우에는 인터페이스 내에서 호출 가능하다.
  - 인터페이스명.메소드명 이렇게 어디서든 접근 가능하다.
- 인터페이스의 static 메소드 호출 방법은 클래스의 static 메소드 호출 방법과 같다.

### 2.6. 인터페이스 대상의 instanceof 연산
~~~java
  if(ca instanceof Cake) ....
~~~
- Cake는 클래스의 이름도, 인터페이스의 이름도 될 수 있다
- ca가 참조하는 인스턴스를 Cake형 참조변수로 참조할 수 있으면 true 반환한다.
= ca가 참조하는 인스턴스가 Cake를 직접 혹은 간접적으로 구현한 클래스의 인스턴스인 경우 true 반환한다.
= 참조 변수 ca가 참조하는 인스턴스가 Cake 인스턴스나 Cake를 부모 클래스로 상속받는 인스턴스여야 한다.

- 상속에서의 instanceof 연산과 의미가 같다.

### 2.7. 인터페이스 대상 instanceof 연산의 예
![KakaoTalk_20230502_090301512](https://user-images.githubusercontent.com/106478906/235552197-2e844045-e33a-4b2d-a065-56e65841c74d.jpg)

- 비공식적으로 간접구현, 직접구현이라고 부른다.
  - SimplePrinter가 Printable 인터페이스를 직접 구현하고, MultiPrinter가 Printable 인터페이스를 간접 구현한다.
  - prn1 참조변수가 참조하는 인스턴스가 Printable 구현하냐? true(직접구현)
  - prn2 참조변수가 참조하는 인스턴스가 Printable 구현하냐? true(간접구현)

### 2.8. 인터페이스의 또 다른 용도: Marker 인터페이스
![KakaoTalk_20230502_090752063](https://user-images.githubusercontent.com/106478906/235552631-52a54f15-2a90-4762-b6d9-1bb856fe7b2f.jpg)

- 클래스에 특정 표시를 해 두기 위한 목적으로 정의된 인터페이스를 마커 인터페이스라 한다. 
- 마커 인터페이스에는구현해야 할 메소드가 없는 경우가 흔하다.

### 2.8. 추상 클래스
~~~java
public abstract class House { // 추상 클래스
  public void methodOne() {
    System.out.println("method one");
  }
  public abstract void methodTwo(); // 추상 메소드
}
~~~
- abstract로 추상 클래스임을 명시해준다.
> 하나 이상의 추상 메소드를 지니는 클래스를 가리켜 추상 클래스라 한다. 

> 추상 클래스를 대상으로는 인스턴스 생성이 불가능하다. 물론 참조변수 선언은 가능하다.
- 인스턴스화 되는 게 아니라 상위 클래스로서 하위 클래스에서 추상 메소드를 구현해서 사용하는 용도로 만들어졌다.

#### 2.8.1. 인터페이스와 추상 클래스의 차이점
- 인터페이스는 인스턴스 변수, 메소드를 안에 둘 수 없고 추상 클래스는 가능하다.

# Chapter 18

## 1. 자바 예외처리의 기본
> 예외 : 프로그램 일반적 원칙에서 벗어난 사용자의 실수

### 1.1. 자바에서 말하는 예외

#### 1.1.1. 예외(Exception)
- ‘예외적인 상황’을 줄여서 ‘예외’라 한다.
- 단순한 문법 오류가 아닌 실행 중간에 발생하는 ‘정상적이지 않은 상황’을 뜻한다.(기대하지 못한 상황)

#### 1.1.2. 예외처리
- 예외 상황에 대한 처리를 의미한다. 
- 자바는 예외처리 메커니즘을 제공한다.

### 1.2. 예외 상황의 예
![KakaoTalk_20230502_093232447](https://user-images.githubusercontent.com/106478906/235554915-c3554d4d-e95c-4450-9d2d-eabce1a4eaf0.jpg)
- 분모에 0이 들어가서 예외가 발생했고 예외 처리를 해주지 않았기 때문에 JVM이 프로그램을 종료시켰다.

### 1.3. 예외 상황의 또 다른 예
![KakaoTalk_20230502_093515817](https://user-images.githubusercontent.com/106478906/235555173-20d13605-203f-44e5-a52c-ee37dde14ec4.jpg)
- 정수가 아닌 문자를 입력해서 예외가 발생했고 예외 처리를 해주지 않았기 때문에 JVM이 프로그램을 종료시켰다.

### 1.4. 예외 상황을 알리기 위한 클래스
> 과거에는 if else로 예외 처리를 했다.
- 예외 처리 코드가 다른 코드와 구분되지 않는 문제가 발생
-> catch 등장

> java.lang.ArithmeticException
→ 수학 연산에서의 오류 상황을 의미하는 예외 클래스
> java.util.InputMismatchException
→ 클래스 Scanner를 통한 값의 입력에서의 오류 상황을 의미하는 예외 클래스

### 1.5. 예외의 처리를 위한 try ~ catch
~~~java
try {
  ...관찰 영역...
}
catch(ArithmeticException e) {
  ...처리 영역...
}
~~~
- 예외의 처리를 위한 코드를 별도로 구분하기 위해 디자인된 예외처리 메커니즘이 try ~ catch 이다.

### 1.6. try ~ catch의 예
![image](https://user-images.githubusercontent.com/106478906/235557649-48c315be-b78a-4884-8269-9ab567fb17fb.png)

### 1.7. 예외 발생 이후의 실행 흐름
~~~java
try {
  1. ...
  2. 예외 발생 지점
  3. ...
}
catch(Exception e) {
  ...
}
4. 예외 처리 이후 실행 지점
~~~

### 1.8. try로 감싸야 할 영역의 결정
![image](https://user-images.githubusercontent.com/106478906/235558073-d9f245fc-82ea-4ed4-a2d2-4a059af0af95.png)

> try: 예외가 발생할 수 있는 영역을 묶기 위한 용도도 있지만, 하나의 작업을 묶는 용도로도 사용된다.

### 1.9. 둘 이상의 예외 처리를 위한 구성1
![image](https://user-images.githubusercontent.com/106478906/235558200-40ada762-5fbf-4b25-aa04-f90f83d1d237.png)

- 위의 catch 다음에 아래 catch가 처리된다는 것을 알아두어야 한다.
### 1.10. 둘 이상의 예외 처리를 위한 구성2
![image](https://user-images.githubusercontent.com/106478906/235558267-06071369-eb46-4119-802a-739e41034701.png)

### 1.11. Throwable 클래스
- cf. 모든 예외처리 클래스를 알 필요 없고 필요한 부분을 상황따라 공부하는 것이 좋다.
> java.lang.Throwable 클래스
- 모든 예외 클래스의 최상위 클래스: 물론 Throwable도 Object를 상속한다.

> Throwable 클래스의 메소드 둘

- public String getMessage() : 예외의 원인을 담고 있는 문자열을 반환
- public void printStackTrace() : 예외가 발생한 위치와 호출된 메소드의 정보를 출력
  - 이거도 원인 문자열 같이 출력해주기 때문에 보통 이 메소드 사용
  
### 1.12. 예외의 (책임)전달
![image](https://user-images.githubusercontent.com/106478906/235560721-359ee8e8-dd9d-4035-8a2d-4a95d93ecf47.png)
> 예외 발생 지점에서 예외를 처리하지 않으면 해당메소드를 호출한 영역으로 예외가 전달된다.
- 예외 처리를 넘기고 넘겨서 JVM한테까지 가면 JVM이 printStachTrace를 호출해서 해결한다.(적절한 방법은 아님)
![KakaoTalk_20230502_103819986](https://user-images.githubusercontent.com/106478906/235561481-81b6f7fc-04c3-4da6-8a09-0b26e1e522f7.jpg)

-  printStachTrace 에서 나오는 예외처리 위치들을 보고 예외를 처리하는 것도 괜찮은 방법이다.

### 1.13. ArrayIndexOutOfBoundsException

![image](https://user-images.githubusercontent.com/106478906/235561747-ce101104-5a9f-4261-92fc-e41c5b7b115b.png)

### 1.14. ClassCastException
~~~java
class Board { }
class PBoard extends Board { }

class ClassCast {
public static void main(String[] args) {
    Board pbd1 = new PBoard(); // 부모 클래스의 참조변수로 자식 클래스의 인스턴스를 참조
    PBoard pbd2 = (PBoard)pbd1; // 강제 형변환을 했기 때문에 OK!

    Board ebd1 = new Board();
    PBoard ebd2 = (PBoard)ebd1; // Exception!
  }
)
~~~
> 자식 클래스의 참조변수로 부모 클래스의 인스턴스를 참조하는 것은 허용되지 않기 때문에 ClassCastException 발생한다.

### 1.15. NullPointerException
~~~java
class NullPointer {
  public static void main(String[] args) {
  String str = null;
  System.out.println(str); // null 출력
  int len = str.length(); //str이라는 참조변수가 참조하는 인스턴스가 없는데 길이를 반환할 수 없기 때문에 Exception!
  }
}
~~~
> null : 아무것도 가리키지 않는다.

## 2. 예외처리에 대한 나머지 설명들 (1)

### 2.1. 예외 클래스의 구분
1. Error 클래스를 상속하는 예외 클래스
2. Exception 클래스를 상속하는 예외 클래스
3. RuntimeException 클래스를 상속하는 예외 클래스
→ RuntimeException 클래스는 Exception 클래스를 상속한다.

### 2.2. Error 클래스를 상속하는 예외 클래스들의 특성
- Error 클래스를 상속하는 예외 클래스의 예외 상황은 시스템 오류 수준의 예외 상황으로 프로그램 내에서 처리 할수 있는 수준의 예외가 아니다.
- 그냥 이런게 있다고 알아두기

### 2.3. RuntimeException 클래스를 상속하는 예외 클래스들의 특성
- 코드 오류로 발생하는 경우가 대부분이다. 따라서 이 유형의 예외 발생시 코드의 수정을 고려해야 한다.
- 보는 관점에 따라 에러가 될 수도, 예외가 될 수도 있다.(에러에 가깝다)
- ex) ArithmeticException
      ClassCastException
      IndexOutOfBoundsException
      NegativeArraySizeException 배열 생성시 길이를 음수로 지정하는 예외의 발생
      NullPointerException
      ArrayStoreException 배열에 적절치 않은 인스턴스를 저장하는 예외의 발생

### 2.4. Exception 클래스를 상속하는 예외 클래스들의 특성
- 코드의 문법적 오류가 아닌, 프로그램 실행 과정에서 발생하는 예외적 상황을 표현하기 위한 클래스들이다. 따라서 예외의 처리를 어떻게 할 것인지 반드시 명시해 주어야 한다.
- ex) java.io.IOException 입출력 관련 예외 상황을 표현하는 예외 클래스

### 2.5. Exception을 상속하는 예외의 예
~~~java
public static void main(String[] args) {
  Path file = Paths.get("C:\\javastudy\\Simple.txt");
  BufferedWriter writer = null;
  
  try {
  writer = Files.newBufferedWriter(file); // IOException 발생 가능
  writer.write('A’); // IOException 발생 가능
  writer.write('Z’); // IOException 발생 가능
  
    if(writer != null)
    writer.close(); // IOException 발생 가능
  }
  
  catch(IOException e) {
  e.printStackTrace();
  }
}
~~~
- Exception을 상속하는 예외는 반드시 처리를 해야 한다. 그렇지 않으면 컴파일 오류로 이어진다.

### 2.6. 처리하거나 아니면 넘기거나
~~~java
public static void main(String[] args) {
  try {
      md1();
  }
  catch(IOException e) {
      e.printStackTrace();
  }
  }
  public static void md1() throws IOException { // IOException 예외 넘긴다고 명시!
    md2();
  }
  public static void md2() throws IOException { // IOException 예외 넘긴다고 명시!
    Path file = Paths.get("C:\\javastudy\\Simple.txt");
    BufferedWriter writer = null;
    writer = Files.newBufferedWriter(file); // IOException 발생 가능
    writer.write('A'); // IOException 발생 가능
    writer.write('Z'); // IOException 발생 가능
    if(writer != null)
    writer.close(); // IOException 발생 가능
}
~~~
- 메소드의 throws절 선언을 통해 예외의 처리를 넘길 수 있다.

### 2.7. 둘 이상의 예외 넘김에 대한 선언
~~~java
public void simpleWrite() throws IOException, IndexOutofBoundsException {
....
}
~~~

## 3. 예외처리에 대한 나머지 설명들 (2)
### 3.1. 프로그래머가 정의하는 예외 클래스
~~~java
class MyExceptionClass {
  public static void main(String[] args) {
  System.out.print("나이 입력: ");
  
  try {
  int age = readAge();
  System.out.printf("입력된 나이: %d \n", age);
  }
  catch(ReadAgeException e) {
    System.out.println(e.getMessage());
  }
}
public static int readAge() throws ReadAgeException {
  Scanner kb = new Scanner(System.in);
  int age = kb.nextInt();
  
  if(age < 0)
    throw new ReadAgeException(); // 예외의 발생
    return age;
  }
}

class ReadAgeException extends Exception {
. . .
}
~~~

### 3.2. 잘못된 catch 구문의 구성
![image](https://user-images.githubusercontent.com/106478906/235838129-bf238f74-d6de-4e39-8b60-a72e2b9fdaf0.png)
- catch(FirstException e) {...}에서 예외를 다 잡아버려서 아래까지 내려오지 않는다.
- catch(ThirdException e) {...} 가 위로 오고 catch(FirstException e) {...}가 아래로 와야 오류가 나지 않는다.

### 3.3. finally
- try 구문에 들어오면 finally 구문은 무조건 실행된다.

### 3.4. finally 구문의 사용의 예
![image](https://user-images.githubusercontent.com/106478906/235839414-89765945-c1e7-49f0-8cb6-c078d0d474a7.png)

- file을 한번 열었으면 꼭 close메소드로 닫아주어야 한다.
  - 이처럼 실행의 흐름이 try 구문 안에 들어왔을 때 반드시 실행해야 하는 문장을 finally 구문에 둘 수 있다. 
하지만 이렇게 finally 구문에 넣으면 또 IOException이 발생해서 try catch문이 finally 구문 안에 들어가게 된다. 이보다 멋진 대안이 등장했다!

### 3.5. try-with-resources
![image](https://user-images.githubusercontent.com/106478906/235840219-2be8205b-9106-46f9-bd31-7dca64cefe9b.png)

- 파일(자원)들은 기본적으로 열고 닫는 과정이 있다.
- 리소스를 처리하기 위한 코드를 try와 합쳐놨다는 뜻.

# Chapter 19

## 1. 자바 가상머신의 메모리 모델

### 1.1. 운영체제 입장에서 자바 가상머신
- 운영체제의 관점에서는 가상머신도 그냥 프로그램의 하나
- 운영체제가 일반 프로그램에게 4G의 메모리 공간을 할당해준다면, JVM에게도 4G 메모리 공간을 할당해준다. 
- 자바 프로그램이 두 개 실행되면, 가상머신도 두 개가 실행된다. 이는 메모장을 두 번 띄우면 두 개의 메모장 프로그램이 실행되는 이치와 같다.

### 1.2. 자바 가상머신의 메모리 모델
- 메모리 공간 활용의 효율성을 높이기 위해 메모리 공간을 세 개의 영역으로 구분하였다.
![image](https://user-images.githubusercontent.com/106478906/235841086-e09ce696-80a3-44fd-a756-d3ebc79b6fe7.png)

> 메소드 영역 (Method Area)
- (메소드의) 바이트코드, static 변수
  - 한번 메소드 영역에 할당되면 프로그램이 종료될 때까지 지우지 않는 특성을 가졌다.
  
> 스택 영역 (Stack Area)
- 지역변수, 매개변수

> 힙 영역 (Heap Area)
- 인스턴스

### 1.3. 메소드 영역
![image](https://user-images.githubusercontent.com/106478906/235842232-49352559-fa73-41a7-bebf-763344725c57.png)
- 바이트코드와 static 변수가 할당되는 메모리 공간
- 이 영역에 저장된 내용은 프로그램 종료 시 소멸된다.

### 1.4. 스택 영역
![image](https://user-images.githubusercontent.com/106478906/235842646-35be5bb6-e4ae-4119-8654-b59c31e7f94a.png)
- 임시 저장
- 지역변수 매개변수 할당되는 영역
- 이 영역에 저장된 변수는 해당 변수가 선언된 메소드 종료 시 소멸된다.

### 1.5. 힙 영역
![image](https://user-images.githubusercontent.com/106478906/236108586-42f79c71-4a55-4693-9d59-492796aa2ea3.png)

- 인스턴스가 저장되는 영역
- 스택에 존재하는 참조변수가 힙에 존재하는 인스턴스를 참조한다.
- 가비지 컬렉션의 대상이 되는 영역이다.(JVM)
  - 아무도 참조하지 않는다는 확신이 있을때 조심스럽게 지우기 위해서 힙 영역에 별도로 존재한다.
 
### 1.6. 자바 가상머신의 인스턴스 소멸 시기
![image](https://user-images.githubusercontent.com/106478906/236108766-1c09a43f-96ab-4753-8dfb-3df11764fd3f.png)
- 참조 관계가 끊어진 인스턴스는 접근이 불가하므로 가비지 컬렉션의 대상이 된다.

## 2. Object 클래스
- 모든 자바 클래스의 최상위 클래스

### 2.1. Object 클래스의 finalize 메소드
~~~java
  protected void finalize() throws Throwable
~~~
- 실무에서 잘 사용되지는 않는다.
- Object 클래스에 정의되어 있는 이 메소드는 JVM에 의해 인스턴스 소멸 시 자동으로 호출이 된다. 
  - 가비지 컬렉션을 하면 프로그램이 느려지기 때문에 힙이 견딜수 있다면 안하는게 좋고 JVM이 알아서 조절해서 가비지 컬렉션을 한다.
- 자식 클래스에서 오버라이딩 할 수 있다. 
- 호출이 될수도 있고 안될수도 있다.
  - ex) 프로그램이 종료될 경우에는 굳이 가비지 컬렉션을 하지 않고 종료된다.
-  object 메소드를 오버라이딩해서 object 클래스의 다른 메소드가 가려지면 안되니까 finalize로 object 클래스의 메소드 호출하고 다른거 실행
(끼워넣기 오버라이딩 - 기존의 것을 최대한 건드리지 않기 위함)
- System.gc(); : gc 체크해달라고 부탁
- System.runFinalization(); : gc 실행해달라고 부탁

### 2.2. 인스턴스의 비교: equals 메소드
- '==' : 참조 대상을 비교
- 인스턴스의 내용 비교를 위한 기능을 equals 메소드에 담아 정의한다.
- equals는 Object 클래스의 메소드이다.

### 2.3. String 클래스의 equals 메소드
- String 클래스는 내용 비교를 하는 형태로 equals 메소드를 오버라이딩 하고 있다.

### 2.4. 인스턴스 복사: clone 
- Object 클래스에 정의되어 있는 clone 메소드가 호출되면 인스턴스의 복사가 이뤄진다. 
- 클래스 정의 시, clone 메소드의 호출을 허용하려면 Cloneable 인터페이스를 구현해야 한다.
- Cloneable 인터페이스는 구현해야 할 추상 메소드가 없는 마커 인터페이스이다.

![image](https://github.com/izzy1202/TIL/assets/106478906/92a1d2df-2dcc-42f8-8d65-29fb90108a0d)

### 2.5. Shallow Copy(얕은 복사)
- 깊이 있게 참조값까지 복사하는 게 아니라 얕게 복사

### 2.6. Deep Copy(깊은 복사)
- 복사하고 바로 반환이 아니라 참조값까지 clone메소드로 복사
![image](https://github.com/izzy1202/TIL/assets/106478906/85081f21-30e1-4f73-8f83-0f4b0ddb3c9c)

### 2.7. 
~~~java
class Point implements Cloneable {
  ....
  @Override
  public Point clone() throws CloneNotSupportedException {
  return (Point)(super.clone());
  }
}

Point org = new Point(1, 2);
Point cpy = org.clone(); // 형 변환 필요 없음
~~~
- 원래라면 해야하는데 이제 형변환 안해도 됨

# Chapter 20

## 1. 래퍼 클래스 (Wrapper 클래스) 

### 1.1. 기본 자료형의 값을 감싸는 래퍼 클래스
- 값을 인스턴스화 시켜서 인스턴스를 호출하면 값을 전달한다.
~~~java
class UseWrapperClass {
  public static void showData(Object obj) { //인스턴스를 요구하는 메소드 이 메소드를 통해서 정수나 실수를 출력하려면 해당 값을인스턴스화 해야 한다.
  System.out.println(obj);
}
  public static void main(String[] args) {
    Integer iInst = new Integer(3);
    showData(iInst);
    showData(new Double(7.15));
  }
}
~~~

### 1.2. 래퍼 클래스의 종류와 생성자
![image](https://github.com/izzy1202/TIL/assets/106478906/32abfe7c-7fff-4d3e-bc6b-34a0ac05abbd)
- Double은 float까지 커버 가능하기 때문에 public Double(float value)의 형태는 없다.

### 1.3. 래퍼 클래스의 두 가지 기능
![image](https://github.com/izzy1202/TIL/assets/106478906/02fa9a0a-0b55-4c96-9d62-3992af3de845)

- Boxing : 기본 자료형 값을 인스턴스화 하는 것
- Unboxing : 인스턴스에 저장된 값을 꺼내는 것
  - 꺼냈다고 사라지는 게 아님! 여러개 꺼낼 수 있음

### 1.4. 박싱과 언박싱 예
~~~java
public static void main(String[] args) {
  Integer iObj = new Integer(10); // 박싱
  Double dObj = new Double(3.14); // 박싱
  . . . .

  int num1 = iObj.intValue(); // 언박싱
  double num2 = dObj.doubleValue(); // 언박싱
  . . . .

  // 래퍼 인스턴스 값의 증가 방법
  iObj = new Integer(iObj.intValue() + 10);
  dObj = new Double(dObj.doubleValue() + 1.2);
  . . . .
}
~~~
- 박싱은 인스턴스 생성을 통해 이뤄지고, 언박싱은 메소드 호출을 통해 이뤄진다.
- 래퍼 클래스의 인스턴스는 immutable 인스턴스(내부 값을 수정할 수 없는)이다.
  - String 인스턴스 : immutable 인스턴스
- 연산을 하려면 값을 꺼내서 연산하고 그 값으로 새로운 인스턴스를 만들어야 한다.(효율적이라고는 못함)

### 1.5. 언박싱 메소드의 이름
![image](https://github.com/izzy1202/TIL/assets/106478906/746804f6-fa59-4b52-97ff-033a6f2744e1)

### 1.6. 오토 박싱과 오토 언박싱
~~~java
class AutoBoxingUnboxing {
  public static void main(String[] args) {
  Integer iObj = 10; // 오토 박싱 진행 -> 인스턴스가 와야 할 위치에 기본 자료형 값이 오면 오토 박싱 진행
  Double dObj = 3.14; // 오토 박싱 진행
  . . . .
  
  int num1 = iObj; // 오토 언박싱 진행 -> 기본 자료형 값이 와야 할 위치에 인스턴스가 오면 오토 언박싱 진행
  double num2 = dObj; // 오토 언박싱 진행
  . . . .
  }
}
~~~
  
### 1.7. 오토 박싱, 오토 언박싱의 또 다른 예
~~~java
public static void main(String[] args) {
Integer num = 10;
num++; // new Integer(num.intValue() + 1); -> 오토 박싱과 오토 언박싱 동시에 진행!
. . . .
num += 3; // new Integer(num.intValue() + 3); -> 오토 박싱과 오토 언박싱 동시에 진행!
. . . .
int r = num + 5; // 오토 언박싱 진행
Integer rObj = num - 5; // 오토 언박싱 진행
. . . .
}
~~~
- but, 실제 프로그래머들은 num++; 보다 명확한 오른쪽 코드를 쓰는 경우도 있다.

### 1.8. Number 클래스
- java.lang.Number : 모든 래퍼 클래스가 상속하는 클래스
- java.lang.Number에 정의된 추상 메소드들
> public abstract int intValue()
> 
> public abstract long longValue()
> 
> public abstract double doubleValue()
→ 즉 래퍼 인스턴스에 저장된 값을 원하는 형의 기본 자료형 값으로 반환할 수 있다.

### 1.9. 래퍼 클래스의 다양한 static 메소드들
![image](https://github.com/izzy1202/TIL/assets/106478906/3c4f4b3f-68af-4b77-9556-bb70d7ba5bbf)

# 2. BigInteger 클래스와 BigDecimal 클래스
- BigInteger : 가장 큰 정수형인 Long보다 큰 정수를 표현할 때
- BigDecimal : 오차를 발생시키지 않는 실수 연산할 때(일반 실수형보다 느리기 때문에 무조건적 사용 지양)

## 2.1. 매우 큰 정수 표현 위한 java.math.BigInteger 클래스
- BigInteger 클래스를 기반으로 만드는 인스턴스는 immutable 인스턴스이다.
- 문자열로 표현해야 BigInteger 클래스로 인식된다.








