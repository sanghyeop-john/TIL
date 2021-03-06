# Java Network

> Mon Jun 20, 2022

---

> TCP - 전화처럼 연결
>
> UDP - TV, 라디오처럼 한쪽에서만 송출

[toc]

통신을 위해서는 IP 가 있어야 하며 IP 하나에 2^16 (65535) 개의 Port 가 있습니다. 



* Terminal 에서 IP Address 확인하기

`ipconfig getifaddr en0`



`java.net.ServerSocket` : Client 가 접속하기를 기다리는 클래스

서버에서 `ServerSocker` 객체를 만들어놔야 합니다.

Socket 이 접속을 하는데 IP Address 와 Port 번호가 있어야 합니다.



### InetAddress

InetAddress 클래스를 사용해서 IP Address 를 객체로 만들어야합니다.

```java
import java.net.InetAddress;

public class InetAddressTest {

	public InetAddressTest() {
		
	}
	public void start() {
		try {
			// ip 에 관련된 객체를 생성한다. 
			// 내컴퓨터의 아이피정보 얻어오기.
			InetAddress ia = InetAddress.getLocalHost();
			String ip = ia.getHostAddress(); // 내컴퓨터 ip
			String name = ia.getHostName(); // 컴퓨터이름 또는 url 주소
			System.out.println("ia.address->"+ip);
			System.out.println("ia.name->"+name);
			
			// 도메인 이용한 InetAddress 를 얻어오기
			InetAddress ia2 = InetAddress.getByName("www.google.com");
			System.out.println("ia2.address->"+ia2.getHostAddress());
			System.out.println("ia2.name->"+ia2.getHostName());
			
			// 아이피를 이용한 InetAddress 를 얻어오기
			InetAddress ia3 = InetAddress.getByName("223.130.195.200");
			System.out.println("ia3.address->"+ia3.getHostAddress());
			System.out.println("ia3.name->"+ia3.getHostName());
			
			System.out.println("---------------------------------------------");
			
			// 여러개의 InetAddress 객체 얻어오기 
			InetAddress[] ia4 = InetAddress.getAllByName("www.google.com");
			for(InetAddress i : ia4) {
				System.out.println("ia4.address->"+i.getHostAddress());
				System.out.println("ia4.name->"+i.getHostName());
			}
			
		}catch(Exception e) {
			e.printStackTrace();
		}
		
	}

	public static void main(String[] args) {
		InetAddressTest it = new InetAddressTest();
		it.start();

	}

}
```



### URL



```java
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URL;
import java.net.URLConnection;

public class URLTest {

	public URLTest() {
		
	}
	public void start() {
		try {
			URL url = new URL("https://www.seoul.go.kr/main/index.jsp");
			System.out.println("protocol->"+ url.getProtocol());
			System.out.println("port->"+ url.getPort());
			System.out.println("host->"+ url.getHost());
			System.out.println("path->"+ url.getPath());
			System.out.println("file->"+ url.getFile());
			//-------인코딩 코드-------------------------------------------
			// URL Connection 객체를 통해 header 정보를 얻어올수 있다.
			URLConnection connection = url.openConnection();
			connection.connect(); // 채널확보하여 헤더정보 가져오기
			String header = connection.getContentType();
			// System.out.println(header);
			String encode = header.substring(header.indexOf("=")+1); // UTF-8, euc-kr
			
			//----------------------------------------------------------
			
			InputStream is = url.openStream(); //byte 단위
			InputStreamReader isr = new InputStreamReader(is, encode); //문자 단위
			BufferedReader br = new BufferedReader(isr); // 한줄 단위 
			
			File f = new File("/Users/myname/testFolder/seoul.html");
			FileWriter fos = new FileWriter(f);
			BufferedWriter bw = new BufferedWriter(fos);
			
			String inData="";
			while((inData = br.readLine()) != null) {
				System.out.println(inData);
				bw.write(inData+"\n");
			}
			
			
		}catch(Exception e) {
			e.printStackTrace();
		}
	}

	public static void main(String[] args) {
		URLTest ut = new URLTest();
		ut.start();

	}

}
```



### ServerSocket - TCP 방식

스레드 없이 일회성으로 클라이언트가 서버를 통해 메세지를 보내기

**클라이언트**

```java
import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.InetAddress;
import java.net.Socket;

// 클라이언트
public class SocketTest {
	Socket s;
	public SocketTest() {
		try {
			InetAddress ia = InetAddress.getByName("나의 IP 주소"); //   
			s = new Socket(ia, 10000); // 서버에 접속됨 
			System.out.println("Connected to server");
			
			// 서버에서 보낸 문자 받기
			InputStream is = s.getInputStream();
			InputStreamReader isr = new InputStreamReader(is);
			BufferedReader br = new BufferedReader(isr);
			
			String str = br.readLine();
			System.out.println("Message received : "+ str);
			
			// 클라이언트가 서버에게 문자 보내기
			OutputStream os = s.getOutputStream();
			OutputStreamWriter osw = new OutputStreamWriter(os);
			PrintWriter pw = new PrintWriter(osw);
			
			pw.println("client--> server : client sent a message to server");
			pw.flush();
			
			
			
		}catch(Exception e) {
			e.printStackTrace();
		}
		System.out.println("Client ended");

	}
	

	public static void main(String[] args) {
		new SocketTest();

	}

}
```

**서버**

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.InetAddress;
import java.net.ServerSocket;
import java.net.Socket;

public class ServerSocketTest {
	ServerSocket ss;
	public ServerSocketTest() {
		try {
			// 접속을 대기할 수 있는 ServerSocket은 port번호를 지정하여 객체를 생성한다. 
			ss = new ServerSocket(10000);
			
			System.out.println("Server start... waiting for connection");
			Socket s = ss.accept();
			
			InetAddress ia = s.getInetAddress();
			System.out.println(ia.getHostAddress()+"->Client is waiting");
			
			// 서버에서 클라이언트에게 문자 보내기
			OutputStream os = s.getOutputStream(); // 1byte
			OutputStreamWriter osw = new OutputStreamWriter(os); // 1byte 문자
			PrintWriter pw = new PrintWriter(osw);
			
			pw.println("Server->Client->Connected to server");
			pw.flush();
			
			// 클라이언트가 보낸 문자 받기
			InputStream is = s.getInputStream();
			InputStreamReader isr = new InputStreamReader(is);
			BufferedReader br = new BufferedReader(isr);
			
			String txt = br.readLine();
			System.out.println("Message server received ==> "+txt);
			
		}catch(IOException ie) {
			ie.printStackTrace();
		}
		System.out.println("Server ended");
	}
	

	public static void main(String[] args) {
		new ServerSocketTest();

	}

}

```



### DatagramSocket - UDP 방식

> UDP 방식의 정보를 보낼 경우 DatagramPacket을 생성하여 전송합니다.

```java
import java.net.DatagramPacket;
import java.net.DatagramSocket;

public class UnicastReceive {
	DatagramSocket ds;
	DatagramPacket dp;
	
	public UnicastReceive() {
		try {
			// 정보 받는 곳
			ds = new DatagramSocket(420);
			// 한번에 보내는 권장 크기 512byte
			// byte 배열 선언
			byte data[] = new byte[512];
			dp = new DatagramPacket(data, data.length);
			System.out.println("Waiting for message...");
			ds.receive(dp);
			
			// 전송 받은 데이터 출력하기
			byte[] receiveData = dp.getData();            // 전송받은 바이트수
			System.out.println(new String(receiveData, 0, dp.getLength()));
		}catch(Exception e) {
			e.printStackTrace();
		}
		
	}

	public static void main(String[] args) {
		new UnicastReceive();

	}

}

```



```java
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

public class UnicastSend {
	DatagramSocket ds;
	DatagramPacket dp;
	InetAddress ia;
	
	public UnicastSend() {
		String str = "I love MJ";
		try {
			// 정보 보내는 곳
			ds = new DatagramSocket();
			
			// udp 방식의 정보를 보낼 경우 DatagramPacket을 생성하여 전송합니다.
			byte[] data = str.getBytes(); // 보낼 데이터를 바이트형식으로 변환
			ia = InetAddress.getByName("myIpAddress");
			//					   보낼데이터,				 받는컴, 포트
			dp = new DatagramPacket(data, 0, data.length, ia, 420);
			// 전송하기
			ds.send(dp);
			
			System.out.println("Message sent!");
			
		}catch(Exception e) {
			e.printStackTrace();
		}
		
	}

	public static void main(String[] args) {
		new UnicastSend();

	}

}

```



### FileUnicast - 이미지 보내기

**서버**

```java
import java.io.File;
import java.io.FileOutputStream;
import java.net.DatagramPacket;
import java.net.DatagramSocket;

public class FileUnicastReceive {
	DatagramSocket ds;
	DatagramPacket dp;
	FileOutputStream fos;
	final int PORT = 4200;


	public FileUnicastReceive() {
		
	}
	public void receiveStart() {
		try {
			ds = new DatagramSocket(PORT);
			byte[] receiveData = new byte[512];
			dp = new DatagramPacket(receiveData, receiveData.length);
			
			
			// 전송이 완료될때까지 반복실행
			while(true) {
				// 전송받기 대기
				System.out.println("Waiting for message...");
				ds.receive(dp); // 전송받기
				
				byte[] receive = dp.getData();
				int byteCount = dp.getLength(); // 전송받은 byte수
				
				String receiveStr = new String(receive, 0, byteCount);
				if(byteCount>=10 && receiveStr.substring(0, 10).equals("[*$@File&]")) { // 파일이 전송되었다. 
					fos = new FileOutputStream(new File("/Users/myname/testfolder", receiveStr.substring(10)));
					System.out.println("Created a file --->"+ receiveStr);
				}else if(byteCount>=10 && receiveStr.equals("[*%&$end4]")) {
					fos.close();
					ds.close();
					System.out.println("File saved...");
					break;
				}else { // 파일내용
					fos.write(receive, 0, byteCount);
				}
			}
		}catch(Exception e) {
			e.printStackTrace();
		}
		
	}

	public static void main(String[] args) {
		new FileUnicastReceive().receiveStart();
	}

}

```

**Client**

```java
import java.io.File;
import java.io.FileInputStream;
import java.net.DatagramPacket;
import java.net.DatagramSocket;
import java.net.InetAddress;

public class FileUnicastSend {
	DatagramSocket ds;
	DatagramPacket dp;
	InetAddress ia;
	final int PORT = 4200;
	
	public FileUnicastSend() {
		
	}
	public void sendStart() {
		try {
			ds = new DatagramSocket();
			ia = InetAddress.getByName("172.30.1.41");
			
			// 파일의 내용을 byte 배열로 읽어와 보내기 위해 InputStream 객체를 생성한다. 
			File f = new File("/Users/myname/img/01.jpeg");
			FileInputStream fis = new FileInputStream(f);
			
			// 파일명을 전송
			String sendFileName = "[*$@File&]" + f.getName(); // "[*$@File&]02/jfif"
			dp = new DatagramPacket(sendFileName.getBytes(), 0, sendFileName.getBytes().length, ia, PORT);
			ds.send(dp);
			
			// 파일내용읽어 전송
			int cnt=0;
			while(true) {
				byte[] b = new byte[512];
				int byteCount = fis.read(b, 0, b.length);
				System.out.println(++cnt+", byte=" + byteCount);
				if(byteCount<=0) break;
				dp = new DatagramPacket(b, 0, byteCount, ia, PORT);
				ds.send(dp);
			}
			
			
			// 전송을 완료...
			String endMessage = "[*%&$end4]";
			dp = new DatagramPacket(endMessage.getBytes(), 0, endMessage.getBytes().length, ia, PORT);
			ds.send(dp);
			
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	public static void main(String[] args) {
		new FileUnicastSend().sendStart();

	}

}
```



### MultiSocket

**Client**

```java
// 보내는쪽
import java.net.DatagramPacket;
import java.net.InetAddress;
import java.net.MulticastSocket;

public class MulticastSend {
	// 사용가능 공용 IP 주소 : 224.0.0.0 ~ 239.255.255.255
	// 사용할 공용 IP 주소 : 224.42.42.42
	
	// 변수 생성
	MulticastSocket ms;
	DatagramPacket dp;
	InetAddress ia;
	final int PORT = 420;
	
	public MulticastSend() {
		// 보낼 내용
		String str = "Practicing network via Multicast";
		try {
			ms = new MulticastSocket();
			ia = InetAddress.getByName("224.42.42.42");
			dp = new DatagramPacket(str.getBytes(), 0, str.getBytes().length, ia, PORT);
			
			ms.send(dp); // 공용아이피로 전송
			System.out.println("Message sent!");
			
		}catch(Exception e) {
			e.printStackTrace();
		}
		
	}

	public static void main(String[] args) {
		new MulticastSend();
		
	}

}

```



**Server**

```java
// 받는쪽
import java.net.DatagramPacket;
import java.net.InetAddress;
import java.net.InetSocketAddress;
import java.net.MulticastSocket;
import java.net.NetworkInterface;

public class MulticastReceive {
	// 변수 생성
	MulticastSocket ms;
	DatagramPacket dp;
	InetAddress ia;
	final int PORT = 420;

	public MulticastReceive() {
		try {
			ms = new MulticastSocket(PORT);
			ia = InetAddress.getByName("224.42.42.42");
			
			InetSocketAddress isa = new InetSocketAddress(ia, PORT);
			NetworkInterface ni = NetworkInterface.getByName("john");
			ms.joinGroup(isa, ni);
			
			byte data[] = new byte[512];
			dp = new DatagramPacket(data, data.length);
			ms.receive(dp); // 받기 대기중
			
			System.out.println(new String(dp.getData(), 0, dp.getLength()));
			
		}catch(Exception e) {
			e.printStackTrace();
		}
		
	}

	public static void main(String[] args) {
		new MulticastReceive();

	}

}

```

