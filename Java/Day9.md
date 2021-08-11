# IO 기반 입출력 및 네트워킹

### 1. 입출력

 : 자바 프로그램의 외부 환경으로부터 데이터를 서로 전달하는 과정이다

ex) 키보드 입력, 모니터 출력, 파일 입/출력, 메모리 입/출력, ...



### 2. java.io 패키지

|                         | 입력 용도 클래스                       | 출력 용도 클래스 |
| ----------------------- | -------------------------------------- | ---------------- |
| 2byte = 문자단위 입출력 | Reader<br />FileReader, BufferedReader | Writer           |
| 4byte = byte단위 입출력 | FileInputStream                        | OutputStream     |

> File 클래스 - 입출력 기능 없다. 파일이나 디렉토리 크기, 리스트 목록, 파일 저장 경로, ...



```java
class Reader{ 메소드 정의 }
class FileReader extends Reader { 자동포함 + 오버라이딩 메소드 + 추가메소드 }

class InputStream{ 메소드 정의 }
class FileInputStream extends InputStream { 자동포함 + 오버라이딩 메소드 + 추가메소드 }

// 이런식으로 상속하는 형태가 된다
```



#### 2-1. InputStream / Reader 메소드

| read()                                                       | 입력(1byte, 2byte)                                           |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **close()**                                                  | **입력 종료 파일 반납 문장**                                 |
| **InputStream<br />read(byte b[])** <br />//1byte씩 입력한 데이터를  b 배열에 저장 | **Reader<br />read(char b[])**<br />// 2byte씩 입력한 문자데이터를 b매열에 저장 |

#### 2-2. OutputStream / Writer 메소드

| write(int i)                                                 | 출력(1byte, 2byte)                                           |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **close()**                                                  | **출력 종료 파일 반납 문장**                                 |
| **OutputStream<br />write(byte b[])** <br />**//byte 배열 b에 저장한 내용 출력 | **Writer<br />write(char b[])<br />**//char 배열 b에 저장한 내용 출력<br />**write(String s)<br />**//String s에 저장한 내용 출력 |

### 3. 콘솔 입출력

키보드입력 = 표준입력 = System.in.read()

모니터출력 = 표준출력 = System.out.print()

+ System.out.print()

  + System 클래스 : java.lang 패키지. 자바 실행 컴퓨터에 대한 여러 정보 제공 클래스
  + System.out 변수 : 자바 실행 컴퓨터의 모니터 장치 변수. 
  + System.in 변수 : 자바 실행 컴퓨터의 키보드 장치 변수. 
  + System.out.print() 메소드 : java.io.PrintStream(write(),close()) 클래스 포함 출력

+ System.in.read() : 1byte만 표현 가능 / 데이터타입 변환 불가능

  : 키보드 => 자바 프로그램

  

+ **java.util.Scanner 클래스**

   : 키보드 입력 데이터를 자바 데이터 타입 변환 입력 역할

  : 키보드 => Scanner객체로 타입변환 => 자바 프로그램

  + 생성자

  Scanner s = new Scanner(System.in);

  + 메소드

  int <= s.nextInt() = 정수타입 변환 입력

  double d <= s.nextDouble() = 실수타입 변환 입력

  boolean <= s.nextBoolean() = 논리값타입 변환 입력

  String1 <= s.next() = 1개 단어 문자열 String 변환 입력

  String2 <= s.nextLine() = 1개 라인 문자열 String 변환 입력

  

### 4. java.io.File : 파일입력 / 파일출력  

+ java.io.File

  : 파일 시스템의 정보 제공 역할

  : 입출력 기능 메소드 존재  x 

  : window 탐색기 기능: 길이, 출력가능파일형태여부 판단

  + 생성자

  File f = new File();

  + 메소드

  f.canRead() / f.canWrite() --> 입력가능(window 파일 기본 입력) / 출력가능

  f.length() --> byte 단위

  f.lastModified() --> 파일을 최근에 수정했던 시각(년 월 일 시 분 초 ====> 1/1000초)

  f.getXXXXPath();

  f.list(); --> 폴더 내부 세부 목록

  f.exists() --> boolean으로 파일 실제 존재 여부 판단



<1byte 파일 입출력>

FileInputStream / FileOutputStream

<2byte 파일 입출력>

FileReader / FileWriter



**<파일 입력>** // read(), close()

```java
FileInputStream fi = new FileInputStream("a,jpg");
while(true){
    int r = fi.read();
    if(r == -1){break;}
}
fi.close(); --> 다른 프로그램이 a.jpg 파일 사용하려고 대기중
```

```java
FileReader fr = new Reader("a.txt");
while(true){
    int r = fr.read(); --> 2바이트
    if(r == -1){break;}
}
fi.close(); --> 다른 프로그램이 a.txt 파일 사용하려고 대기중
```

**<파일 출력>** = 파일로 저장 // write(), close()

```java
FileOutputStream fo = new FileOutputStream("a,jpg");
fo.write(65); --> A
fo.write(66); --> B
    ...
fo.close(); --> 다른 프로그램이 a.jpg 파일 사용하려고 대기중
```

```java
FileWriter fr = new Writer("a.txt");
fw.write(65); --> A
fw.write(66); --> B
    ...
fw.close(); --> 다른 프로그램이 a.txt 파일 사용하려고 대기중
```

### 5. 보조 스트림

InputStreamReader : 1byte 를 2byte로 변환

BufferedReader : 외부 메모리를 내부메모리로 정장하여 필요시 내부에서 뽑아 쓰게 함 - > 입력속도향상

DataInputStream : 자바 데이터타입 변환 입력