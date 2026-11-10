# Terraform AWS Resilient Infrastructure

This project provisions a small AWS environment with Terraform and reusable modules. It focuses on repeatable infrastructure, controlled scaling, IAM access, networking, and S3 storage.

## What it builds

The configuration creates:

- a VPC and subnets
- an EC2 Auto Scaling Group
- CPU based scaling behavior
- security groups for HTTP and HTTPS traffic
- an IAM role and policy for S3 access
- an S3 bucket with logging support

The root configuration is split into reusable Terraform modules so networking, compute, IAM, and storage can evolve independently.

## Why I built it

I wanted a practical example of how I would structure AWS infrastructure in Terraform instead of creating resources manually. The goal was to make the environment repeatable, easier to review before deployment, and simple to extend.

## Project structure

```text
.
├── main.tf
├── variables.tf
├── outputs.tf
├── modules/
│   ├── vpc/
│   ├── auto_scaling_group/
│   ├── iam/
│   └── s3_bucket/
└── scripts/
```

## Deployment flow

Initialize Terraform:

```bash
terraform init
```

Review the configuration:

```bash
terraform fmt -check
terraform validate
terraform plan
```

Apply the infrastructure only after reviewing the plan:

```bash
terraform apply
```

Remove the environment when it is no longer needed:

```bash
terraform destroy
```

## Configuration

The project uses variables for values such as AWS region, AMI ID, instance type, Auto Scaling Group capacity, bucket names, and environment specific settings.

AWS credentials should be supplied through the normal AWS credential chain, for example an AWS CLI profile or short lived environment credentials. Credentials are not stored in the repository.

## Terraform state

Terraform state is intentionally excluded from Git. In a production environment I would use a remote backend with locking and encryption instead of local state.

## Next improvements

I would extend this project with remote state, CI validation, security scanning, and automated policy checks before apply.
