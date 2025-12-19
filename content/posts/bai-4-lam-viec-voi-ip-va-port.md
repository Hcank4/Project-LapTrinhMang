---
title: "Bài 4: Làm việc với IP và Port trong Java"
date: 2025-12-19T11:00:00+07:00
weight: 4
draft: false
summary: "Sử dụng lớp InetAddress trong Java để quản lý địa chỉ IP và kiểm tra kết nối."
tags: ["Java", "Networking", "IP"]
cover:
    image: "https://images.unsplash.com/photo-1629654297299-c8506221ca97?q=80&w=1974&auto=format&fit=crop" # Link ảnh mạng (ví dụ)
    alt: "Mô hình kết nối mạng" # Chú thích ảnh khi không load được
    caption: "Lập trình mạng là nền tảng của Internet" # Chú thích nhỏ dưới ảnh
    relative: false # Để false vì đang dùng link ngoài
---

Trong lập trình mạng Java, lớp `InetAddress` là công cụ chính để làm việc với địa chỉ IP.

### Ví dụ kiểm tra IP của một trang web:
```java
import java.net.InetAddress;

public class GetIP {
    public static void main(String[] args) {
        try {
            InetAddress address = InetAddress.getByName("[www.google.com](https://www.google.com)");
            System.out.println("Địa chỉ IP: " + address.getHostAddress());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}