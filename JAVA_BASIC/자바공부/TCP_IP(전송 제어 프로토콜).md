컴퓨터가 데이터를 교환할 때 서로 통신하는 방식을 관리하는 프로토콜이다.

다른 프로토콜로는 사용자 데이터 그램 프로토콜(UDP) 또는 개방형 시스템 상호 연결(OSI)과 같은

다른 표준도 다양한 상황에서 사용된다.

TCP는 두 개의 호스트를 연결하고 데이터 스트림을 교환하게 해주는 네트워크 프로토콜이며 데이터

와 패킷이 보내진 순서대로 전달하는 것을 보장해준다.

한 컴퓨터에서 다른 컴퓨터로 전송되는 모든 데이터가 오류나 결함 없이 올바른 순서로 성공적으로

수신 되도록 하기 위한 것이다.

TCP는 통신을 수행하기 전에 먼저 두 컴퓨터 간에 세션이 존재하는지 확인해야한다.

### TCP가 두 컴퓨터 간에 연결을 설정하는 방법

- 한 컴퓨터(발신자)가 수신 컴퓨터에게 초기 메시지를 보내 연결 설정을 공식적으로 요청하고 이를 SYN 메시지(동기화)라고 한다.
- 그럼 다음 수신 컴퓨터는 SYN에 대한 승인(SYN-ACK 메시지)을 보내야 한다.
- 마지막으로 발신자가 확인을 승인해야 한다.(수신 확인 메시지라고 한다.)

이 세 단계가 성공적으로 완료되면 데이터 전송을 시작할 수 있다.

TCP는 단순히 통신 채널을 설정하는 데 많은 단계가 필요하며 이것이 UDP기반 연결보다

느린 이유 중 하나 이다.

### TCP의 네 가지 계층

- 애플리케이션 계층 : 이 계층은 웹 브라우저와 같은 애플리케이션이 상호 작용하는 TCP 계층 이다.(애플리케이션 계층에는 HTTPS 및 SMTP와 같은 추가 프로토콜이 포함된다.)
    
- 전송 계층 : 애플리케이션이 웹 브라우저에서 데이터를 수신한 후 포트를 통해 전송 계층과 통신 하는데 웹 브라우저의 경우 80번 포트이며 전송 계층은 수신 된 데이터를 개별 패킷  
    으로 슬라이스 및 다이싱 하여 각각 목적지 까지 가장 빠른 경로로 이동한다. 각 패킷에는 패킷 페이로드 (즉, 전송되는 데이터)를 전달하는 방법에 대한 지침이 포함된 헤더도 함께 제공된다.
    
- 인터넷 계층 : 다음으로 패킷은 이 계층으로 푸시 되며, 이 계층은 인터넷 프로토콜을 사용하여 각 패킷에 출발지 및 목적지 IP 주소를 태그 한다.
    
- 네트워크 계층 : 이 계층은 실제 데이터가 변환되어 외부로 전송되는 계층이다. 네트워크 계층은 미디어 엑세스 제어와 같은 정보를 처리하며 주소를 사용하여 각 패킷이 올바른 컴퓨터로 전달되도록 한다.
    

### TCP를 사용하는 이유

TCP는 전송된 모든 데이터가 오류 없이 도착해야 하는 경우에 사용된다. 실제로 TCP의 본질적인

가치는 전송된 모든 데이터의 무결성을 보장한다는 것이다. 오류가 발생하면 TCP는 데이터를 다시

전송한다.

### TCP와 UDP

TCP의 한 가지 문제점은 특히 공용 인터넷을 통한 지연 시간이다. 이는 데이터 재전송 및 패킷 재정렬

을 포함하여 위에서 언급한 모든 단계에 기인한다.

그렇기 때문에 다른 프로토콜인 UDP가 존재하는데 온라인 게임, 스트리밍, VoIP(voice over IP)

등 빠른 속도가 필요하지만 일부 데이터가 불완전하거나 누락될 수 있는 기타 애플리케이션에

자주 사용된다.

하지만 UDP는 not 연결 지향 프로토콜이다. TCP와 달리 컴퓨터 간에 세션을 설정하거나 전송된

데이터의 무결성을 보장하지 않는다. 따라서 패킷 손실이 흔히 발생할 수 있으며 UDP를 통해

전송되는 각 데이터 패킷은 헤더 정보가 적고, 전송 중에 패킷이 손실 되면 영원히 사라진다.

### 패킷

데이터를 네트워크를 통해 전송되기 위해 더 작은 조각으로 나뉘며, 이러한 작은 조각을 패킷 이라고

하며 다음과 같은 중요한 정보를 포함한다:

- **헤더(Header)**: 패킷의 출발지와 목적지 주소, 패킷 번호, 오류 검출 코드 등 전송에 필요한 제어 정보를 포함한다.
    
- **페이로드(Payload)**: 실제로 전송되는 데이터 조각이다.
    

패킷을 사용하면 큰 데이터를 더 작은 단위로 쪼개어 전송할 수 있어서 네트워크 효율성을 높이고 오류가 발생했을 때 데이터 일부만 재전송할 수 있다.

### 패킷의 구조

**헤더(Header)**:

- **출발지 IP 주소(Source IP Address)** : 패킷을 보낸 컴퓨터의 IP 주소
- **목적지 IP 주소(Destination IP Address)**: 패킷을 받을 컴퓨터의 IP 주소
- **프로토콜(Protocol)**: 어떤 상위 프로토콜(TCP, UDP 등)을 사용하고 있는지 나타냄
- **패킷 번호(Packet Number)**: 데이터가 여러 패킷으로 나뉘어 전송될 때, 각 패킷의 순서를 나타냄
- **제어 정보(Control Information)**: 패킷의 유효성 검사, 오류 검출을 위한 체크섬, 패킷의 수명(TTL, Time to Live) 등 다양한 제어 정보가 포함됨

**페이로드(Payload)**:

- 실제로 전송되는 데이터 조각. 이 부분이 데이터를 담고 있으며, 데이터의 일부분이 패킷의 크기에 맞추어 담긴다.

### 패킷의 전송 과정

패킷은 다음과 같은 과정을 거쳐 전송된다.

**데이터 분할**:

- 큰 데이터를 작은 조각으로 나눈다. ex) 1MB의 파일을 1KB 크기의 패킷으로 나누면 1,024개의 패킷이 생성된다.

**헤더 추가**:

- 각 패킷에 헤더 정보를 추가한다. 이를 통해 각 패킷이 목적지까지 제대로 도착할 수 있게 된다.

**전송**:

- 패킷은 네트워크를 통해 전송된다. 이 과정에서 여러 라우터와 스위치를 거치며 목적지로 향한다.

**수신 및 재조립**:

- 수신 컴퓨터는 도착한 패킷을 모아 원래의 데이터로 재조립한다. 패킷 번호를 참고하여 올바른 순서대로 배열한다.

### 패킷 전송의 장점

**효율성**:

- 네트워크 자원을 효율적으로 사용한다. 패킷이 각기 다른 경로를 통해 전송될 수 있어 네트워크 병목 현상을 줄인다.

**오류 처리**:

- 일부 패킷이 손실되거나 오류가 발생해도, 해당 패킷만 재전송하면 되므로 전체 데이터를 다시 보내지 않아도 됩니다.

**다양한 경로**:

- 패킷은 목적지까지 여러 경로를 통해 전송될 수 있어 네트워크 장애 시에도 데이터를 전송할 수 있다.

### 패킷 전송의 예

### TCP (Transmission Control Protocol):

- **연결 지향(Connection-oriented)**: TCP는 연결 설정 과정을 통해 두 컴퓨터 간에 세션을 수립한다.
- **신뢰성(Reliability)**: 데이터의 무결성을 보장하며, 패킷이 순서대로 도착하도록 한다.
- **오류 수정(Error Correction)**: 손실된 패킷을 재전송하여 데이터의 완전성을 유지한다.

### UDP (User Datagram Protocol):

- **비연결 지향(Connectionless)**: UDP는 연결 설정 없이 데이터를 전송한다.
- **속도(Speed)**: 빠른 전송이 가능하며, 일부 패킷 손실을 허용하는 애플리케이션에 적합하다.
- **오버헤드(Overhead)**: 헤더 정보가 적어 전송 효율이 높다.

### 패킷의 응용

패킷 전송은 다양한 네트워크 통신에서 필수적인 역할을 한다.

- **웹 브라우징**: 웹 페이지를 로드할 때 HTML, 이미지, 스크립트 등의 데이터를 패킷으로 나누어 전송한다.
    
- **이메일**: 이메일 내용과 첨부 파일을 패킷으로 나누어 전송한다.
    
- **비디오 스트리밍**: 비디오 데이터를 작은 패킷으로 분할하여 전송한다. UDP를 통해 지연을 최소화하고 실시간 스트리밍을 가능하게 합니다.
    

패킷은 네트워크 통신의 기본 단위로, 효율적이고 신뢰성 있는 데이터 전송을 가능하게 하며. TCP와 UDP는 각각의 장단점에 따라 다양한 애플리케이션에서 사용됩니다.

네트워크가 서로 연결되려면 IP주소와 port번호가 필요하다.

IP주소로 프로그램들이 통신할 때는 약속된 전송 규약이 있다. 이것을 전소용 프로토콜이라고

하는데 인터넷에서 전송용 프로토콜은 TCP와 UDP가 있다.

```java
import java.net.InetAddress;
import java.net.UnknownHostException;

public class InetAddressEx {
    public static void main(String[] args) {
        try{
            InetAddress local = InetAddress.getLocalHost();
            System.out.println("내 컴퓨터 주소 : " + local.getHostAddress());

            InetAddress[] iaArr = InetAddress.getAllByName("www.naver.com");
            for (InetAddress remote : iaArr) {
                System.out.println("www.naver.com IP 주소 : " + remote.getHostAddress());
            }
        }catch (UnknownHostException ue){
            ue.printStackTrace();
        }
    }
}
```

```java
내 컴퓨터 주소 : 218.38.137.28
www.naver.com IP 주소 : 223.130.200.236
www.naver.com IP 주소 : 223.130.192.247
www.naver.com IP 주소 : 223.130.200.219
www.naver.com IP 주소 : 223.130.192.248
```


네트워킹 : 네트워크 상에서 데이터를 주고 받는 것

TCP네트워킹 : 네트워크 상에서 데이터를 주고 받을 때 TCP(data를 연결하거나 보낼때 신호자체를 어떻게 연결하고 보낼것인가 신호 자체를 어떻게 만들것인가를 정의해놓은것이 프로토콜이다.)규약을 따른다.

IP가지고 연결 작업을 해야 하는데 연결 작업을 하는 프로토콜이 TCP(전송용 프로토콜)이다.

(Trancemission Control Protocol) 상대방이 연결된 상태에서 데이터를 전달한다. - 웹(서버와 클라이언트 간의 전송 응답)

(User Datagram Protocol)

자바는 TCP네트워킹을 위해 java.net패키지에 ServerSorket과 Socket클래스를 제공하고

ServerSoket은 클라이언트의 연결을 수락하는 서버 쪽 클래스 Socket은 클라이언트에서

연결 요청할 때와 클라이언트와 사버 양쪽에서 데이터를 주고 받을 때 사용되는 클래스이다.

### 서버 TCP

ServerSocket을 생성할 때는 바인딩할 Port번호를 지정해야 한다.

서버가 실행되면 클라이언트는 Socket을 이용해서 서버의 IP 주소와 Port번호로 연결 요청을 할 수

있다. 서버가 실행되면 클라이언트는 Socket을 이용해서 서버의 IP주소와 Port번호로 연결 요청을

할 수 있다. ServerSocket은 accept() 메소드로 연결 수락을 하고 통신용 Socket을 생성하고

클라이언트와 서버는 양쪽의 Socket을 이용해서 입출력 스트림으로 데이터를 주고 받게 된다.

TCP서버 프로그램을 개발하려면 우선 ServerSocket 객체를 생성해야 한다.
```java
ServerSoket serverSocket = new ServerSocket(지정할 포트);
or
serverSocket.bind(new InetSoketAddress(지정할 포트));
```

만약 서버 컴퓨터에 여러 개의 IP가 할당되어 있을 경우, 특정 IP에서만 서비스를 하고 싶다면

InetSocketAddress의 첫 번째 매개 값으로 해당 IP를 주면 된다.
```java
ServerSocket serverSocket = new ServerSocket();
serverSocket.bind(new InetSocketAddress("나의 IP", 지정할포트);
```

만약 Port가 이미 다른 프로그램에서 사용 중이라면 BindException이 발생한다. 이 경우에는

다른 Port로 바인딩 하거나 Port를 사용 중인 프로그램을 종료하고 다시 실행하면 된다.

ServerSocket이 생성되었다면 연결 요청을 수락을 위해 accept() 메소드를 실행해야 한다.

accept()는 클라이언트가 연결 요청하기 전 까지 블로킹(실행을 멈춘 상태)된다.

클라이언트의 연결 요청이 들어오면 블로킹이 해제되고 통신용 Socket을 리턴한다.

```java
Socket socket = serverSocket.accept();
```

만약 리턴된 Socket을 통해 연결된 클라이언트의 IP주소와 Port 번호를 얻고 싶다면 방법은

getRemoteSocketAddress() 메소드를 호출해서 InetSocketAddress를 얻은 다음

getHostName()과 getPort() 메소드를 호출하면 된다.

```java
InetSocketAddress isa = (InetSocketAddress)socket.getRemoteSocketAddress();
//소켓에서 얻은 IP주소이기 때문에 소켓이 하나 더 들어갔다?
String clientIP = isa.getHostName();
String portNo = isa.getPoer();
```

서버를 종료하려면 ServerSocket의 close() 메소드를 호출해서 Port 번호를 언바이딩 시켜야 한다.

그래야 다른 프로그램에서 해당 Port 번호를 재사용할 수 있다.

serverSocket의 역할은 클라이언트 Socket이 연결 요청을 하면 accept()로 연결 수락을 하는 역할을 한다.

```java
import java.io.IOException;
import java.net.InetAddress;
import java.net.InetSocketAddress;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Scanner;

public class SeverExample {
    private static ServerSocket serverSocket; // ServerSocket 객체를 static 필드로 선언

    public static void main(String[] args) {
        //TCP 서버 시작
        startServer();

        System.out.println("---------------------------------------------");
        System.out.println("서버를 종료하려면 q또는 Q를 입력하고 Enter키를 입력하세요");
        System.out.println("---------------------------------------------");
        Scanner scanner = new Scanner(System.in);

        while (true){
            System.out.print(":");
            String command = scanner.nextLine();
            //command가 어떤 형태의 문자이든 소문자로 변경하고 소문자로 변경된 문자가 q이면 종료
            if(command.toLowerCase().equals("q")){
                break;
            }
        }
        //JVM이 종료되면 scanner도 종료되지만 24시간 작동하는 프로그램은 입출력을 위해서 사용한 객체들은 안쓰면 종료를 확실히 해주는것이 좋다.
        scanner.close();
        stopServer();
    }

    public static void startServer() {
        // 작업 스레드 정의 (멀티 스레드)
        Thread thread = new Thread() {
            //Tread 객체에 있는 run메서드 재정의
            public void run() {
                try{
                    //SeverSocket 생성 및 Port 바인딩
                    serverSocket = new ServerSocket(20000);
                    System.out.println("Start Server");

                    while (true){
                        System.out.println("\n [서버] 연결 요청을 기다림 \n");
                        Socket socket = serverSocket.accept();
                        //연결된 클라이언트 정보 얻기
                        InetSocketAddress isa = (InetSocketAddress) socket.getRemoteSocketAddress();
                        System.out.println("isa : " + isa);

                        //클라이언트 ip는 접속 추적을 위해 서버에 저장하여야 한다.
                        String clientIp = isa.getHostString();
                        System.out.println("clientIp : " + clientIp);
                        System.out.println("[서버] " + clientIp + "의 연결 수락함");
                    }

                }catch (IOException ie){
                    //ie.printStackTrace();
                    System.out.println("서버 : " + ie.getMessage());
                }
            }
        };
        thread.start();
    }

    public static void stopServer() {
        try{
            System.out.println("Stop Server");
            //SercerSocket을 닫고 Port 언바인딩
            serverSocket.close();
        } catch (IOException ie){

        }
    }

}

```


### TCP클라이언트

클라이언트가 서버에 연결 요청을 하려면 Socket객체를 생성할 때 생성자 매개값으로 서버 IP주소와

Port번호를 제공하면 된다. 로컬 컴퓨터에서 실행하는 서버로 요청을 할 경우에는 IP주소 대신

localhost를 사용할 수 있다.

```java
Socket socket = new Socket("IP", 클라이언트가 연결 요청할 서버 Port)
```

만약 IP주소 대신 도메인 이름을 사용하고 싶다면, DNS에서 IP 주소를 검색할 수 있도록 생성자

매개값으로 InetAddress를 제공한다.

```java
Socket socket = new Socket(inetAddress.getByName("domainName"),연결 요청할 서버 Port)
```

연결 요청 시 두 가지 예외가 발생할 수 있다. UnknownHostException은 IP 주소가 잘못 표기되었을

때 발생하고, IOException은 제공된 IP와 Port번호로 연결할 수 없을 때 발생한다. 따라서 두 가지

예외를 모두 처리해야 한다.

```java
try{
	Socket socket = new Socket("IP", 클라이언트가 연결 요청할 서버 Port)
	} catch (UnknownHostException ue){
		// IP 표기 방법이 잘못되었을 경우
	} catch (IOException ie){
		// IP와 Port로 서버에 연결할 수 없는 경우
	}
```

서버와 연결된 후에 클라이언트에서 연결을 끊고 싶다면 Socket의 close( ) 메소드를 다음과 같이

호출하면 된다.

```java
socket.close();
```

```java
import java.net.Socket;
import java.net.UnknownHostException;
import java.io.IOException;

public class ClientExample {
    public static void main(String[] args)  {
        try {
            Socket socket = new Socket("localhost", 20000);
            System.out.println("Connected to server");

            socket.close();
            System.out.println("Connection closed");
        } catch (UnknownHostException uh){
            // IP 또는 도메인이 잘못입력되었을 경우
            System.out.println("Unknown host err : " + uh.toString());
        } catch (IOException ie){
            // IP 또는 Port 번호가 존재하지 않을 경우
            System.out.println("IOException err : " + ie.toString());
        }
    }
}

```

### 입출력 스트림으로 데이터 주고 받기

클라이언트가 연결 요청(connect())을 하고 서버가 연결 수락(accept()) 했다면, 다음 그림과

같이 양쪽의 Socket 객체로부터 각각 입력 스트림(inputStream)과 출력 스트림(OutputStream)을 얻을

수 있다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/ea204791-94b0-4594-95e9-37705edf8245/4be7debc-2cc7-487f-83b4-ad015f77dd8c/Untitled.png)

```jsx
InputStream = socket.getInputStream();
outputStream = socket.getOutputStream();
```

상대방에게 데이터를 보낼 때에는 보낼 데이터를 byte[ ] 배열로 생성하고, 이것을 매개 값으로

해서 OutputStream의 write( ) 메소드를 호출하면 된다.

```jsx
String data = "보낼 데이터";
byte[] bytes = data.getBytes("UTF-8");
OutputStream outputStream = socket.getOutputStream();
outputStream.write(bytes);
outputStream.flush();
```

문자열로부터 UTF - 8로 인코딩한 바이트 배열을 얻어내고, wirte( )메소드로 전송한다.

문자열을 좀 더 간편하게 보내고 싶다면 보조 스트림인 DataOutputStream을 연결해서 사용하면

된다.

```jsx
String data = "보낼 데이터";
DataOutputStream dos = new DataOutputStream(socket.getOutputStream());
dos.writeUTF(data);
dos.flush();
```

데이터를 받기 위해서는 받은 데이터를 저장할 byte[ ] 배열을 하나 생성하고, 이것을 매개 값으로

해서 InputStream의 read( ) 메소드를 호출하면 된다. read( ) 메소드는 읽은 데이터를 byte[ ] 배열에

저장하고 읽은 바이트 수를 리턴 한다.

```jsx
byte[] bytes = new byte[1024];
InputStream inputStream = socket.getinputStream();
int num = inputStream.read(bytes);
String data = new String(bytes, 0, num, "UTF-8");
```

받은 데이터가 문자열이라면 byte[ ] 배열을 UTF-8로 디코딩해서 문자열로 얻을 수 있다.

문자열을 좀 더 간편하게 받고 싶다면 보조 스트림인 DataOutputStream을 연결해서 사용하면

된다. 단 이 방법은 상대방이 DataOutputStream으로 문자열을 보낼 때만 가능하다.

```java
DataInputStream dis = new DataInputStream(socket.getInputStream());
String data = dis.readUTF();
```

```java
package JavaStandardExample.TCP.Echo;

import java.io.*;
import java.net.Socket;
import java.net.UnknownHostException;
import java.util.Scanner;

public class EchoClient {
    public static void main(String[] args)  {
        try {
            Socket socket = new Socket("localhost", 20000);
            System.out.println("Connected to server");

            Scanner scanner = new Scanner(System.in);
            DataOutputStream dos = new DataOutputStream(socket.getOutputStream());
            DataInputStream dis = new DataInputStream(socket.getInputStream());

            //데이터 보내기
            while (true){
                System.out.println();
                System.out.println("클라이언트를 종료하려면 q또는 Q를 입력하고 Enter키를 입력하세요");
                System.out.print("Client : ");
                String sendMessage = scanner.nextLine();
                
                if(sendMessage.toLowerCase().equals("q")){
                    socket.close();
                    System.out.println("Consnection closed");
                    break;
                }
                dos.writeUTF(sendMessage);
                dos.flush();
                System.out.println("[클라이언트] 데이터 보냄 : " + sendMessage);

                //데이터 받기
                String readMassage = dis.readUTF();
                System.out.println("[클라이언트] 데이터 받음 : " + readMassage);
            }


        } catch (UnknownHostException uh){
            // IP 또는 도메인이 잘못입력되었을 경우
            System.out.println("Unknown host err : " + uh.toString());
        } catch (IOException ie){
            // IP 또는 Port 번호가 존재하지 않을 경우
            System.out.println("IOException err : " + ie.toString());

        }

    }
}

```


```java
package JavaStandardExample.TCP.Echo;

import java.io.*;
import java.net.InetSocketAddress;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Scanner;

public class EchoServer {
    private static ServerSocket serverSocket;

    public static void main(String[] args) {
        startServer();

        System.out.println("---------------------------------------------");
        System.out.println("서버를 종료하려면 q또는 Q를 입력하고 Enter키를 입력하세요");
        System.out.println("---------------------------------------------");
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.print(":");
            String command = scanner.nextLine();
            if (command.equalsIgnoreCase("q")) {
                break;
            }
        }

        scanner.close();
        stopServer();
    }

    public static void startServer() {
        Thread thread = new Thread(() -> {
            try {
                serverSocket = new ServerSocket(20000);
                System.out.println("Start Server");

                while (true) {
                    System.out.println("\n[서버] 연결 요청을 기다림\n");
                    Socket socket = serverSocket.accept();
                    InetSocketAddress isa = (InetSocketAddress) socket.getRemoteSocketAddress();
                    System.out.println("[서버] " + isa.getHostString() + "의 연결 수락함");

                    new ClientHandler(socket).start();
                }
            } catch (IOException ie) {
                System.out.println("서버: " + ie.getMessage());
            }
        });
        thread.start();
    }

    public static void stopServer() {
        try {
            System.out.println("Stop Server");
            serverSocket.close();
        } catch (IOException ie) {
            System.out.println("서버 종료 오류: " + ie.getMessage());
        }
    }

    private static class ClientHandler extends Thread {
        private final Socket socket;

        public ClientHandler(Socket socket) {
            this.socket = socket;
        }

        @Override
        public void run() {
            try (DataInputStream dis = new DataInputStream(socket.getInputStream());
                 DataOutputStream dos = new DataOutputStream(socket.getOutputStream())) {

                while (true) {
                    String message = dis.readUTF();
                    if (message.equalsIgnoreCase("q")) {
                        System.out.println("Client disconnected");
                        break;
                    }
                    dos.writeUTF(message);
                    dos.flush();
                    System.out.println("[서버] 받은 데이터를 다시 보냄 : " + message);
                }
            } catch (IOException e) {
                System.out.println("클라이언트 통신 오류: " + e.getMessage());
            } finally {
                try {
                    socket.close();
                } catch (IOException e) {
                    System.out.println("소켓 닫기 오류: " + e.getMessage());
                }
            }
        }
    }
}

```

```java
Connected to server

클라이언트를 종료하려면 q또는 Q를 입력하고 Enter키를 입력하세요
Client : 안녕하세요
[클라이언트] 데이터 보냄 : 안녕하세요
[클라이언트] 데이터 받음 : 안녕하세요

클라이언트를 종료하려면 q또는 Q를 입력하고 Enter키를 입력하세요
Client : 저는 Java로 TCP를 공부하고 있습니다.
[클라이언트] 데이터 보냄 : 저는 Java로 TCP를 공부하고 있습니다.
[클라이언트] 데이터 받음 : 저는 Java로 TCP를 공부하고 있습니다.

클라이언트를 종료하려면 q또는 Q를 입력하고 Enter키를 입력하세요
Client : 정말 재미 있습니다.
[클라이언트] 데이터 보냄 : 정말 재미 있습니다.
[클라이언트] 데이터 받음 : 정말 재미 있습니다.

클라이언트를 종료하려면 q또는 Q를 입력하고 Enter키를 입력하세요
Client : q
Consnection closed
```