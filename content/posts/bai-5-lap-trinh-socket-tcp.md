---
title: "Bài 5: Lập trình Socket TCP với Java"
date: 2025-12-19T07:00:00+07:00
draft: false
summary: "Hướng dẫn xây dựng mô hình Client-Server sử dụng TCP Socket để truyền dữ liệu tin cậy."
tags: ["Java", "TCP", "Socket"]
weight: 5
showToc: true
cover:
    image: "https://images.unsplash.com/photo-1629654297299-c8506221ca97?q=80&w=1974&auto=format&fit=crop" # Link ảnh mạng (ví dụ)
    alt: "Mô hình kết nối mạng" # Chú thích ảnh khi không load được
    caption: "Lập trình mạng là nền tảng của Internet" # Chú thích nhỏ dưới ảnh
    relative: false # Để false vì đang dùng link ngoài
---

TCP (Transmission Control Protocol) là giao thức hướng kết nối, đảm bảo dữ liệu được truyền đi một cách chính xác và đúng thứ tự. Trong bài học này, chúng ta sẽ cùng xây dựng một ứng dụng giao tiếp đơn giản gồm hai phần: Server và Client.



## 1. Code mẫu
Server có nhiệm vụ mở một cổng (Port) và chờ đợi kết nối từ Client. Khi có kết nối, Server sẽ đọc tin nhắn nhận được và in ra màn hình.

```java
// Code Server :
import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) {
        // Mở ServerSocket tại cổng 5000
        try (ServerSocket serverSocket = new ServerSocket(5000)) {
            System.out.println("Server đang chờ kết nối ở cổng 5000...");
            
            // Chấp nhận kết nối từ Client
            Socket socket = serverSocket.accept();
            System.out.println("Client đã kết nối thành công!");

            // Luồng đọc dữ liệu từ Client gửi tới
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            String message = reader.readLine();
            System.out.println("Tin nhắn từ Client: " + message);

            // Đóng socket sau khi xử lý xong
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
//Code Client: 
import java.io.*;
import java.net.*;

public class TCPClient {
    public static void main(String[] args) {
        // Kết nối tới Server tại localhost, cổng 5000
        try (Socket socket = new Socket("localhost", 5000)) {
            System.out.println("Đã kết nối tới Server thành công!");

            // Luồng gửi dữ liệu tới Server
            PrintWriter writer = new PrintWriter(socket.getOutputStream(), true);
            writer.println("Chào Server! Em là Hồng Cần, đây là tin nhắn từ Client.");

            System.out.println("Đã gửi tin nhắn tới Server.");
        } catch (IOException e) {
            System.err.println("Lỗi: " + e.getMessage());
        }
    }
}
