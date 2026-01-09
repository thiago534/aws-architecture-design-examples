# Highly Available Web Application Architecture (AWS)

## Use Case
A production web application that must remain available during failures and handle variable traffic.

## Requirements
- High availability
- Fault tolerance
- Automatic scaling
- Minimal downtime during failures

## Architecture Overview
- Single VPC spanning multiple Availability Zones
- Public subnets for load balancer
- Private subnets for application servers
- Application Load Balancer across multiple AZs
- Auto Scaling Group for EC2 instances
- RDS Multi-AZ for database

## Key Design Decisions
- Multi-AZ deployment to eliminate single points of failure
- Load balancer used to distribute traffic and perform health checks
- Auto Scaling to adjust capacity based on demand
- Private subnets used to limit direct internet exposure

## Failure Handling
- If an EC2 instance fails, traffic is routed to healthy instances
- If an AZ fails, remaining AZs continue serving traffic
- Database failover handled automatically by RDS Multi-AZ

## Trade-offs
- Higher cost compared to single-AZ designs
- Increased operational complexity
- Requires monitoring and tuning

## When to Use This Design
- Customer-facing production applications
- Business-critical workloads
- Applications with uptime requirements
