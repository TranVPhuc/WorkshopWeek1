---
title : "Workflow"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1.1 </b> "
---

#### Terraform Workflow

![Workflow](/images/1-Introduce/workflow.png?featherlight=false&width=51pc)

Workflow của Terraform thường bao gồm các bước sau:

1. **Thiết kế**:
* Xác định các tài nguyên cần thiết và mối quan hệ giữa chúng.
* Xây dựng cấu trúc thư mục và module nếu cần.
2. **Khởi tạo**:
* Tải và cài đặt các plugin cần thiết cho dự án.
* Terraform sẽ tạo ra một thư mục chứa các plugin cần thiết.
3. **Lập kế hoạch**:
* Terrraform sẽ so sánh trạng thái hiện tại với trạng thái mong muốn được định nghĩa trong mã hạ tầng và hiện thị những thay đổi dự kiến.
4. **Triển khai**:
* Terraform sẽ triển khai các thay đổi đã được lập kế hoạch. Lúc này, Terraform sẽ tạo, cập nhật hoặc xóa các tài nguyên cũng như cập nhật trạng thái.
5. **Quản lý trạng thái**:
* Terraform sử dụng một tập tin state để thao dõi trạng thái thực tế của hạ tầng so với mã mô tả.
* Trong quá trình triển khai, trạng thái này sẽ được cập nhật và lưu trữ một cách an toàn.
6. **Kiểm tra**:
* Sau khi triển khai, kiểm tra cấc tài nguyên đã dược triển khai có hoạt động đúng mong đợi không.
7. **Giám sát và bảo trì**:
* Sử dụng các công cụ giám sát và bảo trì phù hợp như CloudWatch.
8. **Thay đổi**:
* Khi cần thay đổi cấu hình, lặp lại quy trình từ bước thiết kế hoặc chỉnh sửa các tệp cấu hình Terraform.
9. **Giải phóng tài nguyên**:
* Khi không cần sử dụng các tài nguyên nữa, Terraform sẽ xóa các tài nguyên được quản lý và cập nhật trạng thái.



