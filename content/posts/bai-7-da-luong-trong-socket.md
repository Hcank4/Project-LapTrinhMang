---
title: "Bài 7: Đa luồng (Multi-threading) trong Socket"
date: 2025-12-19T09:00:00+07:00
draft: false
summary: "Kỹ thuật giúp Server xử lý nhiều kết nối Client cùng một lúc bằng Thread."
tags: ["Java", "Multi-threading", "Socket"]
weight: 7
showToc: true
cover:
    image: "https://images.unsplash.com/photo-1629654297299-c8506221ca97?q=80&w=1974&auto=format&fit=crop" # Link ảnh mạng (ví dụ)
    alt: "Mô hình kết nối mạng" # Chú thích ảnh khi không load được
    caption: "Lập trình mạng là nền tảng của Internet" # Chú thích nhỏ dưới ảnh
    relative: false # Để false vì đang dùng link ngoài
---

Để Server không bị chặn khi có nhiều Client kết nối, chúng ta cần sử dụng Đa luồng (Multi-threading).



## 1. Code mẫu
Server sẽ tạo một luồng riêng cho mỗi Client kết nối vào.

```java
// Code Multi-threaded Server:
import java.io.*;
import java.net.*;

public class MultiThreadServer {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(5000)) {
            System.out.println("Server đa luồng đang chạy ở cổng 5000...");
            while (true) {
                Socket socket = serverSocket.accept();
                System.out.println("Có Client mới kết nối!");
                // Tạo một luồng mới để xử lý Client này
                new ClientHandler(socket).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// Class xử lý riêng cho từng Client:
class ClientHandler extends Thread {
    private Socket socket;
    public ClientHandler(Socket socket) { this.socket = socket; }

    @Override
    public void run() {
        try {
            BufferedReader reader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            System.out.println("Nhận dữ liệu: " + reader.readLine());
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}