---
title: "Bài 1: Tổng quan về Lập trình mạng"
date: 2025-12-19T08:00:00+07:00
weight: 1
draft: false
summary: "Tìm hiểu những khái niệm cơ bản nhất về lập trình mạng và mô hình Client-Server."
tags: ["Networking", "Basics", "Java"]
showToc: true
cover:
    image: "https://images.unsplash.com/photo-1629654297299-c8506221ca97?q=80&w=1974&auto=format&fit=crop" # Link ảnh mạng (ví dụ)
    alt: "Mô hình kết nối mạng" # Chú thích ảnh khi không load được
    caption: "Lập trình mạng là nền tảng của Internet" # Chú thích nhỏ dưới ảnh
    relative: false # Để false vì đang dùng link ngoài
---

## 1. Lập trình mạng là gì?
Lập trình mạng là việc viết các chương trình máy tính cho phép các thiết bị (máy tính, điện thoại, server) giao tiếp và trao đổi dữ liệu với nhau thông qua mạng internet hoặc mạng nội bộ.

## 2. Mô hình Client - Server
Đây là mô hình phổ biến nhất trong lập trình mạng:
* **Client (Máy khách):** Là bên gửi yêu cầu (request). Ví dụ: Trình duyệt Chrome, ứng dụng Mobile.
* **Server (Máy chủ):** Là bên nhận yêu cầu, xử lý và gửi phản hồi (response). Server thường chạy 24/7 để chờ đợi kết nối.

## 3. Các thành phần chính
Để hai máy tính nói chuyện được với nhau, chúng ta cần:
1. **Địa chỉ IP:** Để biết máy tính đó ở đâu.
2. **Cổng (Port):** Để biết dữ liệu sẽ đi vào ứng dụng nào trên máy tính đó.
3. **Giao thức (Protocol):** Quy tắc để hai bên hiểu nhau (như ngôn ngữ chung).