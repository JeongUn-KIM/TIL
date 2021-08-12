**Day 11**

# 데이터베이스_ SQL 문법

> 서로 연관되고 의미있는 데이터들의 모음

+ DBMS : 데이터베이스 관리시스템

  ㄴ RDBMS : 관계형 데이터베이스 관리시스템

  ​	= 데이터 구조를 테이블 형태로 표현하요 보기 쉽게 함 (행과 열)

  ​	= Oracle, MySQL

## SQL 특징

1. 데이터 베이스 언어
2. 대소문자의 구분이 없다     (단, 계정의 암호와 데이터값은 대소문자 구분 o)
3. 오라클 문자열 데이터 값 = '문자열값'
4. 클래스 생성 x 메인 메소드 x
5. SQL 문법에 맞는 문장을 작성하여 실행

## SQL 종류

| Data Query Language<br />DQL              | **select ~**                                          | **조회**                                                     |
| ----------------------------------------- | ----------------------------------------------------- | ------------------------------------------------------------ |
| **Data Definition Language<br />DDL**     | **create table ~<br />Alter table~<br />drop table~** | **테이블 구조 정의<br />테이블 구조 변경<br />테이블 삭제**  |
| **Data Manipulation Language<br />DML**   | **insert ~<br />update~<br />delete~**                | **테이블 내 데이터 저장<br />테이블 내 데이터 수정<br />테이블 내 데이터 삭제** |
| **Transaction Control Language<br />TCL** | **commit~<br />rollback~**                            | **연속 SQL 실행 완료 / 취소<br />트랜잭션 처리**             |
| **Data Control Language<br />DCL**        | **grant~<br />revoke~**                               | **특정 계정에 권한 부여<br />특정 계정의 권한 부여 취소**    |



connect system/system : 시스템 접속

create 사용자명 test identified by 암호;   : test라는 이름의 계정 생성

grant resource, connect to 사용자명;   : test계정에 접근할 수 있는 권한 부여

connect 사용자명; 

show user;   : 현재 계정 확인

disconnect;



### 1. DQL - select(조회)



**<문법>**  [] = 생략가능

- 작성순서

select 컬럼명, 함수명

​	[from 테이블명] 

​	[where = 조회 데이터의 조건식]

​	[group by = 집계함수 적용 기준 컬럼명]

​	[having = 집계함수에 대한 조건식]

​	[order by = 정렬순서 컬럼명]

- 실행순서

  from => where => group by => having =>  select => order by 



*edit;	= 직전 명령어 메모장에서 편집 / 저장 - 닫기 - /(slash)



#### **1-0. 집계함수**

| 집계함수 (= 다중행함수) | 107레코드의 급여 중 1개의 결과만 가져오는 것<br />sum, avg, max, min, count, std(표준편차), variance(분산) |
| ----------------------- | ------------------------------------------------------------ |
| 단일행함수              | select upper(first_name)<br />from employees;<br />=> 107 레코드의 이름 대문자로 변경 |

- sum, avg => 숫자타입 컬럼만

  max, min => 모든타입 컬럼

  count (컬럼명) => 모든타입 컬럼/ not null 데이터의 갯수만 

  count (*) => 모든타입 컬럼/ null 데이터의 갯수 포함 

  

- 급여총합

```oracle
select sum(salary) from employees;
```

- 급여평균

```oracle
select avg(salary) from employees;
```

- 최대/최소급여

```oracle
select max(salary), min(salary) from employees;
```

- 급여 수령 사원 수

```oracle
select count(salary) from employees;
```

- 가장 먼저 입사한 사장님의 입사일자, 가장 최근에 입사한 신입사원의 입사일자

```oracle
select min(hire_date) 사장님의입사일, max(hire_date) 신입사원의입사일 from employees;
```

- 이름 알파벳 순서상 가장 처음/마지막에 오는 이름

```oracle
select min(first_name), max(first_name) from employees;
```

- 이름의 총 합계를 구하시오

```oracle
select sum(first_name) from employees; // error 발생
```

- 모든 사원 수

```oracle
select count(*) from employees;

- 급여 받는 사원수
select count(salary) from employees;

- 부서 속한 사원수
select count(depatement_id) from employees;

- 커미션 받는 사원수
select count(commission_pct) from employees;

-이름이 있는 사원수
select count(first_name) from employees;
```



***

**select + (* | 컬럼명 | as 별칭 | +_/ * | distinct ) **

​	**from 테이블명 (모든 레코드 조회)**



1. 현재 hr 계정의 테이블 목록 중 테이블 이름만 따오는 명령어

```oracle
select tname from tab;
```

2. employee 테이블에서 first_name 열 조회

```oracle 
select first_name from employees;
```

3. 급여 컬럼 - salary 조회

```oracle
select salary from employees;
```

4. 급여 12배 - 연봉 연산식 작성(연봉 컬럼 없음)

```oracle
select salary, salary*12 from employees;
```

5. 실제 컬럼명을 조회 임시 변경 - alias

```oracle
select salary 월봉, salary*12 as 연봉 from employees;
```

6. 직종 코드 종류별 1개 조회(동일 직종 코드 1번만 조회)

```oracle
select distinct job_id from employees;
	   distinct => 중복 제거
```

7. 이름 대문자 변경 조회

```oracle
(자바)ELLEN ---> "Ellen".toUpperCase();
(oracle) select upper(first_name) from employees;
```

***

#### 1-1. Where

> select + (* | 컬럼명 | as 별칭 | +_/ * | distinct ) 
>
> ​	from 테이블명 (only 조건식 만족 레코드) 
>
> ​		where 레코드 조건



**< where 컬럼명 연산자 값; >**

| 비교 연산자          | > , >= , < , <= , < , = , !=(<>)                             |
| -------------------- | ------------------------------------------------------------ |
| **산술연산자**       | **+ , - , * , /  (나머지함수제공)**                          |
| **논리 연산자**      | **and , or , not**                                           |
| **범위 연산자**      | **컬럼명 between A and B**                                   |
| **목록 연산자**      | **컬럼명 in (값1, 값2, ...)**                                |
| **유사패턴 연산자**  | **like , % ,  _  <br />% --> 0개 이상의 아무 문자<br />_ --> 1개의 아무 문자** |
| **null 비교 연산자** | **is null <br />is not null**                                |

* 대소비교 = 사전 나열 순서
  * 숫자 < 영어 대문자 < 영어 소문자 < 특수문자 < 한글/다국어 < 특수문자들
* 날짜 = (이전=작다, 최근=크다) 
  * select sysdate from dual;   = 오라클 현재 날짜 함수
  * select to_char(sysdate , 'yyyy-mm-dd, hh24:mi:ss') from dual;   

+ run sql command line에서 null은 공백으로 출력된다

**비교연산자**

1. employees 테이블 내, 급여 10,000 이상인 사원의 이름과 급여 조회

```oracle
select first_name, salary from employees 
	where salary >= 10000;
```

**범위 연산자**

1. employees 테이블 내, 급여 10,000 이상, 15,000 이하인 사원의 이름과 급여 조회

```oracle
select first_name, salary from employees 
	where salary between 10000 and 15000;
```

**목록 연산자**

employees 테이블 내, 사번 100, 120, 200, 300 사원의 사번 조회 

```oracle
select employee_id from employees 
	where in '100' '120' '200' '300';
```

**날짜, 시각 표시**

1. 입사일자(hire_date)  날짜 시각형식

```oracle
select hire_date from employees 
	where hire_date = '02/06/07';
```

2. 02년도 입사일자

```oracle
select hire_date from employees 
	where hire_date >= '02/01/01'
	and hire_date <= '02/12/31';
```

**유사패턴 연산자**

1. 이름에 'ex' 문자를 포함한 사원의 이름 조회

```oracle
select first_name from employees
	where first_name like '%ex%';
```

2. 이름에 'e'를 포함하되, 3번째에 있는 경우 이름 조회

```oracle
select first_name from employees
	where first_name like '__e%';
```

3. 이름에 'e'를 포함하되, 2개 이상 있는 경우 이름 조회

```oracle
select first_name from employees
	where first_name like '%e%e%';
```

4. 입사년도  02년도 모음

```oracle
select hire_date from employees
	where hire_date like '02%';
select hire_date from employees	
	where hire_date like '02______';
```

**null  비교 연산자**

1. employees 테이블 내, 커미션을 받는 사원 이름 목록

```oracle
select first_name, commission_pct from employees
	where commission_pct is not null;
```

***

#### 1-2. Order by

> 원하는 순서대로 정렬하여 출력
>
> order by [정렬순서] [컬럼명] [asc/desc] [null first/last] ,,,

1. 알파벳 순으로 이름 나열

```oracle
select first_name from employees
	order by first_name;
```

2. 사번순으로 이름 나열

```oracle
select first_name, employee_id from employees
	order by employee_id desc;
```

3. 급여가 가장 많은 사람부터 나열

```oracle
select first_name, salary from employees
	order by salary desc;
```

4. 급여가 가장 많은 사람부터 조회하되, 이름을 알파벳 순으로 나열

```oracle
select first_name, salary from employees
	order by salary desc, first_name ;
```

5. 커미션이 많은 사원부터 조회

```oracle
select commission_pct from employees
	order by commission_pct desc;  --> null 먼저
select commission_pct from employees
	order by commission_pct asc;  --> null 마지막
```

6. 커미션이 많은 사원부터 조회하되, null값 마지막에 조회

```oracle
select commission_pct from employees
	order by commission_pct desc nulls last;
```

7. 커미션이 적은 사원부터 조회하되, null값 먼저 조회

```oracle
select commission_pct from employees
	order by commission_pct nulls first;
```

***

#### 1-3. rownum 과 sample

> rownum : 고정된 결과 추출

1. 랜덤 사원 5개 추출 => 매번 다른 결과

```oracle
select employee_id from employees sample(5);
```

2. 이름을 조회 순서대로 5개 추출 => 항상 고정된 결과

```oracle
select first_name from employees 
	where rownum <= 5;
```

3. 급여 많은 사원부터 5명 추출

```oracle
select rownum, salary from employees
	where rownum <= 5
	order by salary desc;
```

4. 급여 많은 사원부터 전체사원 조회

```oracle 
select rownum, salary from employees
	order by salary desc;
```

- select 실행
  1. from 절 : 테이블 가져온다 (n개 중 1개의 테이블 메모리)
  2. select절 실행 : 컬럼 가져올 때마다 rownum  생성
  3. order by 실행 : 순서 변경 => 이때 2번에서 부여된 rownum은 고정
  4. 결과 : rownum 뒤죽 박죽 가능 => **subquery로 해결**

#### 1-4. group by / having

1. 부서별 급여 총합 조회

```oracle
select sum(salary) from employees
	group by department_id ;

	select first_name, sum(salary) from employees
		group by department_id ; // 불가능
	select department_id, sum(salary) from employees
		group by department_id ; // 가능
	
	=> 집계함수 select시에 다른 컬럼 추가 불가능,
		그러나 group by 뒤의 컬럼명과는 같이 조회 가능
```

​	1-1.  부서별 급여 총합 조회하되, 부서원이 없는 부서 제외(=부서코드 null 제외)

```oracle
select department_id, sum(salary) from employees
	where department_id is not null
	group by department_id ;
```

​	1-2.  부서별 급여 총합 조회하되, 부서원이 없는 부서 제외(=부서코드 null 제외), 급여 총합이 많은 순으로 조회

```oracle
select department_id, sum(salary) from employees
	where department_id is not null
	group by department_id 
	order by sum(salary) desc ;
```

2. 부서별 급여 총합 조회하되, 총합이 10만 이상 조회

```oracle
select department_id, sum(salary) from employees
	group by department_id 
	having sum(salary) >= 100000;
```

### 2. DML

## Oracle의 데이터 형식

| **숫자** | **number**(38)<br />정수 number(5) number(5,0)<br />실수 number(10,2) = 정수8자리, 소수점 2자리<br />        number(2,2) =   .14 |
| -------- | ------------------------------------------------------------ |
| **날짜** | **date<br />기본적 data 타입 형식 = rr/mm/dd<br />년 월 일 시 분 초 요일 값 저장 가능<br />rr   0~49 - 2000년대<br />    50~99 - 1900년대** |
| **문자** | **varchar2(4000)<br />'java' --> 4 byte<br />'가나다' --> 9 byte (한글 1개당 3byte)** |



## Oracle의 내장함수

| 집계함수   | sum, avg,    | max, min, count                                              |
| ---------- | ------------ | ------------------------------------------------------------ |
| 단일행함수 | 문자열함수   | length - 글자수<br />lengthb - byte 수<br />upper/lower - 대/소문자 변경 |
|            | 숫자함수     |                                                              |
|            | 날짜함수     |                                                              |
|            | 타입변환함수 |                                                              |
|            | null처리함수 |                                                              |

### 문자열 함수

dual = 가상의 테이블, select 결과 저장하는 임시 테이블

​			행의 개수 = 1개

#### 1. ascii/ asciistr

```oracle
select ascii('A') from dual;
```

```oracle
select asciistr('가') from dual;
```



#### 2. || / concat 

>  문자열 결합 연산자 / 문자열 결합 함수

+ employees 테이블 내, first_name salary 조회 시, 'XXX사원은 급여 XXX를 받습니다'

```oracle
select first_name ||'사원은 급여 '|| salary ||' 를 받습니다.' 
as 급여정보 from employees;
```

```oracle
select concat( concat( concat(first_name, '사원은 급여 ') ,salary) ,' 를 받습니다.') 
as 급여정보 from employees;
```

#### 3. instr / substr

> 특정 문자열 위치 리턴/ 특정 인덱스 위치에 있는 문자 리턴
>
> instr('Neena', 'na') --> 1번 인덱스
>
> substr('Neena', 1, 2) --> 'Ne'

+ 이름에서 ex가 포함된 인덱스 번호 출력

```oracle
select instr(first_name, 'ex') from employees;
=> 이름에서 ex가 포함된 인덱스 번호 출력

select first_name from employees
	where instr(first_name, 'ex') >= 1;
    // 동일 결과 : where first_name like '%ex%';
```

+ 02년도 입사자 입사일 조회

```oracle
selecthire_date from employees
	where instr (hire_date,'02');

select hire_date from employees
	where substr (hire_date, 1, 2) ='02';
```

#### 4. lower / upper / initcap

```oracle 
select first_name from employees
 where first_name = initcap('neena');
```

#### 5. lpad/ trim, rpad/ trim

> pad = 추가 , trim = 제거 
>
> l = 문자열 가장 왼쪽에 ~ 추가/제거
>
> r = 문자열 가장 오른쪽에 ~ 추가/제거

```oracle
select trim('    java program  ') from dual;
select lpad('java program', 20, '-') from dual;
```

