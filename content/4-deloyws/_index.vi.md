---
title : "Deloy Web Server"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

#### Deloy Web Server

- Để chạy dự án, sau khi tải xuống tệp project, giải nén nó ở bất kỳ nơi nào bạn muốn.
- Tiếp theo, mở tệp bằng Visual Studio Code và nhấn tổ hợp phím **Ctrl** + **Shift** + **`** để mở **Terminal**.
- Nhập lệnh terraform apply và sau đó nhập yes trong terminal để xác nhận việc áp dụng cấu hình.
![initiate](/images/deloyws/00001.png?featherlight=false&width=75pc).
![initiate](/images/deloyws/00002.png?featherlight=false&width=75pc).
- When the **Terminal** displays **Apply completed** and shows the **Server_IP**, it means Terraform has successfully deployed the infrastructure. Now, simply enter the IP address into any browser, and you should be able to access our Web Server.
![initiate](/images/deloyws/00003.png?featherlight=false&width=75pc).
![initiate](/images/deloyws/00004.png?featherlight=false&width=75pc).