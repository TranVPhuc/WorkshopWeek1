---
title : "Security Group và Network Interface"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

#### Khởi tạo Security Group và Network Interface
Khởi tạo **Security Group**
```
resource "aws_security_group" "allow_web" {
  name        = "allow_web_traffic"
  description = "Allow Web inbound traffic"
  vpc_id      = aws_vpc.prod-vpc.id

  ingress {
    description = "HTTPS"
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "allow_web"
  }
}
```
Đoạn mã trên định nghĩa một **Security Group** trên **AWS**, cho phép lưu lượng web vào và ra khỏi các máy chủ trong **VPC** đã được chỉ định.

* **resource "aws_security_group" "allow_web"**: Đây là khai báo một tài nguyên của loại aws_security_group, nơi "allow_web" là tên mà bạn gán cho nhóm bảo mật này.
*** name = "allow_web_traffic"**: Thuộc tính name xác định tên của nhóm bảo mật. Trong trường hợp này, tên của nhóm bảo mật được đặt là "allow_web_traffic".
* **description = "Allow Web inbound traffic"**: Thuộc tính description cung cấp mô tả cho nhóm bảo mật. Trong trường hợp này, mô tả là "Allow Web inbound traffic"
* **vpc_id = aws_vpc.prod-vpc.id**: Thuộc tính vpc_id xác định VPC mà nhóm bảo mật này thuộc về. Trong trường hợp này, nhóm bảo mật sẽ thuộc về VPC có ID được xác định bằng cách tham chiếu đến tài nguyên aws_vpc.prod-vpc và truy cập thuộc tính id của nó.
* **ingress và egress**: Các khối này định nghĩa các quy tắc định tuyến (lưu lượng vào và ra) cho nhóm bảo mật. Trong trường hợp này:
>* **ingress** định nghĩa các quy tắc cho lưu lượng vào. Ba quy tắc đã được định nghĩa ở đây để cho phép lưu lượng HTTPS (port 443), HTTP (port 80) và SSH (port 22) từ bất kỳ địa chỉ IP nào ("0.0.0.0/0").
>* **egress** định nghĩa các quy tắc cho lưu lượng ra. Trong trường hợp này, nó cho phép mọi lưu lượng ra đến bất kỳ địa chỉ IP nào ("0.0.0.0/0").
* **tags = { Name = "allow_web" }**: Đây là phần tags (nhãn) được gán cho nhóm bảo mật. Trong trường hợp này, có một tag duy nhất được gán với key là "Name" và value là "allow_web". Tags có thể được sử dụng để tổ chức và quản lý các tài nguyên trong môi trường AWS.
Khởi tạo **NetWork Interface**
```
resource "aws_network_interface" "web-server-nic" {
  subnet_id       = aws_subnet.subnet-1.id
  private_ips     = ["10.0.1.50"]
  security_groups = [aws_security_group.allow_web.id]
}
```
Đoạn mã này tạo ra một Network Interace trong một subnet cụ thể, gán cho nó một địa chỉ IP riêng, và liên kết với một Security Group.
* **resource "aws_network_interface" "web-server-nic"**: Đây là khai báo một tài nguyên của loại aws_network_interface, nơi "web-server-nic" là tên mà bạn gán cho NIC này.
* **subnet_id = aws_subnet.subnet-1.id**: Thuộc tính subnet_id xác định subnet mà NIC sẽ được gắn vào. Trong trường hợp này, nó đang chỉ định rằng NIC sẽ được gắn vào subnet có ID được xác định bằng cách tham chiếu đến tài nguyên aws_subnet.subnet-1 và truy cập thuộc tính id của nó.

* **private_ips = ["10.0.1.50"]**: Thuộc tính private_ips chỉ định địa chỉ IP riêng cho NIC. Trong trường hợp này, NIC sẽ có địa chỉ IP là "10.0.1.50" trong subnet đã được chỉ định.

* **security_groups = [aws_security_group.allow_web.id]**: Thuộc tính security_groups xác định các nhóm bảo mật mà NIC sẽ áp dụng. Trong trường hợp này, NIC sẽ áp dụng quy tắc từ nhóm bảo mật có ID được xác định bằng cách tham chiếu đến tài nguyên aws_security_group.allow_web và truy cập thuộc tính id của nó. Điều này đảm bảo rằng NIC sẽ tuân thủ các quy tắc lưu lượng đã được định nghĩa trong nhóm bảo mật này.

Gán **Elastic IP** vào **Network Interface**
```
resource "aws_eip" "one" {
  domain                    = "vpc"
  network_interface         = aws_network_interface.web-server-nic.id
  associate_with_private_ip = "10.0.1.50"
  depends_on = [ aws_internet_gateway.gw,aws_instance.web-server-instance ]
}

output "server_public_ip" {
  value = aws_eip.one.public_ip
}
```
Đoạn mã trên được sử dụng để tạo một địa chỉ **IP động (Elastic IP)** trên **Amazon Web Services (AWS)** và gán nó vào một **Network Interface** trong một môi trường **VPC (Virtual Private Cloud).**
* **domain**: Được đặt thành "vpc", cho biết EIP dành cho môi trường VPC.
* **network_interface**: Thấm chiếm ID của **Network Interface** hiện có (aws_network_interface.web-server-nic.id). EIP sẽ được liên kết với **Network Interface** này.
* **associate_with_private_ip**: Chỉ định **private IP** (10.0.1.50) trong VPC mà EIP sẽ liên kết đến. 
* **depends_on**: Đảm bảo rằng EIP (aws_eip.one) chỉ được tạo sau khi Internet Gateway (aws_internet_gateway.gw) và Instance (aws_instance.web-server-instance) được tạo.
* **value**: Tham chiếu thuộc tính public_ip của tài nguyên aws_eip.one. Thuộc tính này sẽ ghi lại địa chỉ IP công khai được gán cho EIP và hiển thị ở Terminal.