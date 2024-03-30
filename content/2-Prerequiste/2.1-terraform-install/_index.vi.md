---
title : "Cài đặt Terraform"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 2.1. </b> "
---
#### Cài đặt Terraform

**Bước 1**: Tải xuống Terraform
Truy cập trang web chính thức của Terraform https://developer.hashicorp.com/terraform sau đó nhấn vào install, chọn phiên bản phù hợp với hệ điều hành của bạn. Ở Window ta có 2 phiên bản 386 và AMD64, chọn 1 trong 2

![Downloadsite](/images/2.1-terraform-install/00007.png?featherlight=false&width=70pc)
![OS](/images/2.1-terraform-install/00008.png?featherlight=false&width=70pc)
**Bước 2**: Giải nén Terraform
Sau khi tải xuống giải nén gói Terraform. Vị trí giải nén tùy thuộc vào bạn. Ở đây ta giải nén vào thư mục `C:\Program Files\Terraform`.
**Bước 3**: Thêm Terraform vào PATH
Để sử dụng Terraform từ bất kỳ thư mục nào, bạn cần thêm nó vào PATH của hệ thống.
1. Ở phần Search của Window nhập Advanced system settings.
2. Chuyển qua tab **Advanced**, chọn **Enviroment Variables**.
![PATH](/images/2.1-terraform-install/00003.png?featherlight=false&width=26pc)
3. Chọn Path và nhấn Edit
![PATH](/images/2.1-terraform-install/00004.png?featherlight=false&width=26pc)
4. Chọn New và nhập đường dẫn đến thư mục Terraform và nhấn OK/
![PATH](/images/2.1-terraform-install/00005.png?featherlight=false&width=26pc)
5. Kiểm tra cài đặt Terraform thành công chưa bằng cách nhập lệnh ```terrraform --version``` trong cmd. Nếu khi nhập lệnh mà hiện ra version của Terraform tức là bạn đã cài đặt Terraform thành công.
![Advancedsystem](/images/2.1-terraform-install/00006.png?featherlight=false&width=50pc)
