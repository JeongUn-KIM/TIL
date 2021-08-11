# Day 3

## 참조형 변수

> 기본형 변수는 stack 영역에 실제값을 저장
>
> 참조형 변수는 stack 영역에 주소값을 저장하고 해당 주소를 참조하여 heap 영역에 실제값 저장 

### - String 클래스

+ new 키워드 = 객체 새로 생성시 사용

```java
String a = "Hello Java";
String b = "a";
String c = "123";

String a = new String("Hello Java");
String b = new String("a");
String c = new String("123");
```

### - *.equals 메소드

+ 문자열 값 비교시 반드시 equals 메소드 이용!

```java
String a = "hello";
String b = new String("hello");
System.out.println(a.equals(b));
System.out.println(a==b); //동일 객체가 아니라 false 발생
```



***

## 메모리 구조

> 자바 프로그램이 실행 시, JVM은 운영 체제로부터 프로그램 수행에 필요한 메모리를 할당
>
>  JVM은 할당받은 메모리를 용도에 따라 구분하여 관리

#### 메소드 영역 method

: 클래스 변수와 정보가 저장되는 영역

#### 힙 영역 heap

: new 키워드로 생성된 인스턴스 변수가 저장되는 장소

#### 스택 영역 stack

: 메소드 호출 시, 지역변수와 매개변수가 저장되는 영역

 메소드 호출 완료시 소멸



### - 배열 =  동일 타입의 데이터를 여러개 모은 변수 형태

> ex) int score1, score2, score3, score4, score5;
>
> => int [] score = new int [5];

+ 배열 생성과 선언

  ```java
  타입[] 배열이름 = new 타입[배열길이];
  ```

+ 배열 선언과 초기화

  ```java
  타입[] 배열이름 = new 타입[]{배열요소1, 배열요소2, ...}
  ```



***

## 클래스

+ java는 *객체 지향* 프로그래밍 언어

+ 클래스 멤버부

  + 멤버변수 : 객체의 정적 특성 : 변수 (상태, 정보, 데이터 표현)

  + 멤버 메소드 

  + 생성자 

  + 일반 메소드 

  

+ 접근제어 한정자 modifier

  + public : 모든 클래스에서 객체 생성 가능
  + private : 다른 클래스에서 내부 클래스에서만 객체 생성 가능
  + no modifier : 한정자 없이 선언된 클래스는 같은 패키지 내의 클래스에서만 객체 생성 가능

  

+ final 클래스

  = 상속이 안되는 클래스

+ abstract 클래스

  = 추상클래스 자체로 객체 생성이 불가, 하위 클래스에서 상속을 받아야 함



+ new 키워드, 객체 생성

```java
클래스명 참조변수명 = new 클래스명();
Employee e = new Employee();
```



### 1. 메소드 method

### 2. 생성자

