---
title: "Bài 6: Lập trình Socket UDP với Java"
date: 2025-12-19T07:00:00+07:00
draft: false
summary: "Cách truyền dữ liệu nhanh chóng qua giao thức UDP bằng DatagramPacket."
tags: ["Java", "UDP", "Datagram"]
---

UDP không cần thiết lập kết nối nên tốc độ rất nhanh. Chúng ta sử dụng `DatagramSocket` và `DatagramPacket`.

```java
// Gửi dữ liệu UDP
DatagramSocket socket = new DatagramSocket();
byte[] buffer = "Hello UDP".getBytes();
InetAddress address = InetAddress.getByName("localhost");
DatagramPacket packet = new DatagramPacket(buffer, buffer.length, address, 5000);
socket.send(packet);