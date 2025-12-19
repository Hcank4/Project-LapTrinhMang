---
title: "Bài 3: Phân biệt giao thức TCP và UDP"
date: 2025-12-19T10:00:00+07:00
weight: 3
draft: false
summary: "So sánh chi tiết ưu và nhược điểm của hai giao thức cốt lõi trong lập trình Socket."
tags: ["TCP", "UDP", "Protocol"]
showToc: true
---

## 1. Giao thức TCP (Transmission Control Protocol)
* **Đặc điểm:** Hướng kết nối (Connection-oriented). Phải "bắt tay" trước khi truyền dữ liệu.
* **Ưu điểm:** Đảm bảo dữ liệu đến đúng thứ tự và không bị mất mát.
* **Ứng dụng:** Web (HTTP), Email, Truyền file (FTP).

## 2. Giao thức UDP (User Datagram Protocol)
* **Đặc điểm:** Không kết nối (Connectionless). Cứ thế gửi dữ liệu đi mà không cần biết đối phương có nhận được không.
* **Ưu điểm:** Tốc độ cực nhanh, độ trễ thấp.
* **Ứng dụng:** Livestream, Chơi game online, Gọi video.

| Đặc điểm | TCP | UDP |
| :--- | :--- | :--- |
| Độ tin cậy | Cao | Thấp |
| Tốc độ | Chậm hơn | Rất nhanh |
| Bắt tay 3 bước | Có | Không |