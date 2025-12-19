---
title: "Bài 8: Giao thức HTTP và Web Server"
date: 2025-12-19T07:00:00+07:00
weight: 8
draft: false
summary: "Tìm hiểu cách trình duyệt gửi request GET/POST và cách Server phản hồi."
tags: ["HTTP", "Web", "Server"]
cover:
    image: "https://images.unsplash.com/photo-1629654297299-c8506221ca97?q=80&w=1974&auto=format&fit=crop" # Link ảnh mạng (ví dụ)
    alt: "Mô hình kết nối mạng" # Chú thích ảnh khi không load được
    caption: "Lập trình mạng là nền tảng của Internet" # Chú thích nhỏ dưới ảnh
    relative: false # Để false vì đang dùng link ngoài
---

Mọi trang web bạn xem hàng ngày đều hoạt động dựa trên giao thức HTTP.
* **Request:** Trình duyệt gửi yêu cầu lấy dữ liệu.
* **Response:** Server gửi mã trạng thái (200 OK, 404 Not Found) và nội dung HTML.