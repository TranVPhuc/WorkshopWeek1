---
title : "Deloy Web Server"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Deloy Web Server
- Để có thể khởi chạy được Project, sau khi tải file Project, giải nén file Project ở bất cứ đâu bạn muốn. Sau đó thay **access key** và **secret key** của bạn ở khối provider.
- Tiếp đến mở file bằng **Visual Studio Code** và nhấn tổ hợp phím **Ctrl** + **Shift** + **`** để mở bảng Terminal.
- Nhập `terraform apply` sau đó nhập `yes` ở bảng terminal để xác nhận thay đổi.
![initiate](/images/2.2-deloy/00001.png?featherlight=false&width=30pc)
![initiate](/images/2.2-deloy/00002.png?featherlight=false&width=30pc).
- Khi bảng **Terminal** hiển thị **Apply completed** và hiển thị **Server_IP** tức là Terraform đã **Deloy** thành công. Giờ chỉ nhập dãy **IP** vào một trình duyệt bất kì là ta có thể truy cập vào Web Server của chúng ta.
![initiate](/images/2.2-deloy/00003.png?featherlight=false&width=65pc).
![initiate](/images/2.2-deloy/00004.png?featherlight=false&width=70pc).