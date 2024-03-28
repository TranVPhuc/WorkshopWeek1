---
title : "Terraform Provider"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 1.2 </b> "
---

#### Terraform Provider

**Terraform Provider** is a software acting as a bridge between Terraform and a specific platform, such as Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform, etc. It allows **Terraform** to interact with the APIs of the targeted platform to create, manage, and update resources.
**Main Functions**:
* **Resource Creation**: The Terraform provider offers functions and APIs to create new resources on the specific platform.
* **Resource Creation**: The Terraform provider offers functions and APIs to create new resources on the specific platform.
* **State Management**: Tracks the state of resources, aiding Terraform in determining necessary changes.. 


**Examples**:

* **AWS Provider**: Enables Terraform to interact with AWS services such as EC2, S3, RDS, etc.
* **Azure Provider**: Allows Terraform to interact with Azure services such as VMs, Storage, SQL Database, etc.
* **GCP Provider**: Permits Terraform to interact with GCP services such as Compute Engine, Cloud Storage, Cloud SQL, etc.

![TerraformProvider](/images/1-Introduce/terraformproviders.png?featherlight=false&width=30pc)
