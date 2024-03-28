---
title : "Provider"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 1.2 </b> "
---

#### Terraform Provider



**Terraform Provider** là một phần mềm đóng vai trò như một cầu nối giữa Terraform và một nền tảng cụ thể, ví dụ như Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform,.. Cho phép Terraform tương tác với các API của nền tảng đã tạo, quản lý và cập nhật tài nguyên.
**Chức năng chính**:
* **Tao tài nguyên**: Nhà cung cấp Terraform cung cấp các hàm và API để tạo các tài nguyên mới trên nền tảng cụ thể.
* **Quản lý tài nguyên**: Cho phép Terraform cập nhật, thay đổi cấu hình và xóa các tài nguyên hiện có.
* **Cung cấp trạng thái**: Theo dõi trạng thái của các tài nguyên, giúp Terraform xác định những thay đổi cần thực hiện. 

 **Ví dụ**:
* **AWS Provider**: Cho phép Terraform tương tác với các dịch vụ AWS như EC2, S3, RDS, v.v.
* **Azure Provider**: Cho phép Terraform tương tác với các dịch vụ Azure như VM, Storage, SQL Database, v.v.
* **GCP Provider**: Cho phép Terraform tương tác với các dịch vụ GCP như Compute Engine, Cloud Storage, Cloud SQL, v.v.

![Route Tables](/images/1-Introduce/terraformproviders.png?featherlight=false&width=30pc)