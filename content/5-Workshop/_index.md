---
title: "Workshop"
date: 2026-07-04
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# AWS Serverless E-commerce Platform — Deployment Workshop

This workshop walks you through deploying the complete AWS Serverless E-commerce Platform from scratch on AWS. By the end, you will have a fully functional, publicly accessible e-commerce application running in **ap-southeast-1 (Singapore)**.

**Estimated time:** 90–120 minutes  
**Deployment region:** ap-southeast-1 (Singapore)  
**WAF region:** us-east-1 (required for CloudFront)

---

## Architecture Overview

> **Note:** This is a simplified deployment overview. Refer to Proposal Section 5 for the complete production architecture including WAF rule details, X-Ray tracing, log retention, and security headers configuration.

This is a simplified deployment overview. Refer to Proposal Section 5 for the complete production architecture.

```
Browser
  └── CloudFront (HTTPS, HTTP/2+3, WAF, OAC)
        └── S3 FrontendBucket (private, React SPA)

API Gateway REST (100 rps / 200 burst)
  ├── Cognito Authorizer (JWT)
  ├── GET /products       → ProductServiceFunction  (public)
  ├── GET/POST/PUT/DELETE /cart → CartServiceFunction (auth)
  └── POST /orders, GET /orders, GET /orders/{id} → OrderServiceFunction (auth)
                                    │ PutEvents
                                    ▼
                    EcommerceEventBus (EventBridge)
                          └── OrderCreated rule
                                └── OrderQueue (SQS, maxReceive=3)
                                      ├── OrderProcessorFunction
                                      └── OrderDLQ (dead-letter)

EcommerceTable (DynamoDB, PAY_PER_REQUEST, PITR, 3 GSIs)
CloudWatch Dashboard + 6 Alarms → SNS → Email
WAF WebACL: IP Reputation + OWASP CRS + Rate Limit
```

---

## Workshop Contents

1. [Environment Setup](5.1-environment-setup/)
2. [Deploy Backend Stacks](5.2-deploy-backend/)
3. [Deploy Frontend Stack](5.3-deploy-frontend/)
4. [Seed Data & Create Users](5.4-seed-and-users/)
5. [Verify & Test Everything](5.5-verify-and-test/)
6. [Cleanup](5.6-cleanup/)
