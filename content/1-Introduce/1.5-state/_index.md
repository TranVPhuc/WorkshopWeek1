---
title : "Terraform State"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 1.4 </b> "
---
#### Terraform State
Terraform State is a data set that stores information about the infrastructure resources managed by Terraform. It includes:
* Name and type of each resource.
* Attributes of each resource.
* Relationships between resources.

**Purposes**:
* Track changes to the infrastructure.
* Identify resources that need to be created, updated, or deleted.
* Keep your infrastructure consistent with Terraform configuration.

**Types of Terraform State:**:
* **Local State**: Stored in a .tfstate file in your Terraform project directory.
* **Remote State**: Stored in remote storage repositories, such as HashiCorp Vault.

**An example of information for an AWS virtual machine after it has been created **:
```
{
  "resources": {
    "aws_instance.web_server": {
      "type": "aws_instance",
      "name": "web_server",
      "count": 1,
      "primary": {
        "id": "i-1234567890abcdef0",
        "attributes": {
          "ami_id": "ami-1234567890abcdef0",
          "instance_type": "t2.micro",
          "public_ip": "123.45.67.89"
        }
      }
    }
  }
}
```

{{%notice tip%}}

There are several Terraform tools that can help you manage Terraform state, such as Terraform State Viewer and Terraform State Diff
{{%/notice%}}