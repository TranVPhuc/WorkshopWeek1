---
title : "Cấu trúc Web Server"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2.</b> "
---

### Cấu trúc Web Server

![ws-structure](/images/2.2-ws-structure/00001.jpg?featherlight=false&width=60pc)
Cấu trúc của một web server có thể được phân thành các thành phần cơ bản sau:
1. Phần cứng máy chủ (Server Hardware):
> * **Máy chủ**: Một máy tính chạy liên tục để chạy các dịch vụ web.
> * **Kết nối mạng**: Để kết nối với internet hoặc mạng nội bộ.**
2. Phần mềm máy chủ (Server Software):
> * **Hệ điều hành**: Thường là các biến thể của Linux (như Ubuntu, CentOS) hoặc Windows Server.
> * **Web server software**: Phần mềm chạy trên máy chủ để xử lý các yêu cầu HTTP. Apache, Nginx, Microsoft IIS là các ví dụ phổ biến.
3. Ứng dụng và dữ liêu:
> * **Ứng dụng web**: Mã nguồn của trang web hoặc ứng dụng web, thường được viết bằng các ngôn ngữ như HTML, CSS, JavaScript, và back-end languages như PHP, Python, Ruby, hoặc Node.js.
> * **Dữ liệu**: Cơ sở dữ liệu thường được sử dụng để lưu trữ dữ liệu của ứng dụng web, như MySQL, PostgreSQL, MongoDB.
Cách hoạt động của 1 Web Server:
1. Tiếp nhận yêu cầu (Request Handling):
> * Web server lắng nghe trên một cổng nhất định (thường là cổng 80 cho HTTP hoặc 443 cho HTTPS).
> * Khi một yêu cầu HTTP được gửi đến, web server tiếp nhận yêu cầu này qua giao thức TCP/IP.
2. Xử lý yêu cầu (Request Processing):
> * Web server xác định loại yêu cầu (GET, POST, PUT, DELETE) và phân tích URI (Uniform Resource Identifier).
> * Dựa vào URI và các quy tắc cấu hình, web server quyết định làm gì với yêu cầu (ví dụ: truy cập tệp tin, thực thi mã nguồn, gửi lại trang web đã lưu trữ trước đó).
3. Tạo và gửi phản hồi (Response Generation):
> * Dựa vào loại yêu cầu và nội dung yêu cầu, web server tạo ra một phản hồi HTTP.
> * Phản hồi này có thể là một trang HTML, một tệp tin, hoặc một mã trạng thái (status code).
> * Phản hồi được gửi trở lại cho máy khách thông qua giao thức TCP/IP.
4. Kết thúc kết nối (Connection Closure):
> * Sau khi phản hồi được gửi đi, kết nối TCP/IP có thể được đóng hoặc duy trì để hỗ trợ keep-alive (giữ kết nối mở để giảm độ trễ trong việc thiết lập kết nối mới).
5. Ghi log và theo dõi (Logging and Monitoring):
> * Web server có thể ghi lại thông tin về các yêu cầu đã xử lý và hoạt động của máy chủ để phân tích và theo dõi hiệu suất.