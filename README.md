# Infrastructure as Code (IaC) - AWS Resource Provisioning  

## Overview  
This repository contains **Terraform scripts** to provision AWS infrastructure for the **Banking Application**. The infrastructure is defined using multiple Terraform configuration files, each handling a specific resource type. The **local backend** is used for state management, and no external modules are utilized.  

## Directory Structure  
The repository is structured as follows:  

```
├── network.tf          # Defines the VPC, subnets, and networking resources  
├── security_groups.tf  # Defines security groups for EC2, ALB, and RDS  
├── web_tier.tf         # Defines the Application Load Balancer (ALB)  
├── application_tier.tf # Provisions EC2 instances for hosting the Flask application  
├── rds.tf              # Configures the PostgreSQL RDS instance  
├── variables.tf        # Defines input variables for flexibility  
├── outputs.tf          # Specifies outputs such as ALB DNS and RDS endpoint  
├── providers.tf        # Configures the AWS provider and backend settings  
├── terraform.tfvars    # Defines values for Terraform variables (ignored in Git)  
└── README.md           # Documentation  
```

## Provisioned Resources  
The Terraform configuration files collectively provision the following AWS resources:  

- **VPC** with public and private subnets  
- **Security Groups** to manage access control for ALB, EC2, and RDS  
- **Application Load Balancer (ALB)** to distribute traffic across EC2 instances  
- **EC2 Instances** in a private subnet for hosting the Flask application  
- **PostgreSQL RDS Instance** for persistent data storage  
- **IAM Roles** for EC2 instances to interact with AWS services  

## Prerequisites  
Before running Terraform scripts, ensure you have:  

- **Terraform CLI (`>= 1.x`)** installed  
- **AWS CLI (`>= 2.x`)** installed and configured (`aws configure`)  

## Deployment Steps  

1. **Initialize Terraform**  
   ```sh
   terraform init
   ```  

2. **Validate Configuration**  
   ```sh
   terraform validate
   ```  

3. **Preview Changes**  
   ```sh
   terraform plan -var-file="terraform.tfvars" -out=myplan  

4. **Deploy Infrastructure**  
   ```sh
   terraform apply "myplan"
   ```  

5. **Destroy Infrastructure (if needed)**  
   ```sh
   terraform destroy
   ```  

## Notes  
- **State Management:** The Terraform state file is stored locally (`terraform.tfstate`), meaning it's not shared across multiple users.  
- **No External Modules:** All resources are defined in separate `.tf` files within the same directory.  

## Future Enhancements  
- Use **S3 + DynamoDB** as a remote backend for better state management.  
- Refactor Terraform code to use **modules** for better maintainability.  

---

