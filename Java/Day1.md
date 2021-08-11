# Day 1

## 변수 Variable

> 값을 저장할 수 있는 메모리 공간

+ (데이터 타입)  (변수이름) ;

```java
int a ; // 정수 값을 저장할 수 있는 a 변수 선언
int a = 30 ; // 변수 생성, 선언 + 초기화 (숫자값 저장)
```

+ 변수 이름 규칙
  + 대소문자 구분
  + 숫자로 시작 x
  + 특수문자  only :   _   $
  + 키워드 사용 불가



***

## 데이터 타입 Data Type

### 1. 기본형 	

| **논리값** | boolean    | **true / false** |
| ---------- | ---------- | ---------------- |
| **문자형** | **char**   | **2 byte**       |
| **정수형** | **byte**   | **1 byte**       |
|            | **short**  | **2 byte**       |
|            | **int**    | **4 byte**       |
|            | **long**   | **8 byte**       |
| **실수형** | **float**  | **4 byte**       |
|            | **double** | **8 byte**       |

### 2. 참조형

+ 프로그래머가 직접 만들어 사용가능
+ 정해진 수 x
+ 기본형 = 실제값 저장 / 참조값 = 주소값 저장



***

## 형 변환 Type Conversion(Casting)

> 형변환이란, 하나의 자료형을 다른 자료형으로 변환하는 것을 의미
>
> 컴파일러 판단하의 ***자동 형변환***과 개발자에 의한 ***강제형변화*** 2가지가 있음



### 1. 자동 형 변환 Implicit Conversion

+ byte => short => int => long => float => double

  ​			   char

+ 값의 범위가 작은 타입에서 큰 타입으로의 형 변환은 생략 가능

  (컴파일러가 자동으로 생략된 형변환 실행)

+ boolean은 형변환 x

### 2. 명시적 형 변환 Explicit Conversion

+ 값의 범위가 큰 타입에서 작은 타입으로의 형변환

+ 또는 문자<-> 숫자 간의 형변환에 사용

  + **String to int**

    ```java
    //Integer.parseInt(String값)
    //Integer.valueOf(String값)
    
    String s = "10";
    int i = Integer.parseInt(s);
    int i = Integer.valueOf(s);
    ```

  + **int to String**

    ```java
    //String.valueOf(Int값)
    //Integer.toString(Int값)
    
    int i = 10;
    String s;
    		
    s = String.valueOf(i);
    s = Integer.toString(i);
    ```




***

## 연산자

1. 산술 연산자 

   ```java
   int num1 = 4, num2 = 3, num3 = 2;
       
   System.out.println(num1 + num2); // 7
   System.out.println(num1 - num2); // 1
   System.out.println(num1 * num2); // 12
   System.out.println(num1 / num3); // 2
   System.out.println(num1 % num2); // 1
   ```

2. 대입 연산자

   ```java
   int num1 = 7, num2 = 7, num3 = 7;
   
   num1 = num1 -3;
   num2 -= 3;
   num3 =- 3;
   
   System.out.println(num1); // 4
   System.out.println(num2); // 4
   System.out.println(num3); // -3 (num3에 -3을 대입한 사례)
   ```

3. 증감 연산자

   ```java
   int num1 = 7, num2 = 7;
   int result1;
   int result2;
   
   result1 = --num1 + 4;
   result2 = num2-- + 4;
   
   System.out.println(result1); // 10
   System.out.println(num1); // 6
   System.out.println(result2); // 11 (연산이 끝나고 나서 변수의 값 감소)
   System.out.println(num2); // 6
   ```

4. 비교 연산자

   ```java
   char c1 = '10';
   char c2 = '20';
   
   System.out.println(c1 == c2); // false
   System.out.println(c1 < c2); // true
   System.out.println(c1 != c2); // true
   ```

5. 논리 연산자

   ```java
   char c1 = 'b', c2 = 'B';
   boolean result1, result2;
   
   result1 = (c1 > 'a') && (c1 < 'z') ;
   result2 = (c2 < 'A') || (c2 < 'Z') ;
   
   System.out.println(result1); // true
   System.out.println(result2); // true
   System.out.println(!result2); // false
   ```

6.  삼항 연산자

   ```java
   //조건식 ? 반환값1 : 반환값2
   
   int num1 = 5, num2 = 7;
   int result;
   
    
   result = (num1 - num2 > 0) ? num1 : num2;
   System.out.println(result); // 두 정수 중 더 큰 수는 7
   ```

   

