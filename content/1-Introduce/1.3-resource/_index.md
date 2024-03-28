---
title : "Terraform Resource"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 1.3 </b> "
---

#### Terraform Resource


In **Terraform**, a **resource** is a fundamental building block that makes up the infrastructure you manage with Terraform. It can consist of various types of resources, depending on the cloud provider you are using. They may include the following types of resources:

* **Virtual Machines**: EC2 instances on AWS, Azure VMs, Google Compute Engine.
* **Networking**: Includes VPC, subnet, load balancer, firewall.
* **Storage**: S3 buckets on AWS, Azure Blob Storage, Google Cloud Storage.
* **Other Services**: CloudWatch on AWS, Azure Monitor, Google Cloud Monitoring.

 **Characteristics of Terraform Resources:**:
* **Defined by Code**: Utilizes the HashiCorp Configuration Language (HCL) to describe the desired configuration of resources.
* **Lifecycle Management**: Terraform can create, update, and delete resources automatically.
* **Flexibility**: Supports multiple cloud providers and can be used to manage on-premises infrastructure.
* **Ease of Use**: Provides simple and understandable syntax, making it easy to get started with.

**Syntax Usage**:
```
provider "aws" {
  region = "us-east-1"
}
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  
  instance_type = "t2.micro"              
}

```
In this example::
* **provider "aws"**: specifies that we will use AWS as the service provider.
* **resource** "aws_instance" "example": defines an EC2 resource named "example".
* **ami**: Selects an Amazon Machine Image (AMI) to create the instance.
* **instance_type**: Selects the instance type, which here is t2.micro.

{{%notice tip%}}
There are several cloud service providers supported by Terraform. Make sure to choose the right provider for your needs.
{{%/notice%}}
