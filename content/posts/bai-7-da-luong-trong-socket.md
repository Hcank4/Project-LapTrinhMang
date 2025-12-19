---
title: "Bài 7: Đa luồng (Multi-threading) trong Socket"
date: 2025-12-19T07:00:00+07:00
draft: false
summary: "Cách xử lý nhiều Client kết nối cùng lúc vào một Server."
tags: ["Java", "Multi-threading", "Advanced"]
---

Để Server không bị "treo" khi có nhiều người cùng truy cập, mỗi kết nối Client cần được xử lý trong một luồng (Thread) riêng biệt.

```java
while (true) {
    Socket socket = serverSocket.accept();
    new Thread(new ClientHandler(socket)).start();
}