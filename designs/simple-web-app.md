# Simple Web Application Architecture (AWS)

## Use Case
A small startup or MVP application that needs to go live quickly with minimal cost and operational overhead.

## Requirements
- Low initial cost
- Simple deployment and maintenance
- Basic availability
- Ability to scale later if required

## Architecture Overview
- Single VPC
- Public subnet for application access
- EC2 instance hosting the web application
- Application Load Balancer (optional at early stage)
- RDS (single AZ) for database

## Key Design Decisions
- EC2 used instead of managed containers to keep setup simple
- Single AZ chosen to reduce cost
- Managed database used to reduce operational effort

## Trade-offs
- Limited fault tolerance due to single AZ
- Manual scaling required initially
- Lower availability compared to multi-AZ designs

## When to Use This Design
- Early-stage products
- Proof-of-concept workloads
- Non-critical applications
