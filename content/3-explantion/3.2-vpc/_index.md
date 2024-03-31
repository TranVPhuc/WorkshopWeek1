---
title : "Create VPC and configure connectivity "
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2.  </b> "
---

#### Create VPC and configure connectivity 

1. Create **VPC**:
```
resource "aws_vpc" "prod-vpc" {
  cidr_block = "10.0.0.0/16"
  tags = {
    Name = "production"
  }
}
```

The code snippet above is used to create a **VPC (Virtual Private Cloud)** on **Amazon Web Services (AWS)**.
* **cidr_block** = "10.0.0.0/16": This is an important part to specify the network range of the VPC. The **CIDR block** is a way to define the range of IP addresses that the VPC will use. In this case, the CIDR block is **"10.0.0.0/16"**, meaning the VPC will have available IP addresses ranging from 10.0.0.0 to 10.0.255.255.

* **tags = { Name = "production" }**: This is the tags section assigned to the resource. In this case, there is a single tag assigned with key "Name" and value "production". Tags can be used to organize and manage resources in the AWS environment.

2. Create Internet Gateway
```
resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.prod-vpc.id
}
```
This code creates an **Internet Gateway (IGW)** on **AWS** and attaches it to the VPC that was previously created in the preceding code snippet.
* **resource "aws_internet_gateway" "gw"**: This is a declaration of an **aws_internet_gateway** resource type, where **"gw"** is the name you assign to this resource. Similar to before, you can reference this resource after it is created.
* **vpc_id = aws_vpc.prod-vpc.id**: The **vpc_id** attribute specifies the **VPC** to which the I**G**W will be attached. In this case, the IGW will be attached to the **VPC** identified by referencing the **aws_vpc.prod-vpc** resource and accessing its id attribute. This ensures that the **IGW** will be attached to the previously created **VPC** named "prod-vpc".
3. Create Route Table
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
The code snippet above creates a **route table** on **AWS** and configures routes for the VPC that was created earlier. When this code is executed, it will generate a route table and configure routes for the previously created VPC, allowing resources within the VPC to access the internet.
* vpc_id = aws_vpc.prod-vpc.id: The vpc_id attribute identifies the **VPC** to which the route table will be applied. In this case, this **Route Table** is applied to the **VPC** with the ID identified by referencing the **aws_vpc.prod-vpc** resource and accessing its id attribute.
* route { cidr_block = "0.0.0.0/0" gateway_id = aws_internet_gateway.gw.id }: This configures routes for IPv4 addresses. This route will forward all packets destined for any IP address (CIDR block is "0.0.0.0/0") to the previously created Internet Gateway. This allows resources within the VPC to access the Internet.
* **route { ipv6_cidr_block = "::/0" gateway_id = aws_internet_gateway.gw.id }**: This configures routes for **IPv6** addresses. Similar to the **IPv4** route, this route will also forward all IPv6 packets destined for any IP address (CIDR block is "::/0") to the previously created Internet Gateway.llows resources within the VPC to access the Internet.
* t**ags = { Name = "Prod" }**: This is the tags section assigned to the route table. In this case, there is a single tag assigned with key "Name" and value "Prod".

3. Create Subnet
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

This code snippet creates a **subnet** with specific parameters, including *VPC*, **IP** address range, a**vailability zone**, and **tags**, on the Amazon Web Services (AWS) cloud computing service.
* **resource "aws_subnet" "subnet-1"**: This is a declaration of an aws_subnet resource type, where subnet-1 is the name you assign to this subnet.
* **vpc_id = aws_vpc.prod-vpc.id**: The vpc_id attribute specifies the ID of the VPC to which the subnet will belong. In this case, it is specifying that the subnet will belong to the VPC with the ID identified by referencing the aws_vpc.prod-vpc resource and accessing its id attribute.
* **cidr_block = "10.0.1.0/24"**: The cidr_block attribute defines the IP address range of the subnet. In this case, the subnet will have a range from 10.0.1.0 to 10.0.1.255, with 256 available IP addresses.
* **availability_zone = "us-east-1a**": The availability_zone attribute specifies the region where the subnet will be created. In this case, the subnet will be created in the "us-east-1a" region.
* **tags = { Name = "prod-subnet" }**: This is the tags section assigned to the subnet. In this case, there is a single tag assigned with key "Name" and value "prod-subnet". Tags can be used to organize and manage resources in the AWS environment.

4.  Linking the subnet with the route table
```
resource "aws_route_table_association" "a" {
  subnet_id      = aws_subnet.subnet-1.id
  route_table_id = aws_route_table.prod-route-table.id
}
```
This code snippet associates the subnet "subnet-1" with the route table "prod-route-table". This way, instances launched in the subnet "subnet-1" will use the routes declared in the "prod-route-table" to route traffic between the VPC and the internet gateway.

* **resource "aws_route_table_association" "a"**: This is a declaration of a resource of type aws_route_table_association, where "a" is the name you assign to this resource.
* **subnet_id = aws_subnet.subnet-1.id:** The subnet_id attribute specifies the subnet to which this association will apply. In this case, it is specifying that this association applies to the subnet with the ID identified by referencing the aws_subnet.subnet-1 resource and accessing its id attribute.
* **route_table_id = aws_route_table.prod-route-table.id**: The route_table_id attribute identifies the Route Table to which this association will apply. In this case, it is specifying that this association will apply to the Route Table with the ID identified by referencing the aws_route_table.prod-route-table resource and accessing its id attribute.