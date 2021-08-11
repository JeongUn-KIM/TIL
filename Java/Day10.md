# IO 기반 입출력 및 네트워킹

### 6. 네트워크 기초

### java.net 패키지



네트워크 : 물리적인 통신 회선으로 연결된 다른 컴퓨터와의 입출력

1. ip adress : 연결 컴퓨터 식별번호

   ​					인터넷 상 모든 컴퓨터의 고유한 식별번호(중복 x)

   IPv4 주소 . . . . . . . . . : 192.168.35.213

   최대갯수 : 256 * 256 * 256 * 256 개

2. port : 1개의 컴퓨터 동작 프로그램 식별번호 (0 - 65535)

java.net.InetAddress 클래스 - ip

1. IP알아보기

2. 통신

   | tcp 통신방식 (전화방식)                     | udp 통신방식 (우편방식)                               |
   | ------------------------------------------- | ----------------------------------------------------- |
   | java.net.ServerSocket<br />java.netS\.Sockt | java.net.DatagramSocket<br />java.net.DatatgramPacket |

   또는

   이미 구현된 네트워크 방식을 이용하여 통신

   인터넷 = 웹 = http / 파일전송특화 = ftp / 원격접속 = telnet

   tp = protocol = 통신 하는 컴퓨터 사이의 규칙



| 로그인 서버 프로그램                                         | 로그인 클라이언트 프로그램                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1) 서버 시작(port)<br />3) 클라이언트 요청 승인<br />5) 클라이언트가 전송한 아이디와 암호  처리<br />    (가입, 암호 일치 여부, ...)<br />6) 처리결과 클라이언트에 전송 <br />    (정상로그인, 아이디/암호 일치 여부, ...)<br />9) 클라이언트와의 접속 해제 | 2) 서버 접속 요청(서버 ip, port)<br />4) 서버로 로그인 아이디와 암호 전송<br />7) 서버가 전송한 처리결과 이용<br />8) 서버와의 접속 해제 |
| InputStream is = s.getInputStream();<br />is.read(byte[]);<br />바이트 배열 -> String | String --> 바이트 배열 변환 후<br />                         |



```java
1) ServerSocket ss = new ServerSocket(9999);
3) Socket s = ss.accept();
5) byte[] id_byte_server = new byte[100];
    InputStream is = s.getInputStream();
	is.read(id_byte_server);
	String id = new String(id_byte_server);
6) OutputStream os = s.getOutputStream();
	os.write();
9) s.close();
   ss.close();
```



```java
2) Socket s = new Socket(ip, 9999);
4) String id = "multi"; //String 타입의 데이터를
	byte [] id_byte = id.getBytes();// byte 타입으로 변환하여
    OutputStream os = s.getOutputStream();// byte 배열로 서버로 전달
	os.write(id_byte);
7) InputStream is = s.getInputStream();
	____ <= is.read();
8) s.close();
```



+ 예외 사항 

  1) java.net.ConnectException: Connection refused: connect

  => 서버가 아직 시작되지 않았는데 클라이언트가 접속상태 

  =>(해결책) : 서버를 먼저 시작한다

  2. java.net.BindException: Address already in use: JVM_Bind

  => 서버가 이미 시작한 상태에서 서버가 또 실행 상태 (포트번호 중복)

  =>(해결책) : 이미실행중인 1개의 서버만 사용

***

실습예제1. 

​					

| 클라이언트                                        | 서버                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| 키보드<br />아이디 : *multi*<br />암호 : *campus* | LoginServer.java<br />클라이언트가 입력하여 전송한 아이디와 암호를 받아 적합성을 검사한다.<br /><br />HashMap<String, String> users = <br />new HashMap<String, String> ();<br />users.put("multi", "campus");<br />users.put("java", "program");<br />users.put("oracle", "db");<br /><br />users 해당 아이디x => "회원가입부터 하세요" 클라이언트 출력<br />users 해당 아이디o 암호x => "암호를 확인하세요" 클라이언트 출력<br />users 해당 아이디o 암호o => "정상 로그인 사용자입니다" 클라이언트 출력<br /> |

*