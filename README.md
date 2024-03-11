# AWS Multi-Region Deployment with Terraform

## Project Description

This project deploys a solution consisting of an EC2 instance, an S3 bucket, and a DynamoDB table in two different AWS regions, `us-east-1` and `us-west-2`. The solution is designed to have the same configurations across both regions, leveraging Terraform modules to avoid duplications.

## Components

### EC2 Instance
- The EC2 instance is deployed using the `ec2` module.
- It is connected to a public subnet in both regions.

### S3 Bucket
- The S3 bucket is deployed using the `s3` module.
- It serves as an object storage solution.

### DynamoDB Table
- The DynamoDB table is deployed using the `dynamodb` module.
- It is connected to a private subnet in both regions.

## Module Configuration

### Network Module
- Manages the VPC, subnets, and security groups.
- Inputs:
  - `cidr_vpc`: The CIDR block for the VPC.
  - `cidr_public_subnet`: The CIDR block for the public subnet.
  - `cidr_private_subnet`: The CIDR block for the private subnet.

### EC2 Module
- Deploys the EC2 instance.
- Inputs:
  - `ami`: The AMI ID for the EC2 instance.
  - `instance_type`: The instance type for the EC2 instance.
  - `subnet_id`: The ID of the public subnet.
  - `security_group_id`: The ID of the security group attached to the EC2 instance.

### S3 Module
- Creates the S3 bucket.
- Inputs:
  - `bucket_s3`: The name of the S3 bucket.

### DynamoDB Module
- Sets up the DynamoDB table.
- Inputs:
  - `dyn_db`: The name of the DynamoDB table.

## Terraform Backend Configuration

- The Terraform state is stored in an S3 bucket named `amterra`.
- The state files are named `state`.
- The region for the state bucket is set to `us-west-2`.

