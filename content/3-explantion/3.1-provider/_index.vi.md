---
title : "Thiết lập kết nối đến tài khoản AWS"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1.</b> "
---

### Thiết lập kết nối đến tài khoản AWS
```
provider "aws" {
  region     = "us-east-1"
  shared_config_files      = ["~/.aws/config"]
  shared_credentials_files = ["~/.aws/credentials"]
  profile                  = "terraform"
}
```
Đoạn mã trên là một phần cấu hình của Terraform để sử dụng dịch vụ **AWS (Amazon Web Services)**.

* **provider "aws"**: Đây là khai báo một provider cho Terraform, cụ thể là AWS.
* **region = "us-east-1"**: Đây là cấu hình cho khu vực (region) mà các tài nguyên sẽ được tạo ra. Trong trường hợp này, khu vực được chọn là "us-east-1".
* **shared_config_files = ["~/.aws/config"]**: Đây là đường dẫn tới tệp cấu hình chung (shared configuration files) của AWS. Trong trường hợp này, tệp cấu hình được sử dụng là "~/.aws/config".
* **shared_credentials_files = ["~/.aws/credentials"]**: Đây là đường dẫn tới tệp chứa thông tin xác thực chung (shared credentials files) của AWS. Trong trường hợp này, tệp chứa thông tin xác thực được sử dụng là "~/.aws/credentials".
* **profile = "terraform":** Đây là tên của profile (hồ sơ) trong tệp cấu hình và tệp chứa thông tin xác thực. Trong trường hợp này, tên profile được sử dụng là "terraform".
