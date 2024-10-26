# Basic VPC and EC2 CloudFormation Template

This template deploys a basic AWS infrastructure consisting of:

* A Virtual Private Cloud (VPC) with a CIDR block of 10.0.0.0/16
* An Internet Gateway attached to the VPC
* A public subnet with a CIDR block of 10.0.0.0/24
* A route table associated with the subnet, routing all traffic (0.0.0.0/0) to the internet gateway
* A security group allowing HTTP (port 80) and SSH (port 22) access
* An EC2 instance launched into the public subnet

The EC2 instance will have a user data script that installs and starts an Apache web server (httpd) if the instance is Amazon Linux 2023. If the instance is Ubuntu, the script will install and start apache2.

## Parameters

The template has the following parameters:

* **ProjectEnvironment:**  Allows you to select the environment type (Dev, QA, or Prod). This affects the instance type and name tag.
* **ProjectKeyPair:**  An existing EC2 Key Pair to be used for SSH access to the instance.
* **ProjectAMI:** The ID of the Amazon Machine Image (AMI) to use for the EC2 instance. You can choose an Amazon Linux 2023 or Ubuntu AMI.
* **ProjectAVZone:** The Availability Zone where the resources will be created.

## How to Deploy

1.  **Save the template:** Save the template as a YAML file (e.g., `test-project.yaml`).
2.  **Create the stack:** Use the AWS Management Console, AWS CLI, or SDKs to create a CloudFormation stack using the template.
3.  **Provide parameter values:** When creating the stack, you'll be prompted to provide values for the parameters.

## Outputs

The template provides the following outputs:

* **EnvironmentName:** The name associated with the selected environment.
* **Region:** The AWS region where the stack is deployed.

## Notes

* Make sure that you create a key pair and download your private key before creating the stack!
* The default AMI in this template is associated with the region us-west-2. If you want to deploy this template in another region you have make sure that you have the appropriate AMI.
* Make sure you have the necessary IAM permissions to create and manage AWS resources.

## Cleanup

To delete the resources created by this template, simply delete the CloudFormation stack.