---
title: "Week 3 Worklog"
date: 2026-05-04
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Gain deeper understanding of AWS Compute and Storage services.
* Practice EC2 deployment, Backup, Storage Gateway, and Amazon S3.
* Learn backup/restore, static website hosting, and replication mechanisms.

---

### Weekly Tasks:

| Day | Tasks | Start | End |
|-----|------|------|-----|
| Mon | EC2 Fundamentals (Instance Types, AMI, EBS, Instance Store) | 04/05/2026 | 04/05/2026 |
| Tue | User Data, Metadata, Auto Scaling | 05/05/2026 | 05/05/2026 |
| Wed | EFS, FSx, Lightsail, MGN | 06/05/2026 | 06/05/2026 |
| Thu | Lab 13 – AWS Backup | 07/05/2026 | 07/05/2026 |
| Fri | Lab 24 – Storage Gateway | 08/05/2026 | 08/05/2026 |
| Sat | Lab 57 – Amazon S3 & CloudFront | 09/05/2026 | 09/05/2026 |

---

# 🧪 Lab Details

---

## 🔹 Lab 13 – Deploy AWS Backup to the System

### Tasks:

- Create S3 Bucket
- Deploy infrastructure
- Create Backup Plan
- Configure notifications
- Test restore process

### Learned:

- Centralized AWS backup management
- Backup lifecycle & retention policy
- Disaster recovery & restore capability
- Automated backup strategy

---

## 🔹 Lab 24 – Using AWS Storage Gateway

### Tasks:

- Create S3 Bucket
- Deploy EC2 for Storage Gateway
- Create File Gateway
- Create File Shares
- Mount shares from on-premises machine

### Learned:

- Hybrid storage architecture
- On-premises ↔ AWS synchronization
- File Gateway as NAS with S3 backend storage
- Data upload flow:
  - Client → Gateway → S3

---

## 🔹 Lab 57 – Starting with Amazon S3

### 1. Static Website Hosting

- Create S3 Bucket
- Upload website files
- Enable static website hosting
- Configure public access
- Test website

### Learned:

- Static website hosting on S3
- Bucket policy & object permissions

---

### 2. CloudFront Integration

- Block direct public access
- Configure CloudFront distribution
- Test CDN delivery

### Learned:

- CDN caching
- Global content acceleration
- Protecting S3 origin access

---

### 3. Bucket Versioning & Replication

- Enable Versioning
- Move objects
- Configure Cross-Region Replication

### Learned:

- Data protection with Versioning
- Disaster Recovery using replication
- Multi-region synchronization

---

# ✅ Achievements:

- Deep understanding of Amazon EC2:
  - Instance Types
  - AMI
  - EBS vs Instance Store
  - User Data & Metadata

- Auto Scaling concepts:
  - Scale in/out
  - High availability

- AWS Storage services:
  - S3
  - EFS
  - FSx
  - Storage Gateway

- Backup & Restore:
  - AWS Backup
  - Retention policies

- Static Website Deployment:
  - S3 Website Hosting
  - CloudFront CDN

- Data protection:
  - Versioning
  - Cross-Region Replication

---