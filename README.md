# Automated-Infrastructure-Provisioning-with-Terraform-Modules

![instance_running.png](https://github.com/pulkit-dheer/Automated-Infrastructure-Provisioning-with-Terraform-Modules/blob/main/images/instance_running.png)


This project demonstrates how to set up a basic AWS architecture using Terraform. It includes the creation of a VPC, subnets, security groups, EC2 instances, an Application Load Balancer (ALB), and more. The resources are all defined in a modular and reusable way.

## Project Structure

```
.
├── main.tf                  # Main configuration file
├── provider.tf              # AWS provider configuration
├── terraform.tfvars         # Variable definitions (sensitive values, etc.)
├── variables.tf             # Default variable values
├── terraform.tfstate        # Terraform state file (auto-generated)
├── terraform.tfstate.backup # Backup of the Terraform state file (auto-generated)
└── modules                  # Custom modules for reusable resources
    ├── alb                  # Module for Application Load Balancer (ALB)
    ├── ec2                  # Module for EC2 instances
    ├── sg                   # Module for Security Groups
    └── vpc                  # Module for VPC and related resources
```


## Description of Resources

- VPC: A Virtual Private Cloud (VPC) is created with subnets and an internet gateway for internet access.

- Security Groups: Configured to allow HTTP and SSH traffic to EC2 instances.

- EC2 Instances: Web servers deployed in the subnets, configured with a simple HTML page that displays instance details (like instance ID, type, and availability zone).

- ALB: An Application Load Balancer (ALB) with a listener that forwards HTTP requests to a target group, which is attached to the EC2 instances.

**Modules**:
- VPC Module: Defines the VPC, subnets, and route table resources.
- Security Group Module: Configures a security group that allows inbound HTTP and SSH traffic.
- EC2 Module: Deploys EC2 instances using a bash script to install and configure a basic web server.
- ALB Module: Configures the ALB, target group, and listener for routing traffic.


Prerequisites
1. **Terraform**: Ensure you have Terraform installed. You can download it from here.
2. **AWS Account**: You need an AWS account and access to create resources (VPC, EC2, Security Groups, etc.).
3. **AWS CLI**: Ensure the AWS CLI is configured with your credentials. Run aws configure to set up your credentials.

## Getting Started

**Clone the Repository**
```
git clone https://github.com/your-repo/terraform-vpc.git
cd terraform-vpc
```


**Configure AWS Credentials**

Make sure your AWS credentials are configured for Terraform to work. You can configure them using the AWS CLI:

```
aws configure
```


**Update the terraform.tfvars File**

Update the terraform.tfvars file with your specific values, such as VPC CIDR, subnet CIDRs, and EC2 instance names.


**Initialize Terraform**

Initialize the Terraform configuration. This will download the necessary provider plugins.

```
terraform init
```

**Plan and Apply the Configuration**

Run the following command to see the changes that will be made by Terraform.
```
terraform plan
```

If everything looks good, apply the configuration to create the resources.
```
terraform apply
```
![terraform apply](https://github.com/pulkit-dheer/Automated-Infrastructure-Provisioning-with-Terraform-Modules/blob/main/images/terraform_apply.png)

***Accessing the EC2 Instances***

Once the infrastructure is deployed, you can access the EC2 instances via the public IPs provided by Terraform. The instances will have a basic webpage running, which includes instance metadata like instance ID, type, and availability zone.

**Destroy the Infrastructure**
To clean up the resources after use, run the following command:

```
terraform destroy
```
This will tear down all the resources created by the Terraform configuration.

## Modules

**ALB Module**
This module creates an Application Load Balancer (ALB) and attaches it to the EC2 instances.

Resources:

`aws_lb`: Creates the load balancer.

`aws_lb_listener`: Defines the HTTP listener for the ALB.

`aws_lb_target_group`: Defines the target group for routing traffic.

`aws_lb_target_group_attachment`: Attaches EC2 instances to the target group.


**EC2 Module**
This module deploys EC2 instances in the specified subnets, installs a web server, and serves a simple HTML page with instance metadata.

Resources:
aws_instance: Launches EC2 instances.
user_data: Bash script that installs Apache, creates the HTML page, and starts the service.

**Security Group Module**
This module creates a security group that allows inbound HTTP and SSH traffic.

Resources:
aws_security_group: Defines the security group and its ingress/egress rules.

**VPC Module**
This module creates a Virtual Private Cloud (VPC), subnets, route tables, and an internet gateway.

Resources:
aws_vpc: Creates the VPC.
aws_subnet: Creates public subnets.
aws_internet_gateway: Attaches an internet gateway to the VPC.
aws_route_table & aws_route_table_association: Configure routing for the subnets.

## Contributing
If you'd like to contribute to this project, feel free to fork the repository, create a branch, and submit a pull request.

