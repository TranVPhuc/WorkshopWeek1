---
title : "Khởi tạo VPC và cấu hình kết nối"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

#### Khởi tạo VPC và cấu hình kết nối

1. Khởi tạo **VPC**:
```
resource "aws_vpc" "prod-vpc" {
  cidr_block = "10.0.0.0/16"
  tags = {
    Name = "production"
  }
}
```

Đoạn mã trên được sử dụng để tạo một **VPC (Virtual Private Cloud)** trên Amazon Web Services (AWS).
* **resource "aws_vpc" "prod-vpc"**: Đây là khai báo một tài nguyên loại **aws_vpc**, nơi **"prod-vpc"** là tên mà bạn gán cho tài nguyên này. Trong Terraform, các tài nguyên có thể được tham chiếu thông qua tên này sau khi được tạo.
* **cidr_block = "10.0.0.0/16"**: Đây là phần quan trọng để định rõ phạm vi mạng của VPC. **CIDR block** là cách xác định phạm vi các địa chỉ IP mà VPC sẽ sử dụng. Trong trường hợp này, CIDR block là "10.0.0.0/16", có nghĩa là **VPC** sẽ có địa chỉ IP khả dụng bắt đầu từ 10.0.0.0 đến 10.0.255.255.
* **tags = { Name = "production" }**: Đây là phần tags (nhãn) được gán cho tài nguyên. Trong trường hợp này, có một tag duy nhất được gán với key là "Name" và value là "production". Tags có thể được sử dụng để tổ chức và quản lý các tài nguyên trong môi trường AWS.

2. Khởi tạo Internet Gateway
```
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.prod-vpc.id
}
```
Đoạn mã này tạo một **Internet Gateway (IGW)** trên AWS và gắn nó với **VPC** đã được tạo trước đó trong đoạn mã trước.
* **resource "aws_internet_gateway" "gw"**: Đây là khai báo một tài nguyên loại **aws_internet_gateway**, nơi "gw" là tên mà bạn gán cho tài nguyên này. Tương tự như trước, bạn có thể tham chiếu tài nguyên này sau khi nó được tạo.
* **vpc_id = aws_vpc.prod-vpc.id**: Thuộc tính **vpc_id** chỉ định **VPC** mà **IGW** sẽ được gắn vào. Trong trường hợp này, **IGW** sẽ được gắn vào **VPC** có ID được xác định bằng cách tham chiếu đến tài nguyên **aws_vpc.prod-vpc** và truy cập thuộc tính **id** của nó. Điều này đảm bảo rằng **IGW** sẽ được gắn vào **VPC** đã được tạo trước với tên là **"prod-vpc"**.

3. Khởi tạo Route Table
```
resource "aws_route_table" "prod-route-table" {
  vpc_id = aws_vpc.prod-vpc.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.gw.id
  }

  route {
    ipv6_cidr_block = "::/0"
    gateway_id      = aws_internet_gateway.gw.id
  }

  tags = {
    Name = "Prod"
  }
}
```
Đoạn mã trên tạo một **bảng định tuyến (route table)** trên AWS và cấu hình các tuyến đường (routes) cho **VPC** đã được tạo trước đó. Khi mã này được thực thi, nó sẽ tạo ra một bảng định tuyến và cấu hình các tuyến đường cho VPC đã được tạo trước đó, cho phép các tài nguyên trong VPC có thể truy cập Internet.
* **resource "aws_route_table" "prod-route-table"**: Đây là khai báo một tài nguyên loại **aws_route_table**, nơi **"prod-route-table"** là tên mà bạn gán cho tài nguyên này.
* **vpc_id = aws_vpc.prod-vpc.id**: Thuộc tính **vpc_id** xác định **VPC** mà bảng định tuyến sẽ được áp dụng. Trong trường hợp này, **Route Table** này được áp dụng cho **VPC** có **ID** được xác định bằng cách tham chiếu đến tài nguyên **aws_vpc**.**prod-vpc** và truy cập thuộc tính id của nó.
* **route { cidr_block = "0.0.0.0/0" gateway_id = aws_internet_gateway.gw.id }**: Đây là cấu hình tuyến đường cho các địa chỉ IPv4. Tuyến đường này sẽ chuyển hết các gói tin có đích đến là bất kỳ địa chỉ IP nào (CIDR block là "0.0.0.0/0") đến **Internet Gateway** đã được tạo trước đó. Điều này cho phép các tài nguyên trong **VPC** có thể truy cập Internet.
* **route { ipv6_cidr_block = "::/0" gateway_id = aws_internet_gateway.gw.id }**: Đây là cấu hình tuyến đường cho các địa chỉ IPv6. Tương tự như tuyến đường IPv4, tuyến đường này cũng sẽ chuyển hết các gói tin IPv6 có đích đến là bất kỳ địa chỉ IP nào (CIDR block là "::/0") đến **Internet Gateway** đã được tạo trước đó.
* **tags = { Name = "Prod" }**: Đây là phần tags (nhãn) được gán cho bảng định tuyến. Trong trường hợp này, có một tag duy nhất được gán với key là "Name" và value là "Prod".

3. Khởi tạo subnet
```
resource "aws_subnet" "subnet-1" {
  vpc_id            = aws_vpc.prod-vpc.id
  cidr_block        = "10.0.1.0/24"
  availability_zone = "us-east-1a"

  tags = {
    Name = "prod-subnet"
  }
}
```
Đoạn code này tạo ra một **subnet** với các thông số nhất định, bao gồm VPC, phạm vi địa chỉ IP, khu vực phân phối và các thẻ trên dịch vụ điện toán đám mây của Amazon Web Services (AWS).
* **resource "aws_subnet" "subnet-1"**: Đây là khai báo một tài nguyên loại **aws_subnet**, nơi **subnet-1** là tên mà bạn gán cho **subnet** này.
* **vpc_id = aws_vpc.prod-vpc.id**: Thuộc tính *vpc_id* chỉ định **ID** của **VPC** mà subnet sẽ thuộc về. Trong trường hợp này, nó đang chỉ định rằng subn**et sẽ thuộc về **VPC** có **ID** được xác định bằng cách tham chiếu đến tài nguyên **aws_vpc.prod-vpc** và truy cập thuộc tính id của nó.
* **cidr_block = "10.0.1.0/24"**: Thuộc tính **cidr_block** xác định phạm vi địa chỉ **IP** của **subnet**. Trong trường hợp này, **subnet** sẽ có phạm vi từ 10.0.1.0 đến 10.0.1.255, với 256 địa chỉ IP khả dụng.
* **availability_zone = "us-east-1a"**: Thuộc tính availability_zone xác định khu vực mà **subnet** sẽ được tạo ra. Trong trường hợp này, **subnet** sẽ được tạo ra trong khu vực "us-east-1a".
* **tags = { Name = "prod-subnet" }**: Đây là phần tags (nhãn) được gán cho **subnet**. Trong trường hợp này, có một tag duy nhất được gán với key là "Name" và value là **"prod-subnet"**. Tags có thể được sử dụng để tổ chức và quản lý các tài nguyên trong môi trường AWS.

4. Liên kết **subnet** với **route table**
```
resource "aws_route_table_association" "a" {
  subnet_id      = aws_subnet.subnet-1.id
  route_table_id = aws_route_table.prod-route-table.id
}
```

The code above defines an association between a **subnet** and a **route table** in the AWS environment.

* **resource "aws_route_table_association" "a"**: Đây là khai báo một tài nguyên của loại aws_route_table_association, nơi "a" là tên mà bạn gán cho tài nguyên này.

* **subnet_id = aws_subnet.subnet-1.id**: Thuộc tính subnet_id xác định subnet mà liên kết này sẽ áp dụng đến. Trong trường hợp này, nó đang chỉ định rằng liên kết này áp dụng cho subnet có ID được xác định bằng cách tham chiếu đến tài nguyên aws_subnet.subnet-1 và truy cập thuộc tính id của nó.

* **route_table_id = aws_route_table.prod-route-table.id**: Thuộc tính route_table_id xác định **Route Table** mà liên kết này sẽ được áp dụng. Trong trường hợp này, nó đang chỉ định rằng liên kết này sẽ áp dụng cho **Route Table** có ID được xác định bằng cách tham chiếu đến tài nguyên **aws_route_table**.prod-route-table và truy cập thuộc tính id của nó.