---
title : "Terraform State"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 1.5 </b> "
---

#### Terraform State

Terraform State là một tập dữ liệu lưu trữ thông tin về các tài nguyên cơ sở hạ tầng mà Terraform đã quản lý. Bao gồm:
* Tên và loại mỗi tài nguyên.
* Thuộc tính mỗi tài nguyên.
* Mối quan hệ giữa các tài nguyên.

**Mục đích**:
* Theo dõi các thay đổi đối với cơ sở hậ tầng.
* Xác định các tài nguyên cần được tạo, cập nhật hoặc xóa.
* Giữ cho cơ sở hạ tầng của bạn nhất quán với cấu hình Terraform.

**Các loại Terraform State**:
* **Trạng thái cục bộ**: được lưu trữ trong tệp `.tfstate` trong thư mục dự án Terraform của bạn.
* **Trạng thái xa**: được lưu trữ trong kho lưu trữ từ xa, chẳng hạn như HashiCorp Vault.

**Ví dụ về thông tin của một máy ảo AWS sau khi được tạo**:
```
{
  "resources": {
    "aws_instance.web_server": {
      "type": "aws_instance",
      "name": "web_server",
      "count": 1,
      "primary": {
        "id": "i-1234567890abcdef0",
        "attributes": {
          "ami_id": "ami-1234567890abcdef0",
          "instance_type": "t2.micro",
          "public_ip": "123.45.67.89"
        }
      }
    }
  }
}
```

{{%notice tip%}}
Có một số công cụ Terraform có thể giúp bạn quản lý trạng thái Terraform, chẳng hạn như Terraform State Viewer và Terraform State Diff.
{{%/notice%}}