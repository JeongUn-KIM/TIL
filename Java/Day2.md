# Day 2

## 제어문

### 1. 조건문 (if문, switch 문)

#### + if/else 문

+ if 문

```java
if (조건) {
    조건 true 시, 실행 명령문
} // false 일 경우 무시
```

+ if/else 문

```java
if (조건) {
    조건 true 시, 실행 명령문
} else {조건 false 시, 실행 명령문}
```

+ else if 문

```java
if (조건 1) {
    조건 1 true 시, 실행 명령문
} else if (조건 2) {
    조건 1 false 조건 2 true 시, 실행 명령문
} else if (조건 3) {
    조건 1,2 false 조건 3 true 시, 실행 명령문
} else { 조건 1,2,3 false 시, 실행 명령문}
```

+ 중첩 if문

```java
if (조건 1) {
    if(조건 2) {조건 1,2 true 시, 실행 명령문}
    else {조건 1 true 조건 2 false 시, 실행 명령문}
}
```



#### + switch/case 문

```java
switch (입력변수) {
    case 값1:
        조건 값이 값1일 때 실행 명령문;
        break;// switch 블록 중단 후 빠져나감
    case 값2:
        조건 값이 값2일 때 실행 명령문;
        break;// switch 블록 중단 후 빠져나감
   	 ...
    default:
        조건 값이 어떠한 case 절에도 해당하지 않을 때 실행 명령문;
        break;
}
```



***

### 2. 반복문 (for문, while문, do-while문)



#### + for문 : 횟수가 정해진 반복 (0번 이상)

***for (초기화; 조건식; 증감식) {반복 실행문;}***

```java 
for(int i = 1 ; i <= 10; i =i+1) {
    Systme.out.println(i);} // 1~ 10 의 정수 출력
```



####  + while문 : 횟수가 정해지지 않은 반복 (0번 이상)

***while (반복 조건식) {반복 실행문;}***

 = 반복 조건식의 결과가 참인 동안 반복적으로 실행코자 하는 명령문

```java
int i = 0;
while(i <5) {
    System.out.println(i+1);
	i++;// 이게 사라지면 결과는 1로 무한루프
}
    Systme.out.println(i); //while문 종료 후 변수 i의 값 = 5
```



#### + do / while문 : 횟수가 정해지지 않은 반복 (1번 이상)

***do{반복 실행문;}***

​	 ***while (반복 조건식);***

= 반복 조건식의 결과가 참인 동안 반복적으로 실행코자 하는 명령문

```java
int i = 11;
	do{
		System.out.println(i = i + 1);
	}
	while (i <= 10);
```



***

### 3. 이동문 (continue문, break문, return문)

#### + continue문

 = for/ while/ do-while 반복문 내부에서 사용하면, 반복 중단하고

블록 처음 문장으로 이동하여 나머지 반복 수행



#### + break문

= for/ while/ do-while 반복문 내부에서 사용하면, 반복 중단하고

블록 다음 문장으로 이동

= switch 블록 내부에서 사용하면, 나머지 문장 무시하고 

블록 다음 문장으로 이동



#### + return문

= 현재 수행중인 메소드 중단 후 main 메소드로 이동



***

#### 실습예제

**1번 :** if/else

국어 영어 수학 점수 3개 총점, 평균(정수, 실수) 

//정수 평균이 80 이상이면  "A" 
// 60 이상이고 80 미만이면 "B"
// 40이상이고 60미만이면 "C"
// 나머지 "낙제"

```java

```

**2번 : ** switch/case/break

3의 배수 여부 판단 

```java
```

**3번 :** for 

순서대로 1~10까지 출력

```java

```

역순으로 10~1까지 출력

```java

```

순서대로 10부터 1씩 증가 무한루프

```java
```

순서대로 1부터 10까지의 총합

```java
```

구구단 2단~9단 출력

```java
```

소수 여부 판단

```java
```

StarTest

//10*10개의 별 출력  = 사각형모양

```java
```

//직각 삼각형 모양 출력

```java

```

//정삼각형모양 출력

```java
```

1~100 사이의 홀수의 합계

```java
public class Coutinue {

    public static void main(String[] args) {

        int sum = 0;

        for (int i = 1; i <= 100; i++) {
            if (i % 2 == 0) {
                continue;
            }
            sum += i;
        }

        System.out.println("sum=" + sum);
    }
}
```

**4번 : **return 예제

```java
```

