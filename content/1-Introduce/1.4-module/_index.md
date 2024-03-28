---
title : "Terraform Module"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 1.4 </b> "
---

#### Terraform Module

A **Terraform Module** is a feature that allows you to divide Terraform code into smaller, more manageable parts. It's similar to functions or classes in programming, helping to reuse code and organize infrastructure structure efficiently.

**Benefits of Using Terraform Modules::**
* **Benefits of Using Terraform Modules:**: You can create modules for common infrastructure components, such as virtual machines, networks, or databases, and reuse them in multiple projects.
* **Maintainability**: Dividing code into smaller modules makes it easier to search, debug, and update code.un nhỏ giúp bạn dễ dàng tìm kiếm, sửa lỗi và cập nhật mã hơn.
* **Collaboration**: You can share modules with other members of your team to collaborate on developing and managing infrastructure together.
*Example of a Terraform Module
```
module "aws_ec2_instance" {
  source = "hashicorp/aws/modules/ec2-instance"

  name = "my-instance"

  ami = "ami-01234567890abcdef0"
  instance_type = "t2.micro"

  count = 2
}
```
This module can be used in any Terraform project to create an AWS EC2 virtual machine.
