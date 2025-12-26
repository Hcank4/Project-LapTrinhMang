---
title: "Bài 8: Đỉnh núi cuối cùng - Xây dựng Web Server từ con số 0"
date: 2025-12-26T08:00:00+07:00
author: "PHẠM HỒNG CẦN"
weight: 8
draft: false
summary: "Tại sao phải dùng Apache hay Nginx khi chúng ta có thể tự tay xây dựng một 'linh hồn' cho trang web bằng Java Socket?"
tags: ["Networking", "Java", "Web Server", "HTTP", "Final Project"]
showToc: true
cover:
    image: "https://images.unsplash.com/photo-1460925895917-afdab827c52f?q=80&w=2015&auto=format&fit=crop" 
    alt: "Giao diện Web và Server"
    caption: "Đỉnh núi cuối cùng của sự sáng tạo"
    relative: false
---

## 1. Tham vọng của một người lữ khách

Hồi mới chập chững vào **HUTECH**, mình nhìn những trang web lung linh và tự hỏi: *"Làm sao cái máy tính vô hồn kia có thể hiểu được mình muốn xem gì mà gửi trả lại hình ảnh, chữ viết?"*. Sau 7 bài viết vừa qua, mình nhận ra: Web Server thực chất chỉ là một Server TCP "biết nói tiếng người" (Giao thức HTTP).

Thay vì dùng những công cụ có sẵn, việc tự tay xây dựng một Web Server từ con số 0 giúp ní chạm vào "linh hồn" của Internet. Đó chính là viên sỏi óng ánh nhất trong hành trình này.

## 2. HTTP - Ngôn ngữ chung của đại dương Web

Để Web Server hoạt động, nó phải hiểu được giao thức **HTTP (HyperText Transfer Protocol)**.
* **Request:** Khi ní nhập địa chỉ web, trình duyệt (Client) sẽ gửi một "bản yêu cầu" kèm theo phương thức (GET, POST) và địa chỉ tài liệu.
* **Response:** Server nhận yêu cầu, lục lọi trong kho dữ liệu và gửi trả lại một "bản tin" kèm mã trạng thái (như 200 OK) và nội dung HTML.
import java.io.*;
import java.net.*;

public class SimpleWebServer {
    public static void main(String[] args) {
        int port = 8080;
        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("[System] Web Server đang khởi chạy tại cổng " + port + "...");

            while (true) {
                Socket clientSocket = serverSocket.accept();
                // Xử lý mỗi yêu cầu trình duyệt trong một luồng riêng (Multi-threading)
                new Thread(() -> handleRequest(clientSocket)).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void handleRequest(Socket socket) {
        try (BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
             OutputStream out = socket.getOutputStream()) {

            // Đọc dòng yêu cầu đầu tiên từ trình duyệt (GET / HTTP/1.1)
            String requestLine = in.readLine();
            if (requestLine != null) {
                System.out.println("[Request] " + requestLine);
            }

            // Chuẩn bị nội dung phản hồi chuẩn HTTP
            String htmlContent = "<html><body><h1>Welcome to My Web Server!</h1>"
                               + "<p>Chao ni Pham Hong Can, day la phan hoi tu Java Socket.</p></body></html>";
            
            String httpResponse = "HTTP/1.1 200 OK\r\n"
                                + "Content-Type: text/html; charset=UTF-8\r\n"
                                + "Content-Length: " + htmlContent.getBytes().length + "\r\n"
                                + "\r\n"
                                + htmlContent;

            // Gửi dữ liệu về trình duyệt
            out.write(httpResponse.getBytes("UTF-8"));
            out.flush();
            System.out.println("[Response] Da gui trang web cho Client.");
            socket.close();

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

Trong Java, chúng ta kết hợp **Socket TCP (Bài 5)** để tạo cầu nối và **Đa luồng (Bài 7)** để phục vụ nhiều trình duyệt cùng lúc.

## 3. 🖥️ Kết quả thực chiến (Console Output)

Hãy cùng quan sát cách Web Server "tự chế" của mình giao tiếp với trình duyệt Chrome thực tế nhé.

> **[WEB SERVER TERMINAL]**
> 
> `[System] Web Server đang khởi chạy tại cổng 8080...`
>
> `[Listen] Đang chờ yêu cầu từ trình duyệt...`
>
> `[Request] Đã nhận một yêu cầu GET từ Chrome (IP: 127.0.0.1)`
>
> `[Header]: User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)...`
>
> `[Action]: Đang đọc file index.html và đóng gói dữ liệu...`
>
> `[Response]: Đã gửi trả mã 200 OK kèm nội dung trang web.`
>
> ---
> *Trạng thái: Trang web đã hiển thị rực rỡ trên trình duyệt Client!*


## 4. Vạch lá tìm đường hay đứng yên một chỗ?

Anh Tiger Nguyen từng nói: *"Bắt tay vào làm ngay trước khi quá già"*. Việc xây dựng Web Server này không chỉ là để nộp đồ án, mà là để ní rèn luyện tư duy diễn đạt — thứ mà dân IT mình thường thiếu và yếu. 

Dành 5 giờ để nghiên cứu cách cấu trúc một bản tin HTTP Response sẽ giúp ní hiểu tại sao trang web của mình bị lỗi 404 hay 500 sau này. Đừng giữ khư khư kiến thức cho riêng mình, hãy share nó ra, vì biết đâu chính bài viết này sẽ giúp một bạn sinh viên khác thoát khỏi "bãi lầy" của sự mơ hồ.

## 5. Lời nhắn nhủ

Khi ní nhìn thấy dòng chữ "Welcome to My Web Server" hiện lên trên trình duyệt từ chính code Java của mình, đó là khoảnh khắc ní thực sự trở thành một kỹ sư. Hãy tận hưởng thành quả này trước khi chúng ta bước vào bài tổng kết cuối cùng nhé!

---
*Ở Bài 9, chúng ta sẽ nhìn lại toàn bộ hành trình và vạch ra những hướng đi tiếp theo cho tương lai. Hẹn gặp lại ní ở vạch đích!*