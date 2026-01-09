## Architecture Diagram
```
                              ┌─────────────┐
                              │    Users    │
                              └──────┬──────┘
                                     │
                                     │ HTTPS
                                     ▼
                        ┌────────────────────────┐
                        │   Amazon CloudFront    │
                        │        (CDN)           │
                        └───────────┬────────────┘
                                    │
                                    │
                       ┌────────────▼────────────┐
                       │  Application Load       │
                       │      Balancer           │
                       │     (Multi-AZ)          │
                       └────────────┬────────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
    ┌─────────▼────────┐  ┌────────▼────────┐  ┌────────▼────────┐
    │  EC2 Instance    │  │  EC2 Instance   │  │  EC2 Instance   │
    │   AZ-1a          │  │   AZ-1b         │  │   AZ-1c         │
    │  (Auto Scaling)  │  │ (Auto Scaling)  │  │ (Auto Scaling)  │
    └──────────────────┘  └─────────────────┘  └─────────────────┘
              │                     │                     │
              └─────────────────────┼─────────────────────┘
                                    │
                       ┌────────────▼────────────┐
                       │   Amazon ElastiCache    │
                       │       (Redis)           │
                       │      Multi-AZ           │
                       └────────────┬────────────┘
                                    │
                       ┌────────────▼────────────┐
                       │     Amazon RDS          │
                       │      (MySQL)            │
                       │  ┌──────────────────┐   │
                       │  │  Primary (AZ-1a) │   │
                       │  └────────┬─────────┘   │
                       │           │ Sync        │
                       │  ┌────────▼─────────┐   │
                       │  │ Standby (AZ-1b)  │   │
                       │  └──────────────────┘   │
                       └─────────────────────────┘
                                    │
                       ┌────────────▼────────────┐
                       │      Amazon S3          │
                       │   (Static Assets)       │
                       │   + Versioning          │
                       └─────────────────────────┘
```

**Key Components:**
- **CloudFront:** CDN with edge locations
- **ALB:** Multi-AZ load balancer
- **Auto Scaling Group:** 3-10 EC2 instances across multiple AZs
- **ElastiCache:** Redis for session management & caching
- **RDS Multi-AZ:** Automatic failover to standby
- **S3:** Versioned storage for static assets

**Cost:** ~$500-1000/month  
**Availability:** 99.9%+  
**Best For:** Production apps, e-commerce, SaaS
