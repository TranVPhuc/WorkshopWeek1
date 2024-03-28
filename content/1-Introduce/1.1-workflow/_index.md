---
title : "Workflow"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1.1 </b> "
---

#### Terraform Workflow

![Workflow](/images/1-Introduce/workflow.png?featherlight=false&width=51pc)

The typical workflow of **Terraform** often includes the following steps::

1. **Design**:
* Identify the necessary resources and their relationships.
* Build directory structure and modules if required..
2. **Initialization**:
* Download and install necessary plugins for the project..
* **Terraform** will create a directory containing the required plugins.
3. **Plan**:
* **Terraform** will compare the current state with the desired state defined in the infrastructure code and display the expected changes.
4. **Deployment**:
* **Terraform** will deploy the planned changes. At this point, **Terraform** will create, update, or delete resources as well as update the state.
5. **State Management**:
*  **Terraform** uses a state file to track the actual state of the infrastructure compared to the configuration code.
* During the deployment process, this state is updated and securely stored.
6. **Verification**:
* After deployment, verify that the deployed resources are functioning as expected.
7. **Monitoring and Maintenance**:
* Utilize appropriate monitoring and maintenance tools such as CloudWatch.
8. **Adjust**:
* When configuration changes are needed, iterate through the process starting from the design phase or by modifying Terraform configuration files.
9. **Clean up**:
* When resources are no longer needed, Terraform will delete the managed resources and update the state.

