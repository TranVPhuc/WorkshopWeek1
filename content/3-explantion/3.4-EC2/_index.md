---
title : "Configure EC2 instance"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3.3.  </b> "
---

#### Configure EC2 Instance
```
resource "aws_instance" "web-server-instance" {
  ami               = "ami-085925f297f89fce1"
  instance_type     = "t2.micro"
  availability_zone = "us-east-1a"
  key_name          = "web-server-key"

  network_interface {
    device_index         = 0
    network_interface_id = aws_network_interface.web-server-nic.id
  }

  user_data = <<-EOF
                #!/bin/bash
                sudo apt update -y
                sudo apt install apache2 -y
                sudo systemctl start apache2
                sudo bash -c 'echo your very first web server > /var/www/html/index.html'
                EOF
  tags = {
    Name = "web-server"
  }
}
```

The code above is a description of an EC2 instance resource (a virtual server) in AWS, created and managed by Terraform.
  
* **resource "aws_instance" "web-server-instance"**: defines a resource of type aws_instance and assigns it the name web-server-instance. This name will be used to reference this specific server in your Terraform configuration.

* **ami = "ami-085925f297f89fce1"**: This line specifies the Amazon Machine Image (AMI) to use for launching the server. You can find different AMIs in the AWS Marketplace or create your own custom AMI.
* **instance_type = "t2.micro"**: This line specifies the instance type that will be launched. In this case, it is **t2.micro**.
* **availability_zone = "us-east-1a"**: This line specifies the **Availability Zone (AZ)** where the instance will be launched.

* **network_interface { ... }**: This block defines the network interface for the server. Terraform seems to be referencing an existing resource named **aws_network_interface.web-server-nic**.

* **user_data = <<-EOF ... EOF**: This defines a set of commands to be executed on the server during the first boot. The script uses #!/bin/bash to perform the following actions:
>+ **sudo apt update -y**: Updates the package list for the package manager.
>+ **sudo apt install apache2 -y**:  Installs the Apache web server software.
>+ **sudo systemctl start apache2**:  Starts the Apache web server service.
>+ **sudo bash -c 'echo your very first web server > /var/www/html/index.html'**: Creates a simple index.html file with the text "your very first web server" in the root document directory of the web server (/var/www/html).
* **tags = { Name = "web-server" }**: This line assigns a tag named "Name" with the value "web-server" to the server.