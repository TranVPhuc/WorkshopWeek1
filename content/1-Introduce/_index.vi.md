---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

#### Terraform

**Terraform** là một công cụ **mã nguồn mở (open source)** được sử dụng để quản lý cơ sở hạ tầng (infrastructure) dưới dạng mã (Infrastructure as Code - IaC). Terraform cho phép bạn định nghĩa và quản lý các tài nguyên cơ sở hạ tầng như máy ảo, mạng, lưu trữ, v.v. trên nhiều nhà cung cấp dịch vụ đám mây (cloud provider) khác nhau như AWS, Azure, Google Cloud Platform (GCP), Alibaba Cloud, v.v.

![Terraform](/images/1-Introduce/terraform.png?featherlight=false&width=26pc)


**Lợi ích của việc sử dụng Terraform:**
- **Tự động hóa**: Terraform giúp tự động hóa việc triển khai và quản lý cơ sở hạ tầng, giúp tiết kiệm thời gian và giảm thiểu lỗi do thao tác thủ công.
- **Tính nhất quán**: Terraform giúp đảm bảo tính nhất quán trong việc triển khai cơ sở hạ tầng trên các môi trường khác nhau.
- **Khả năng tái sử dụng**: Terraform cho phép bạn mô-đun hóa cơ sở hạ tầng và tái sử dụng các mô-đun này trong các dự án khác nhau.
- **Khả năng theo dõi**: Terraform giúp theo dõi trạng thái (state) của cơ sở hạ tầng, giúp bạn dễ dàng xác định các thay đổi đã được thực hiện.
Bây giờ chúng ta sẽ cùng nhau đi qua các khái niệm cơ bản nhất của Terraform.

#### Nội dung

- [Workflow](1.1-workflow/)
- [Provider](1.2-provider/)
- [Resource](1.3-resource/)
- [Module](1.4-module/)
- [State](1.5-state/)

