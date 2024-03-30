---
title : "Adding an AWS profile using AWS CLI"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 2.3.</b> "
---

### Adding an AWS profile for Terraform
To install **AWS CLI**
* Ensure you have Python installed on your system. The AWS CLI requires Python 2 version 2.6.5+ or Python 3 version 3.3+.
* Access the **AWS CLI** download page [here](https://aws.amazon.com/vi/cli/) and download the appropriate version of the AWS CLI for your operating system. Here, we'll use Windows. After installing the **AWS CLI**, you can check if it has been installed successfully by opening a command prompt and running the following command: `aws --version `
![awscli](/images/2.3-aws-cli/00001.png?featherlight=false&width=70pc)
![awscli](/images/2.3-aws-cli/00002.png?featherlight=false&width=60pc)
To add an **AWS profile** for Terraform using the **AWS CLI**:
>* Open a command prompt or terminal window.
>* Run the following command to configure a new AWS profile `aws configure --profile <profile-name> `and follow the instruction. Replace `<profile-name>` with the name you want to give to your AWS profile for Terraform.
>* You will be prompted to enter your **AWS access key ID**, **secret access key**, **default region**, and **output** format. Enter the required information accordingly then hit **Enter**.
>* Once you've entered the details, the AWS CLI will create a new profile in the ~/.aws/credentials file (on Linux/macOS) or %USERPROFILE%\.aws\credentials file (on Windows) with the specified profile name.