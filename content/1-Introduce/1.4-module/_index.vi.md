---
title : "Module"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 1.4 </b> "
---

#### Terraform Module

Terraform Module là một tính năng cho phép bạn chia mã Terraform thành các phần nhỏ, dễ quản lý hơn. Nó tương tự như các hàm hoặc các lớp trong lập trình, giúp tái sử dụng code và tổ chức cấu trúc hạ tầng một cách hiệu quả.

**Lợi ích của việc sử dụng Terraform Module:**
* **Tái sử dụng mã**: Bạn có thể tạo các mô-đun cho các thành phần cơ sở hạ tầng phổ biến, chẳng hạn như máy chủ ảo, mạng hoặc cơ sở dữ liệu, và sử dụng lại chúng trong nhiều dự án khác nhau.
* **Khả năng bảo trì**: Chia mã thành các mô-đun nhỏ giúp bạn dễ dàng tìm kiếm, sửa lỗi và cập nhật mã hơn.
* **Tính cộng tác**: Bạn có thể chia sẻ các mô-đun với các thành viên khác trong nhóm của mình để cùng nhau phát triển và quản lý cơ sở hạ tầng.
*Ví dụ về module Terraform
```
module "aws_ec2_instance" {
  source = "hashicorp/aws/modules/ec2-instance"

  name = "my-instance"

  ami = "ami-01234567890abcdef0"
  instance_type = "t2.micro"

  count = 2
}
```
Mô-đun này có thể được sử dụng trong bất kỳ dự án Terraform nào để tạo ra một máy chủ ảo AWS EC2.
