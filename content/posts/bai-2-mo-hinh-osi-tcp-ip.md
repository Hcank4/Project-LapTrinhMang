---
title: "Bài 2: Mô hình OSI và TCP/IP"
date: 2025-12-19T09:00:00+07:00
weight: 2
draft: false
summary: "Phân tích 7 tầng của mô hình OSI và cách internet vận hành dựa trên bộ giao thức TCP/IP."
tags: ["Networking", "OSI", "TCP/IP"]
showToc: true
---

## 1. Mô hình OSI (7 tầng)
Mô hình OSI chia quá trình truyền tin thành 7 lớp:
1. **Physical:** Truyền tải dòng bit vật lý.
2. **Data Link:** Quản lý lỗi vật lý và địa chỉ MAC.
3. **Network:** Định tuyến (IP).
4. **Transport:** Truyền tải dữ liệu giữa các tiến trình (TCP/UDP).
5. **Session:** Quản lý phiên kết nối.
6. **Presentation:** Mã hóa và định dạng dữ liệu.
7. **Application:** Giao diện người dùng (HTTP, FTP, SMTP).

## 2. Mô hình TCP/IP
Thực tế, Internet sử dụng mô hình TCP/IP rút gọn gồm 4 tầng:
* **Tầng ứng dụng (Application):** Tương ứng tầng 5, 6, 7 của OSI.
* **Tầng giao vận (Transport):** Đảm bảo truyền dữ liệu.
* **Tầng mạng (Internet):** Định vị mục tiêu qua IP.
* **Tầng truy cập mạng (Network Access):** Kết nối vật lý.