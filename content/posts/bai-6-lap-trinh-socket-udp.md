---
title: "Bài 6: Lập trình Socket UDP với Java"
date: 2025-12-19T08:00:00+07:00
weight: 6
draft: false
summary: "Tìm hiểu cách truyền nhận dữ liệu tốc độ cao qua giao thức UDP bằng DatagramSocket."
tags: ["Java", "UDP", "Datagram"]
weight: 6
showToc: true
---

Khác với TCP, UDP là giao thức không kết nối, tập trung vào tốc độ truyền tải nhanh.



## 1. Code mẫu
Dưới đây là cách triển khai Server nhận dữ liệu và Client gửi gói tin.

```java
// Code Server (Nhận dữ liệu):
import java.net.*;

public class UDPServer {
    public static void main(String[] args) {
        try (DatagramSocket socket = new DatagramSocket(6000)) {
            System.out.println("UDP Server đang chờ gói tin ở cổng 6000...");
            
            byte[] buffer = new byte[1024];
            DatagramPacket packet = new DatagramPacket(buffer, buffer.length);
            
            socket.receive(packet); // Chờ nhận dữ liệu
            
            String message = new String(packet.getData(), 0, packet.getLength());
            System.out.println("Tin nhắn từ Client: " + message);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

// Code Client (Gửi dữ liệu):
import java.net.*;

public class UDPClient {
    public static void main(String[] args) {
        try (DatagramSocket socket = new DatagramSocket()) {
            String message = "Chào Server! Đây là tin nhắn UDP từ Hồng Cần.";
            byte[] data = message.getBytes();
            
            InetAddress address = InetAddress.getByName("localhost");
            DatagramPacket packet = new DatagramPacket(data, data.length, address, 6000);
            
            socket.send(packet); // Gửi gói tin đi
            System.out.println("Đã gửi gói tin thành công!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}