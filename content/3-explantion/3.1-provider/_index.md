---
title : "Configure connection to AWS account"
date :  "`r Sys.Date()`" 
weight : 1
chapter : false
pre : " <b> 3.1.</b> "
---

### Configure connection to AWS account

```
provider "aws" {
  region     = "us-east-1"
  shared_config_files      = ["~/.aws/config"]
  shared_credentials_files = ["~/.aws/credentials"]
  profile                  = "terraform"
}
```

The code above is a configuration snippet of Terraform to utilize the **AWS (Amazon Web Services)**.

* **provider "aws"**: This is a declaration of a provider for Terraform, specifically for AWS.
* **region = "us-east-1"**: This is the configuration for the region where the resources will be created. In this case, the chosen region is "us-east-1".
* **shared_config_files = ["~/.aws/config"]**: This is the path to the shared configuration files of AWS. In this case, the configuration file used is "~/.aws/config".
* **shared_credentials_files = ["~/.aws/credentials"]**: 
This is the path to the shared credentials file of AWS. In this case, the credentials file used is "~/.aws/credentials".
* **profile = "terraform":** This is the name of the profile in both the configuration file and the credentials file. In this case, the profile name used is "terraform".
