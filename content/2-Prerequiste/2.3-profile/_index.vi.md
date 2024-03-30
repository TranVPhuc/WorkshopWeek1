---
title : "Thêm Profile AWS bằng AWS CLI"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 2.3.</b> "
---

### Thêm Profile AWS cho Terraform
Cài đặt **AWS CLI**
* Đảm bảo rằng bạn đã cài đặt **Python** trên hệ thống của bạn. AWS CLI yêu cầu Python 2 version 2.6.5+ hoặc Python 3 version 3.3+.
* Truy cập trang Web tải **AWS CLI** [tại đây](https://aws.amazon.com/vi/cli/) và tải AWS CLI phù hợp với hệ điều hành của bạn. Ở đây ta dùng Window. Sau khi cài đặt xong bạn có thể kiểm tra AWS CLI đã cài đặt thành công chưa bằng lệnh `aws --version `
![awscli](/images/2.3-aws-cli/00001.png?featherlight=false&width=70pc)
![awscli](/images/2.3-aws-cli/00002.png?featherlight=false&width=60pc)
Thêm **Profile AWS** cho Terraform bằng **AWS CLI**
* Mở terminal hoặc command prompt.
* Chạy lệnh `aws configure --profile <profile-name> ` và tuân thủ theo hướng dẫn. Thay `<profile-name>` bằng tên profile bạn muốn sử dụng cho Terraform.
* **AWS CLI** sẽ hỏi bạn về **Access Key ID**, **Secret Access Key**, **region** và định dạng **output** (ví dụ: JSON). Nhập các giá trị tương ứng và nhấn Enter.
* Sau khi bạn đã nhập đầy đủ, AWS CLI sẽ tạo một cấu hình mới trong tệp ~/.aws/credentials (trên Linux/macOS) hoặc tệp %USERPROFILE%.aws\credentials (trên Windows) với tên cấu hình được chỉ định.