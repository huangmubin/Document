# 简易 Socket TCP 通讯

Server 端创建之后自动 bind 以及 listen(或者没有？)
Client 端创建之后自动 connect.
发送消息的时候，必须使用 println，否则消息发送不成功。

## Server 端

```
// Server.java
import java.io.*;
import java.net.*;

public class Server {

	static ServerSocket server;
	static Socket client;
	
	static void close() {
		try {
			if (server != null) {
				server.close();
			}
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		try {
			if (client != null) {
				client.close();				
			}
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		System.exit(1);;
	}
	
	public static void
			main(String[] args) {

		try {
			socket();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			close();
		}

		System.out.println("The server socket is end!");
	}
	
	static void socket() throws IOException {
		BufferedReader sysIn = new BufferedReader(
				new InputStreamReader(System.in));
		System.out.println("Please input the port: ");
		
		String ports = sysIn.readLine();
		int port = Integer.parseInt(ports);
		server = new ServerSocket(port);
		
		System.out.println("Address: " + InetAddress.getLocalHost().getHostAddress());
		System.out.println("Start accepting the client.");
		client = server.accept();
		BufferedReader in = new BufferedReader(
				new InputStreamReader(client.getInputStream()));
		PrintWriter out = new PrintWriter(client.getOutputStream());
		
		System.out.println("TCP is connect: " + 
				client.getInetAddress().getHostAddress() + ":" + 
				client.getPort());
		System.out.println("...");
		System.out.println("Client: " + in.readLine());
		
		String line = "hello!";
		System.out.print("Server: ");
		line = sysIn.readLine();
		while (!line.equals("bye!")) {
			// 必须使用 println, 否则检测不到 \n 系统并不会发送消息。
			out.println(line);
			out.flush();
			System.out.println("...");
			System.out.println("Client: " + in.readLine());
			System.out.print("Server: ");
			line = sysIn.readLine();
		}
		out.println(line);
		out.flush();
		
		server.close();
		client.close();
	}

}
```

## Client 端

```
// Client.java
import java.io.*;
import java.net.*;

public class Client {

	static Socket client;
	
	public static void
			main(String[] args) {
		// TODO Auto-generated method stub
		try {
			socket();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			
			if (client != null) {
				try {
					client.close();
				} catch (IOException e1) {
					// TODO Auto-generated catch block
					e1.printStackTrace();
				}
			}
		}
		
		System.out.println("The client socket is end!");
	}

	static void socket() throws IOException {
		BufferedReader sysIn = new BufferedReader(new InputStreamReader(System.in));
		
		System.out.print("Please input the address: ");
		String address = sysIn.readLine();
		System.out.print("Please input the port: ");
		String ports = sysIn.readLine();
		int port = Integer.parseInt(ports);
		
		client = new Socket(address, port);
		
		BufferedReader in = new BufferedReader(new InputStreamReader(client.getInputStream()));
		PrintWriter out = new PrintWriter(client.getOutputStream());
		
		String line = "";
		System.out.print("Client: ");
		line = sysIn.readLine();
		while (!line.equals("bye!")) {
			out.println(line);
			out.flush();
			System.out.println("...");
			System.out.println("Server: " + in.readLine());

			System.out.print("Client: ");
			line = sysIn.readLine();
		}
		out.println(line);
		out.flush();
		
		client.close();
	}
}
```

# Socket 超时设置

```
// 设置 3 秒连接超时，3秒读取超时
client.connect(new InetSocketAddress(address, port), 3000);
client.setSoTimeout(3000);
```

## Server 端

```
import java.io.*;
import java.net.*;

public class Server_Timeout {

	static ServerSocket server;
	static Socket client;
	static BufferedReader sysIn;
	static BufferedReader in;
	static PrintWriter out;
	
	static void close() {
		try {
			if (server != null) {
				server.close();
			}
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		try {
			if (client != null) {
				client.close();				
			}
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}

		System.out.println("The server socket is end!");
		System.exit(0);
	}
	
	public static void
			main(String[] args) {
		sysIn = new BufferedReader(new InputStreamReader(System.in));
		
		createServer();
		acceptClient();
		takeStream();
		read() ;
		write();
		
	}
	
	static void createServer() {
		try {
			System.out.println("Into Create Server;");
			System.out.print("Please input the port: ");
			String ports = sysIn.readLine();
			int port = Integer.parseInt(ports);
			server = new ServerSocket(port);
			System.out.println("Address: " + InetAddress.getLocalHost().getHostAddress() + ":" + ports);
		} catch (IOException e) {
			e.printStackTrace();
			createServer();
		}
	}
	
	static void acceptClient() {
		try {
			System.out.println("Start accepting the client.");
			client = server.accept();
			/// 设置 3 秒超时
			client.setSoTimeout(3000);
			System.out.println("Accep the: " 
					+ client.getInetAddress().getHostAddress() + ":"
					+ client.getPort()
			);
		} catch (IOException e) {
			e.printStackTrace();
			acceptClient();
		}
	}
	
	static void takeStream() {
		try {
			System.out.println("Start take the stream.");
			in = new BufferedReader(
					new InputStreamReader(client.getInputStream()));
			out = new PrintWriter(client.getOutputStream());
			System.out.println("OK take the stream.");
		} catch (IOException e) {
			e.printStackTrace();
			takeStream();
		}
	}
	
	static void read() {
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					Thread.sleep(1000);
					String re = in.readLine();
					if (re != null) {
						System.out.println("Client: " + re);
					}
				} catch (Exception e) {
//					e.printStackTrace();
				}
				read();
			}
		}).start();
	}
	
	static void write() {
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					Thread.sleep(1000);
					
					String line = sysIn.readLine();
					if (line.equals("bye!")) {
						out.println(line);
						out.flush();
						
						close();
					}
					else {
						out.println(line);
						out.flush();
					}
				} catch (IOException e) {
					e.printStackTrace();
				} catch (Exception e) {
					e.printStackTrace();
				}
				write();
			}
		}).start();
	}

}
```

## Client 端

```
import java.io.*;
import java.net.*;

public class Client_Timeout {

	static Socket client;
	static BufferedReader sysIn;
	static BufferedReader in;
	static PrintWriter out;
	
	public static void main(String[] args) {
		sysIn = new BufferedReader(new InputStreamReader(System.in));
		
		connectSocket();
		takeStream();
		read();
		write();
	}
	
	static void connectSocket() {
		try {
			System.out.println("Start connect Socket");
			System.out.print("Please input the address: ");
			String address = sysIn.readLine();
			System.out.print("Please input the port: ");
			String ports = sysIn.readLine();
			int port = Integer.parseInt(ports);
			
			client = new Socket();
			// 设置 3 秒连接超时，3秒读取超时
			client.connect(new InetSocketAddress(address, port), 3000);
			client.setSoTimeout(3000);
			System.out.println("End connect Socket");
		} catch (Exception e) {
			e.printStackTrace();
			connectSocket();
		}
	}

	static void takeStream() {
		try {
			System.out.println("Start take the stream.");
			in = new BufferedReader(
					new InputStreamReader(client.getInputStream()));
			out = new PrintWriter(client.getOutputStream());
			System.out.println("OK take the stream.");
		} catch (IOException e) {
			e.printStackTrace();
			takeStream();
		}
	}
	
	static void read() {
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					Thread.sleep(1000);
					String re = in.readLine();
					if (re != null) {
						System.out.println("Client: " + re);
					}
				} catch (Exception e) {
//					e.printStackTrace();
				}
				read();
			}
		}).start();
	}
	
	static void write() {
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					Thread.sleep(1000);
					
					String line = sysIn.readLine();
					if (line.equals("bye!")) {
						out.println(line);
						out.flush();
						
						client.close();
						System.out.print("End!!!");
						System.exit(0);
					}
					else {
						out.println(line);
						out.flush();
					}
				} catch (IOException e) {
					e.printStackTrace();
				} catch (Exception e) {
					e.printStackTrace();
				}
				write();
			}
		}).start();
	}
	
}
```

# UDP

```
DatagramSocket server = new DatagramSocket(1234);
byte[] recvBuffer = new byte[1024];
DatagramPacket recvPacket = new DatagramPacket(recvBuffer, recvBuffer.length);
server.receive(recvPacket);
DatagramPacket sendPacket = new DatagramPacket(sendBuf , sendBuf.length , addr , port );
server.send(sendPacket);
```

## Server 端

```
import java.io.*;
import java.net.*;

public class Server_udp {

	static BufferedReader sysIn;
	static DatagramSocket  server;
	static byte[] recvBuffer = new byte[1024];
	static DatagramPacket recvPacket = new DatagramPacket(recvBuffer, recvBuffer.length);
	
	public static void main(String[] args) {
		sysIn = new BufferedReader(new InputStreamReader(System.in));
		createServer();
		receive();
		send();
	}

	static void createServer() {
		try {
			System.out.println("Into Create Server;");
			System.out.print("Please input the port: ");
			String ports = sysIn.readLine();
			int port = Integer.parseInt(ports);
			server = new DatagramSocket(port);
			System.out.println("Address: " + InetAddress.getLocalHost().getHostAddress() + ":" + ports);
		} catch (IOException e) {
			e.printStackTrace();
			createServer();
		}
	}
	
	static void receive() {
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					Thread.sleep(1000);
					server.receive(recvPacket);
					String line = new String(recvPacket.getData(), 0, recvPacket.getLength());
					if (line != null) {
						System.out.println("Address: "
								+ recvPacket.getAddress().getHostAddress() + ":"
								+ recvPacket.getPort() + "; \n"
								+ "Client: " + line);
					}
				} catch (Exception e) {
//					e.printStackTrace();
				}
				receive();
			}
		}).start();
	}
	
	static void send() {
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					Thread.sleep(1000);
				    String sendStr = sysIn.readLine();
				    byte[] sendBuf = sendStr.getBytes();
					
				    if (sendStr.equals("bye!")) {
			    			System.out.println("End!");
				    		server.close();
				    		System.exit(0);
				    }
				    
					int port = recvPacket.getPort();
					InetAddress addr = recvPacket.getAddress();
					
				    DatagramPacket sendPacket = new DatagramPacket(sendBuf , sendBuf.length , addr , port );
				    server.send(sendPacket);
				} catch (Exception e) {
					e.printStackTrace();
				}
				send();
			}
		}).start();
	}
	
	
}
```

## Client 端

```
import java.io.*;
import java.net.*;
/// 向 255.255.255.255 发送消息即为广播。发送的时候，自己也会收到
public class Client_udp {
	
	static BufferedReader sysIn;
	static DatagramSocket  client;
	static byte[] recvBuffer = new byte[1024];
	static DatagramPacket recvPacket = new DatagramPacket(recvBuffer, recvBuffer.length);
	
	public static void main(String[] args) {
		sysIn = new BufferedReader(new InputStreamReader(System.in));
		createServer();
		send();
		receive();
	}

	static void createServer() {
		try {
			System.out.println("Into Create Client;");
			client = new DatagramSocket();
			System.out.println("Address: " + InetAddress.getLocalHost().getHostAddress() + ";");
		} catch (IOException e) {
			e.printStackTrace();
			createServer();
		}
	}
	
	static void send() {
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					Thread.sleep(1000);
					System.out.print("Send to address: ");
				    String sendAddress = sysIn.readLine();
				    System.out.print("Send to port: ");
				    String ports = sysIn.readLine();
					int sendPort = Integer.parseInt(ports);
				    System.out.print("Send to Message:  ");
				    String sendStr = sysIn.readLine();
				    byte[] sendBuf = sendStr.getBytes();
					
				    if (sendStr.equals("bye!")) {
			    			System.out.println("End!");
				    		client.close();
				    		System.exit(0);
				    }
				    
				    DatagramPacket sendPacket = new DatagramPacket(
				    		sendBuf , 
				    		sendBuf.length ,
				    		InetAddress.getByName(sendAddress) , 
				    		sendPort
				    	);
				    
				    client.send(sendPacket);
				} catch (Exception e) {
					e.printStackTrace();
				}
				send();
			}
		}).start();
	}
	

	static void receive() {
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					Thread.sleep(1000);
					client.receive(recvPacket);
					String line = new String(recvPacket.getData(), 0, recvPacket.getLength());
					if (line != null) {
						System.out.println("Address: "
								+ recvPacket.getAddress().getHostAddress() + ":"
								+ recvPacket.getPort() + "; \n"
								+ "Client: " + line);
					}
				} catch (Exception e) {
//					e.printStackTrace();
				}
				receive();
			}
		}).start();
	}
	
}
```


