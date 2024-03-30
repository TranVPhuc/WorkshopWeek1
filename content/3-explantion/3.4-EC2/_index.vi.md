---
title : "Cấu hình EC2"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 3.4. </b> "
---

#### Cấu hình EC2 Instance
```
resource "aws_instance" "web-server-instance" {
  ami               = "ami-085925f297f89fce1"
  instance_type     = "t2.micro"
  availability_zone = "us-east-1a"
  key_name          = "web-server-key"

  network_interface {
    device_index         = 0
    network_interface_id = aws_network_interface.web-server-nic.id
  }

  user_data = <<-EOF
                #!/bin/bash
                sudo apt update -y
                sudo apt install apache2 -y
                sudo systemctl start apache2
                sudo bash -c 'echo your very first web server > /var/www/html/index.html'
                EOF
  tags = {
    Name = "web-server"
  }
}
```
Đoạn mã trên là một mô tả của một tài nguyên EC2 instance (một máy chủ ảo) trong AWS, được tạo ra và quản lý bởi Terraform.
Định nghĩa tài nguyên  
*** resource "aws_instance" "web-server-instance**": Dòng này định nghĩa một tài nguyên thuộc loại aws_instance và gán cho nó tên web-server-instance. Tên này sẽ được sử dụng để tham khảo đến máy chủ cụ thể này trong cấu hình Terraform của bạn.
Cấu hình máy chủ
* **ami = "ami-085925f297f89fce1"**: Dòng này chỉ định Amazon Machine Image (AMI) để sử dụng cho việc khởi chạy máy chủ. Bạn có thể tìm thấy các AMI khác nhau trong AWS Marketplace hoặc tạo AMI tùy chỉnh của riêng bạn.
* **instance_type = "t2.micro"**: Dòng này xác định loại máy chủ sẽ được khởi chạy. Trong trường hợp này, nó là **t2.micro**.
* **availability_zone = "us-east-1a"**: Dòng này chỉ định **Availability Zone** (AZ) nơi máy chủ sẽ được khởi chạy.
Cấu hình mạng
network_interface { ... }: Khối này định nghĩa giao diện mạng cho máy chủ. Terraform dường như đang tham chiếu đến một tài nguyên **Network Interface** hiện có tên aws_network_interface.web-server-nic

User Data:
+ **user_data = <<-EOF ... EOF**: Định nghĩa một tập lệnh sẽ được thực thi trên máy chủ trong lần khởi động đầu tiên. Tệp lệnh sử dụng #!/bin/bash để thực hiện các hành động sau:
>+ **sudo apt update -y**: Cập nhật danh sách gói cho trình quản lý gói.

>+ **sudo apt install apache2 -y**: Cài đặt phần mềm máy chủ web Apache.

>+ **sudo systemctl start apache2**: Khởi động dịch vụ máy chủ web Apache.

>+ **sudo bash -c 'echo your very first web server > /var/www/html/index.html'**: Tạo một tệp index.html đơn giản với văn bản "your very first web server" trong thư mục gốc tài liệu của máy chủ web (/var/www/html).
Tag:
>+ **tags = { Name = "web-server" }**: Dòng này gán một thẻ tên "Name" với giá trị "web-server" cho máy chủ.