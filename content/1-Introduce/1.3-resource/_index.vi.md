---
title : "Resource"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 1.3 </b> "
---


#### Terraform Resource

Trong terraform, **resource (tài nguyên)** là các thành phần cơ bản cấu tạo nên cơ sở hạ tầng mà bạn quản lý với Terraform. Nó có thể bao gồm nhiều lại tài nguyên khác nhau, tùy thuộc vào nhà cung cấp dịch vụ đám mấy (cloud provider) mà bạn sử dụng. Chúng có thể bao gồm các loại tài nguyên sau:
* **Máy ảo**: EC2 instance trên AWS, Azure VM, Google Compute Engine
* **Mạng**: Bao gồm VPC, subnet, load balancer, firewall.
* **Lưu trữ**: S3 bucket trên AWS, Azure Blob Storage, Google Cloud Storage.
* **Các dịch vụ khác**: CloudWatch trên AWS, Azure Monitor, Google, Cloud Monitoring.

 **Đặc điểm của Terraform resource**:
* **Được định nghĩa bằng mã**: Sử dụng ngôn ngữ HashiCorp Configuration Language (HCL) để mô tả cấu hình mong muốn của tài nguyên.
* **Quản lý vòng đời**: Terraform có thể tạo, cập nhật và xóa tài nguyên một cách tự động.
* **Tính linh hoạt**: Hỗ trợ nhiều nhà cung cấp dịch vụ đám mây (cloud provider) và có thể được sử dụng để quản lý cơ sở hạ tầng on-premises.
* **Dễ sử dụng**: Cung cấp cú pháp đơn giản và dễ hiểu, giúp bạn dễ dàng bắt đầu sử dụng.

**Cú pháp sử dụng**:
```
provider "aws" {
  region = "us-east-1"
}
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  
  instance_type = "t2.micro"              
}

```
Trong ví dụ này:
* provider "aws" xác định chúng ta sẽ sử dụng AWS làm nhà cung cấp dịch vụ.
* resource "aws_instance" "example" định nghĩa một tài nguyên EC2 với tên là "example"
* `ami`: Chọn một AmazonMachine Image (AMI) để tạo instance. 
* instance_type: Chọn loại instance, ở đây là `t2.micro`.

{{%notice tip%}}
Có nhiều nhà cung cấp dịch vụ đám mây (cloud provider) hỗ trợ Terraform. Hãy đảm bảo rằng bạn chọn đúng nhà cung cấp cho nhu cầu của mình.
{{%/notice%}}
