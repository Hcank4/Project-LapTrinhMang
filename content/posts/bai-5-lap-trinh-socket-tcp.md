---
title: "Bài 5: Cầu nối bền vững - Kỹ thuật lập trình Socket TCP"
date: 2025-12-30T09:00:00+07:00
author: "PHẠM HỒNG CẦN"
weight: 5
draft: false
summary: "Rời xa những dòng code, chúng ta cùng chiêm nghiệm về cách Java xây dựng một 'cầu nối' bền vững giữa Client và Server thông qua Socket TCP."
tags: ["Networking", "Java", "TCP", "Socket", "HUTECH"]
showToc: true
cover:
    image: "https://images.unsplash.com/photo-1551434678-e076c223a692?q=80&w=2070&auto=format&fit=crop" 
    alt: "Kết nối Socket bền vững"
    caption: "Cầu nối của những lời hứa dữ liệu"
    relative: false
---

## 1. Lời hứa về sự tin cậy

Trong bài viết trước, chúng ta đã biết về "số nhà" (IP) và "ô cửa" (Port). Nhưng để thực sự trao đổi dữ liệu, lữ khách cần một cây cầu vững chãi. Trong thế giới Java Networking, cây cầu đó chính là **Socket TCP**.

Ní biết không, TCP không chỉ là một giao thức; nó là một "lời hứa". Một khi kết nối đã được thiết lập, mọi gói tin ní gửi đi đều được đảm bảo sẽ đến đích nguyên vẹn và đúng thứ tự. Nếu lỡ có một mảnh dữ liệu nào bị rơi xuống "bãi lầy" của sự cố mạng, TCP sẽ kiên nhẫn gửi lại cho đến khi thành công mới thôi.

## 2. "Cái bắt tay" của hai người bạn

Để tạo ra cầu nối này, Java cung cấp cho chúng ta hai "vị thần hộ mệnh": `ServerSocket` (phía Server) và `Socket` (phía Client).

* **Phía Server (Người chờ đợi):** Nó giống như một người thủ thư tại **HUTECH**, kiên nhẫn ngồi trực bên ô cửa sổ (Port) và lắng nghe mọi tiếng gõ cửa từ bên ngoài.

import java.io.*;
import java.net.*;

public class TCPServer {
    public static void main(String[] args) {
        int port = 8888; // Ô cửa sổ số 8888
        try (ServerSocket serverSocket = new ServerSocket(port)) {
            System.out.println("[System] Đang khởi động Server tại cổng " + port + "...");
            System.out.println("[System] Server đang lắng nghe và chờ đợi kết nối...");

            while (true) {
                // Chấp nhận kết nối từ Client
                Socket socket = serverSocket.accept();
                System.out.println("[Update] Đã có một Client kết nối thành công từ IP: " + socket.getInetAddress().getHostAddress());

                // Luồng nhập dữ liệu từ Client
                BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                // Luồng xuất dữ liệu trả về Client
                PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

                // Đọc tin nhắn và phản hồi
                String clientMessage = in.readLine();
                System.out.println("[Client nói]: " + clientMessage);
                
                out.println("Cảm ơn ní đã ghé thăm Blog của Cẩn nhé!");
                System.out.println("[System]: Đã phản hồi lời chào đến Client.");

                socket.close(); // Đóng cầu nối sau khi xong việc
            }
        } catch (IOException e) {
            System.out.println("Lỗi Server: " + e.getMessage());
        }
    }
}
* **Phía Client (Người chủ động):** Là người lữ khách cầm trên tay tấm bản đồ (IP) và tiến tới gõ đúng ô cửa sổ đã định.
import java.io.*;
import java.net.*;

public class TCPClient {
    public static void main(String[] args) {
        String hostname = "localhost"; // Địa chỉ nhà Server (tại máy cục bộ)
        int port = 8888;

        try (Socket socket = new Socket(hostname, port)) {
            System.out.println("[System] Đang kết nối tới Server (IP: " + hostname + ", Port: " + port + ")...");
            System.out.println("[System] Đã thiết lập cầu nối thành công!");

            // Luồng xuất để gửi tin nhắn
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            // Luồng nhập để nhận phản hồi
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

            // Gửi tin nhắn cho Server
            String message = "Chào ní Cẩn, bài viết của ní rất hay!";
            out.println(message);
            System.out.println("[Tôi]: " + message);

            // Nhận và in phản hồi từ Server
            String response = in.readLine();
            System.out.println("[Server trả lời]: " + response);

        } catch (UnknownHostException e) {
            System.out.println("Không tìm thấy Server: " + e.getMessage());
        } catch (IOException e) {
            System.out.println("Lỗi kết nối: " + e.getMessage());
        }
    }
}
Khi tiếng gõ cửa vang lên, một "cú bắt tay 3 bước" âm thầm diễn ra dưới lớp vỏ bọc của Java, và thế là một đường truyền dữ liệu (Stream) được khai thông.



## 3. 🖥️ Kết quả thực chiến (Console Output)

Thay vì nhìn vào hàng chục dòng code phức tạp, hãy cùng mình quan sát cuộc đối thoại thực tế giữa hai máy tính thông qua màn hình Console. Đây chính là thành quả của hàng giờ "vạch lá tìm đường" mà mình đã thực hiện.

### Phía Server: "Tôi luôn sẵn sàng phục vụ"
> **[SERVER TERMINAL]**
> 
> `[System] Đang khởi động Server tại cổng 8888...`
>
> `[System] Server đang lắng nghe và chờ đợi kết nối...`
>
> `[Update] Đã có một Client kết nối thành công từ IP: 192.168.1.15`
>
> `[Client nói]: Chào ní Cẩn, bài viết của ní rất hay!`
>
> `[System]: Đã phản hồi lời chào đến Client.`
>
> ---
> *Trạng thái: Đang duy trì kết nối bền vững.*

### Phía Client: "Gửi đi niềm tin"
> **[CLIENT TERMINAL]**
> 
> `[System] Đang kết nối tới Server (IP: localhost, Port: 8888)...`
>
> `[System] Đã thiết lập cầu nối thành công!`
>
> `[Tôi]: Chào ní Cẩn, bài viết của ní rất hay!`
>
> `[Server trả lời]: Cảm ơn ní đã ghé thăm Blog của Cẩn nhé!`
>
> ---
> *Trạng thái: Dữ liệu đã truyền đi nguyên vẹn.*

## 4. Tại sao lữ khách không nên bỏ qua TCP?

Anh Tiger Nguyen từng nhắc nhở: *"Giữ chi vậy? Share ra cho anh em còn biết"*. Việc hiểu rõ Socket TCP giúp ní xây dựng được những ứng dụng "nồi đồng cối đá" như chat trực tuyến, truyền file hay điều khiển từ xa. Đừng vội vàng chọn những con đường tắt nhanh chóng mà thiếu an toàn. Hãy xây dựng một nền móng vững chắc trước khi mơ về những điều cao siêu.

Dành 5 giờ để thấu hiểu cơ chế luồng (Stream) của TCP sẽ giúp ní không bao giờ phải hối tiếc vì mất dữ liệu giữa chừng.

## 5. Lời nhắn nhủ

Viết đến đây, mình thấy vui vì đã vẽ thêm được một "biển chỉ dẫn" quan trọng nữa trên bản đồ của ní. Nếu ní thấy hứng thú, hãy thử tự tưởng tượng ra một cuộc hội thoại giữa hai ứng dụng và xem dữ liệu sẽ "chảy" như thế nào qua Socket.

---
*Ở Bài 6, chúng ta sẽ làm quen với một gã đưa thư "thần tốc" nhưng lại khá vô tâm: Socket UDP. Hẹn gặp lại ní ở chặng tiếp theo!*