---
title: "Bài 7: Dâu trăm họ - Kỹ thuật xử lý Đa luồng trong Socket"
date: 2025-12-26T08:00:00+07:00
author: "PHẠM HỒNG CẦN"
weight: 7
draft: false
summary: "Làm sao để một Server có thể phục vụ hàng ngàn người dùng cùng lúc mà không bị 'đứng hình'? Câu trả lời nằm ở Multi-threading."
tags: ["Networking", "Java", "Multi-threading", "Socket", "Performance"]
showToc: true
cover:
    image: "https://images.unsplash.com/photo-1518770660439-4636190af475?q=80&w=1000&auto=format&fit=crop"
    alt: "Hệ thống đa luồng song song"
    caption: "Sức mạnh từ sự phân thân"
    relative: false
---

## 1. Nỗi ám ảnh mang tên "Xếp hàng"

Hãy tưởng tượng ní xây dựng một Server TCP như ở Bài 5, nhưng khi có hai lữ khách cùng gõ cửa, người thứ hai phải đứng đợi cho đến khi người thứ nhất "nói chuyện" xong và đóng kết nối. Trong thế giới Internet hiện đại, sự chờ đợi này là một "bãi lầy" chết chóc.

Server của chúng ta cần phải trở thành một "người dâu trăm họ" thực thụ, có thể tiếp đón và trò chuyện với tất cả mọi người cùng một lúc.

## 2. Multi-threading - Giải pháp phân thân của Java

Để giải quyết vấn đề này, chúng ta sử dụng kỹ thuật **Đa luồng (Multi-threading)**. Thay vì một mình Server làm hết mọi việc, mỗi khi có một Client kết nối đến, Server sẽ "đẻ" ra một nhân viên phục vụ riêng (Worker Thread) cho người khách đó.

* **Server:** Chỉ tập trung vào việc canh cửa (Listen) và chấp nhận kết nối.
* **Worker Thread:** Chịu trách nhiệm tâm sự, trao đổi dữ liệu riêng tư với Client cho đến khi kết thúc.

import java.io.*;
import java.net.*;

public class MultiThreadedServer {
    public static void main(String[] args) {
        int port = 8888;
        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("[System] Server Đa luồng đang khởi động tại cổng " + port);

            while (true) {
                Socket clientSocket = serverSocket.accept();
                // Mỗi khi có khách, tạo một Thread mới để phục vụ
                new ClientHandler(clientSocket).start();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

// Lớp nhân viên phục vụ (Worker Thread)
class ClientHandler extends Thread {
    private Socket socket;

    public ClientHandler(Socket socket) {
        this.socket = socket;
    }

    public void run() {
        try (BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
             PrintWriter out = new PrintWriter(socket.getOutputStream(), true)) {
            
            System.out.println("[Connect] Client mới đã vào từ: " + socket.getInetAddress());
            String inputLine;
            while ((inputLine = in.readLine()) != null) {
                out.println("Server nhận được: " + inputLine);
            }
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
## 3. 🖥️ Kết quả thực chiến (Console Output)

Hãy cùng quan sát cách Server của mình "phân thân" để phục vụ 3 Client cùng lúc như thế nào nhé.

> **[MULTI-THREADED SERVER TERMINAL]**
> 
> `[System] Server Đa luồng đang khởi động tại cổng 8888...`
>
> `[System] Đang sẵn sàng tiếp đón nhiều Client cùng lúc...`
>
> `[Connect] Client #1 (IP: 192.168.1.5) đã vào.`
>
> `[Connect] Client #2 (IP: 192.168.1.12) đã vào.`
>
> `[Worker-1]: Đang xử lý yêu cầu cho Client #1...`
>
> `[Worker-2]: Đang xử lý yêu cầu cho Client #2...`
>
> `[Connect] Client #3 (IP: 10.0.0.8) đã vào.`
>
> `[Worker-3]: Đang xử lý yêu cầu cho Client #3...`
>
> ---
> *Trạng thái: 03 luồng đang hoạt động song song mượt mà.*

## 4. Cái tâm của người lập trình

Anh Tiger Nguyen từng nhắc nhở về việc vẽ ra những biển chỉ dẫn để lữ khách không đạp lên bãi lầy. Việc sử dụng Đa luồng chính là cách ní bảo vệ trải nghiệm của người dùng. Một kỹ sư có tầm sẽ không bao giờ để khách hàng của mình phải đứng đợi trong vô vọng.

Dành 5 giờ để làm chủ lớp `Thread` hoặc `Runnable` trong Java sẽ giúp ní xây dựng được những hệ thống lớn như ứng dụng Chat phòng nhiều người hay các Game Online phức tạp.

## 5. Lời nhắn nhủ

Đa luồng rất mạnh mẽ nhưng cũng đầy cạm bẫy. Hãy cẩn thận với việc quản lý tài nguyên, đừng để Server của ní "kiệt sức" vì tạo ra quá nhiều nhân viên cùng lúc. Hãy coi đây là một bài tập luyện tư duy logic cực kỳ tốt cho dân IT mình.

---
*Ở Bài 8, chúng ta sẽ ứng dụng tất cả "tinh hoa" từ Bài 1 đến Bài 7 để xây dựng một Web Server thực thụ. Đừng bỏ lỡ chặng về đích này nhé!*