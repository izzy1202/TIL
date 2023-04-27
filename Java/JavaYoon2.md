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


