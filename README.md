# AWS-Education-Simulation-Creating-a-Virtual-Private-Cloud
Hands-on AWS lab for creating and configuring a Virtual Private Cloud (VPC) with public/private subnets, EC2 instances, security groups, and routing.

# AWS Virtual Private Cloud (VPC) Lab Simulation

## Overview

This repository contains the step-by-step instructions and configuration details from an AWS VPC simulation lab. The lab demonstrates how to build a virtual private cloud (VPC) and deploy resources into it, moving from traditional complex networking to simplified cloud-based network deployment.

## Lab Objectives

After completing this simulation, you will be able to:
- Explain the basic components of a VPC
- Deploy a basic VPC with public subnets
- Deploy an Amazon EC2 instance into a VPC

## Architecture Diagram

```
┌─────────────────────────────────────────────────┐
│                 AWS Region                      │
│  ┌───────────────────────────────────────────┐  │
│  │              VPC                          │  │
│  │  ┌─────────────────────────────────────┐  │  │
│  │  │           Public Subnet             │  │  │
│  │  │  ┌─────────────────────────────┐    │  │  │
│  │  │  │        EC2 Instance         │    │  │  │
│  │  │  └─────────────────────────────┘    │  │  │
│  │  └─────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

## Lab Duration
Approximately 45 minutes

## Lab Tasks

### Task 1: Explore the Example VPC Configuration
- Navigate to AWS VPC service
- Examine default VPC and Example VPC
- Understand CIDR range configuration (172.31.0.0/16)

### Task 2: Explore a Subnet
- Examine public subnet configuration
- Understand IPv4 CIDR ranges and address allocation
- Learn about auto-assign public IPv4 addresses

**Key Concepts:**
- Public subnet: Resources accessible from the internet
- Private subnet: Resources isolated from the internet
- CIDR ranges must not overlap within the same VPC

### Task 3: Explore an Internet Gateway
- Understand internet gateway functionality
- Review gateway attachment to VPC
- Learn about NAT capabilities for public IPv4 addresses

**Internet Gateway Functions:**
- Provides routing target for internet-bound traffic
- Performs Network Address Translation (NAT)

### Task 4: Explore Route Tables
- Examine route table configuration
- Understand longest prefix matching
- Learn about public vs private subnet routing

**Route Table Rules:**
- Local route: `172.31.0.0/16` → Local (VPC internal traffic)
- Public route: `0.0.0.0/0` → Internet Gateway (external traffic)

### Task 5: Explore Security Groups
- Configure security group rules
- Update Web-Server-SG for HTTP access
- Understand inbound and outbound rule management

**Security Group Configuration:**
```
Inbound Rules:
- Type: HTTP
- Port: 80
- Source: 0.0.0.0/0 (Anywhere-IPv4)
- Description: Allow web access
```

### Task 6: Identify EC2 Instance VPC and Subnet
- Locate EC2 instance in Example VPC
- Verify instance deployment in Public Subnet 1
- Test security group configuration

### Task 7: Create a Custom VPC

**Customer Requirements:**
- **VPC IPv4 CIDR block:** `10.0.0.0/16`
- **Availability Zones:** 2
- **Public Subnets:**
  - Public Subnet 1: `10.0.0.0/24`
  - Public Subnet 2: `10.0.1.0/24`
- **Private Subnets:**
  - Private Subnet 1: `10.0.2.0/24`
  - Private Subnet 2: `10.0.3.0/24`

**VPC Creation Steps:**
1. Use VPC Creation Wizard
2. Select "VPC and more" for comprehensive setup
3. Configure name tag auto-generation: `Lab`
4. Set IPv4 CIDR block: `10.0.0.0/16`
5. Configure 2 Availability Zones
6. Create 2 public and 2 private subnets
7. Customize subnet CIDR blocks as specified

### Task 8: Launch EC2 Instance in Custom VPC

**Instance Configuration:**
- **Name:** Web-Server2
- **AMI:** Amazon Linux 2 AMI
- **Instance Type:** t2.micro
- **Key Pair:** Proceed without key pair
- **VPC:** Lab-vpc
- **Subnet:** public1 subnet
- **Auto-assign Public IP:** Enabled
- **Security Group:** WebServer2-SG

## Network Components Created

### VPC Components
- Virtual Private Cloud with custom CIDR range
- Internet Gateway for external connectivity
- Route tables for traffic routing
- Security groups for instance-level firewall rules

### Subnets
- **Public Subnets:** Direct internet access via Internet Gateway
- **Private Subnets:** Internal communication only, no direct internet access

### Security
- Custom security groups with HTTP access rules
- Inbound and outbound traffic control
- Instance-level firewall protection

## Key Learning Points

1. **VPC Isolation:** Each VPC is logically isolated from other virtual networks
2. **CIDR Planning:** Proper IP address range planning prevents conflicts
3. **Route Table Logic:** Longest prefix matching determines traffic routing
4. **Security Layers:** Security groups provide instance-level protection
5. **Public vs Private:** Route table configuration determines subnet accessibility

## Best Practices Demonstrated

- Never modify default security groups
- Create custom security groups for specific applications
- Plan CIDR ranges to avoid conflicts with on-premises networks
- Use separate public and private subnets for different resource types
- Enable auto-assign public IP for public subnet resources

## Prerequisites

- AWS Account with appropriate permissions
- Basic understanding of networking concepts
- Familiarity with AWS Console navigation

## Additional Resources

- [AWS VPC User Guide](https://docs.aws.amazon.com/vpc/)
- [Amazon EC2 User Guide](https://docs.aws.amazon.com/ec2/)
- [AWS Networking Best Practices](https://aws.amazon.com/architecture/well-architected/)

---

**Note:** This simulation demonstrates fundamental AWS VPC concepts and serves as a foundation for more complex networking scenarios in cloud environments.
