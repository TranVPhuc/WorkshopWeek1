---
title : "Security Group and Network Interface"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

#### Create Security Group và Network Interface
Create **Security Group**
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

The code snippet above defines a **Security Group** on **AWS**, allowing web traffic in and out of the designated servers within the specified **VPC**.

* **resource "aws_security_group" "allow_web"**: This is a declaration of a resource of type aws_security_group, where "allow_web" is the name you assign to this security group.
name = "allow_web_traffic": The name attribute specifies the name of the security group. In this case, the security group is named "allow_web_traffic".

* **description = "Allow Web inbound traffic"**: The description attribute provides a description for the security group. In this case, the description is "Allow Web inbound traffic".

* **vpc_id = aws_vpc.prod-vpc.id**: The vpc_id attribute identifies the VPC to which this security group belongs. In this case, the security group belongs to the VPC with the ID determined by referencing the aws_vpc.prod-vpc resource and accessing its id attribute.

* **ingress and egress**: These blocks define the routing rules (inbound and outbound traffic) for the security group. In this case:

* **ingress**: defines rules for inbound traffic. Three rules are defined here to allow HTTPS traffic (port 443), HTTP traffic (port 80), and SSH traffic (port 22) from any IP address ("0.0.0.0/0").

* **egress**: defines rules for outbound traffic. In this case, it allows all outbound traffic to any IP address ("0.0.0.0/0").

* **tags = { Name = "allow_web" }:** This is the tags section where labels are assigned to the security group. In this case, a single tag is assigned with the key "Name" and the value "allow_web". Tags can be used to organize and manage resources in the AWS environment.


Create **NetWork Interface**
```
resource "aws_network_interface" "web-server-nic" {
  subnet_id       = aws_subnet.subnet-1.id
  private_ips     = ["10.0.1.50"]
  security_groups = [aws_security_group.allow_web.id]
}
```
This code creates a **network interface** within a specified **subnet**, assigns it a private IP address, and associates it with a **Security Group**.
* **resource "aws_network_interface" "web-server-nic"**: This is a declaration of a resource of type aws_network_interface, where "web-server-nic" is the name you assign to this Network Interface (NIC).
* **subnet_id = aws_subnet.subnet-1.id**: The subnet_id attribute identifies the subnet that the NIC will be attached to. In this case, it specifies that the NIC will be attached to the subnet with the ID determined by referencing the aws_subnet.subnet-1 resource and accessing its id attribute.
* **private_ips = ["10.0.1.50"]**: The private_ips attribute specifies the private IP address for the NIC. In this case, the NIC will have the IP address "10.0.1.50" within the specified subnet.
* **security_groups = [aws_security_group.allow_web.id]**: The security_groups attribute identifies the security groups that the NIC will apply. In this case, the NIC will apply the rules from the security group with the ID determined by referencing the aws_security_group.allow_web resource and accessing its id attribute. This ensures that the NIC will adhere to the traffic rules defined in this security group.

Assign an **Elastic IP** to the **Network Interface**.
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

After applying this Terraform configuration, you can access the public IP address associated with Elastic IP "one" using the output variable server_public_ip.
* **domain**: Set to "vpc", indicating that the EIP is intended for the VPC environment.
* **network_interface**: Specifies the ID of the current Network Interface (aws_network_interface.web-server-nic.id). The EIP will be associated with this Network Interface.
* **associate_with_private_ip**: Specifies the private IP address (10.0.1.50) within the VPC to which the EIP will be associated.
* **depends_on**: Ensures that the EIP (aws_eip.one) is created only after the Internet Gateway (aws_internet_gateway.gw) and Instance (aws_instance.web-server-instance) are created.
* **value**: References the public_ip attribute of the aws_eip.one resource. This attribute will capture the public IP address assigned to the EIP and display it in the Terminal.