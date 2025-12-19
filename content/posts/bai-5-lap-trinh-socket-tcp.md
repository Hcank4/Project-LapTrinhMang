---
title: "Bài 5: Lập trình Socket TCP với Java"
date: 2025-12-19T12:00:00+07:00
draft: false
summary: "Hướng dẫn xây dựng mô hình Client-Server sử dụng TCP Socket."
tags: ["Java", "TCP", "Socket"]
---

TCP Socket đảm bảo dữ liệu được truyền đi một cách tin cậy.

### Mã nguồn phía Server:
```java
ServerSocket server = new ServerSocket(5000);
System.out.println("Server đang chờ kết nối...");
Socket socket = server.accept(); // Chấp nhận kết nối từ Client

### Mã nguồn phía Client:
Socket socket = new Socket("localhost", 5000);
System.out.println("Đã kết nối tới Server!");