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
                    │    Application Load     │
                    │       Balancer          │
                    └────────────┬────────────┘
                                 │
                                 │
                    ┌────────────▼────────────┐
                    │      EC2 Instance       │
                    │   (Web + App Server)    │
                    │    t3.medium            │
                    └────────────┬────────────┘
                                 │
                    ┌────────────┴────────────┐
                    │                         │
          ┌─────────▼──────────┐   ┌─────────▼──────────┐
          │   Amazon RDS       │   │    Amazon S3       │
          │   (MySQL)          │   │  (Static Assets)   │
          │   Single-AZ        │   │                    │
          └────────────────────┘   └────────────────────┘
```

**Key Components:**
- **CloudFront:** Global CDN for fast content delivery
- **ALB:** Application Load Balancer for traffic distribution
- **EC2:** Single instance running web application
- **RDS:** MySQL database (single availability zone)
- **S3:** Storage for static files (images, CSS, JS)

**Cost:** ~$50-100/month  
**Availability:** 95-98%  
**Best For:** Small websites, MVPs, learning projects
