# Socket Programming in Java

Socket programming is a way to enable communication between two computers using sockets. It involves two main components: the server and the client. Here’s a comprehensive guide on socket programming in Java.

## Table of Contents
1. [Introduction](#introduction)
2. [Understanding Sockets](#understanding-sockets)
3. [Creating a Socket Server](#creating-a-socket-server)
4. [Creating a Socket Client](#creating-a-socket-client)
5. [Data Transmission](#data-transmission)
6. [Handling Exceptions](#handling-exceptions)
7. [Conclusion](#conclusion)

## Introduction
Socket programming in Java allows developers to establish network communication between machines. It is widely used in various applications like web servers, email clients, and chat applications.

## Understanding Sockets
A socket is an endpoint for sending and receiving data across a network. In Java, the `java.net` package provides classes for implementing socket-based communication. The main classes are:
- **Socket**: Used by the client to connect to the server.
- **ServerSocket**: Used by the server to listen for client requests.

## Creating a Socket Server
To create a socket server, follow these steps:
1. Import necessary packages: `import java.io.*; import java.net.*;`
2. Create a `ServerSocket` instance, specify the port number.
3. Use `accept()` method to listen for incoming connections.
4. Handle requests using a loop or thread pooling.

### Example: Socket Server
```java
import java.io.*;
import java.net.*;

public class SocketServer {
    public static void main(String[] args) throws IOException {
        ServerSocket serverSocket = new ServerSocket(12345);
        System.out.println("Server started and waiting for connections...");
        while (true) {
            Socket clientSocket = serverSocket.accept();
            System.out.println("Client connected: " + clientSocket.getInetAddress());
            // Handle client in a separate thread...
        }
    }
}
```

## Creating a Socket Client
To create a socket client, follow these steps:
1. Import necessary packages: `import java.io.*; import java.net.*;`
2. Create a `Socket` instance and connect it to the server.
3. Use input/output streams to communicate.

### Example: Socket Client
```java
import java.io.*;
import java.net.*;

public class SocketClient {
    public static void main(String[] args) throws IOException {
        Socket socket = new Socket("localhost", 12345);
        System.out.println("Connected to server");
        // Communicate with server...
    }
}
```

## Data Transmission
Data can be sent and received using input and output streams. In the server and client, you can create `InputStream` and `OutputStream` objects to read and write data.

### Example:
```java
// On the server side:
OutputStream out = clientSocket.getOutputStream();
PrintWriter writer = new PrintWriter(out, true);
writer.println("Hello from server");

// On the client side:
InputStream in = socket.getInputStream();
BufferedReader reader = new BufferedReader(new InputStreamReader(in));
String response = reader.readLine();
System.out.println("Server response: " + response);
```

## Handling Exceptions
Always handle exceptions like `IOException` and `UnknownHostException` to ensure the robustness of socket programs. Enclose your socket communication code in try-catch blocks accordingly.

## Conclusion
Socket programming in Java provides a powerful way to create networked applications. Understanding the basics of sockets and implementation patterns allows for building efficient and scalable communication between clients and servers.