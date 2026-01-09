# Secure VPC Architecture Design (AWS)

## Use Case
An organization hosting internal or sensitive workloads that require strong network isolation and controlled access.

## Requirements
- Secure network segmentation
- Restricted internet access
- Controlled inbound and outbound traffic
- Clear separation of public and private resources

## Architecture Overview
- Single VPC with multiple Availability Zones
- Public subnets for internet-facing resources (ALB, Bastion)
- Private subnets for application and database layers
- Internet Gateway attached to VPC
- NAT Gateway for outbound internet access from private subnets
- Security Groups and NACLs for traffic control

## Key Design Decisions
- Private subnets used for application and database workloads
- NAT Gateway allows outbound access without exposing private resources
- Security Groups used as primary access control mechanism
- NACLs used for an additional layer of network security

## Access Control Approach
- Internet-facing access only through Load Balancer
- No direct internet access to application or database instances
- SSH or admin access restricted via Bastion host or VPN
- Least-privilege access enforced at network level

## Trade-offs
- Increased cost due to NAT Gateway
- Slightly higher operational complexity
- Strongly reduced attack surface and blast radius

## When to Use This Design
- Enterprise or regulated workloads
- Applications handling sensitive data
- Environments requiring strict security controls
