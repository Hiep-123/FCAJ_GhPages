---
title: "Week 4 Worklog"
date: 2026-05-16
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Gain deeper understanding of AWS Storage services.
* Practice Backup, Storage Gateway, FSx, and Amazon S3.
* Learn migration, replication, and storage optimization mechanisms.

---

### Weekly Tasks:
---

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|----------------------------|-------------|-----------|------------|
| Mon | Module 04-01: AWS Storage Services | 11/05/2026 | 11/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Tue | Module 04-02: Amazon S3 - Access Point - Storage Classes | 12/05/2026 | 12/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Wed | Module 04-03 & 04-04: S3 Static Website, Glacier, Snow Family, Storage Gateway, Backup | 13/05/2026 | 13/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| Thu | Lab 13: Deploy AWS Backup to the System <br> Lab 14: VM Import/Export | 14/05/2026 | 14/05/2026 | https://000013.awsstudygroup.com/ |
| Fri | Lab 24: Using File Storage Gateway <br> Lab 25: Amazon FSx for Windows File Server | 15/05/2026 | 15/05/2026 | https://000024.awsstudygroup.com/ |
| Sat | Lab 57: Starting with Amazon S3 & CloudFront | 16/05/2026 | 16/05/2026 | https://000057.awsstudygroup.com/ |

---

---

# Lab Details

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
- Retention policies & lifecycle
- Disaster recovery workflow
- Automated backup strategy

---

## 🔹 Lab 14 – VM Import/Export

### Import VM to AWS

- Export VM from VMware
- Upload VM to S3
- Import VM as AMI
- Launch EC2 from imported AMI

### Export VM from AWS

- Export Instance / AMI
- Configure S3 ACL
- Download VM to On-premises

### Learned:

- Workload migration from On-premises to AWS
- Convert VM into AMI
- Hybrid migration workflow

---

## 🔹 Lab 24 – Using File Storage Gateway

### Tasks:

- Create S3 Bucket
- Deploy EC2 for Storage Gateway
- Create File Gateway
- Create File Shares
- Mount shares from On-premises machine

### Learned:

- Hybrid storage architecture
- On-premises ↔ AWS synchronization
- File Gateway using S3 backend storage

---

## 🔹 Lab 25 – Amazon FSx for Windows File Server

### Tasks:

- Create:
  - SSD Multi-AZ file system
  - HDD Multi-AZ file system
- Create file shares
- Test & monitor performance
- Enable:
  - Data Deduplication
  - Shadow Copies
  - Storage Quotas
  - Continuous Availability

### Scaling:

- Scale throughput capacity
- Scale storage capacity

### Learned:

- Managed Windows File Server on AWS
- Multi-AZ High Availability
- Enterprise file sharing
- Storage optimization & monitoring

---

## 🔹 Lab 57 – Starting with Amazon S3

### Static Website Hosting

- Create S3 Bucket
- Upload website data
- Enable static website hosting
- Configure public access
- Test website

### CloudFront Integration

- Block public access
- Configure CloudFront distribution
- Test CDN delivery

### Versioning & Replication

- Enable Versioning
- Move objects
- Configure Cross-Region Replication

### Learned:

- Static website hosting on S3
- CDN acceleration using CloudFront
- Data protection with Versioning
- Disaster Recovery with replication

---

#  Achievements:

- Deep understanding of AWS Storage services:
  - Amazon S3
  - FSx
  - Storage Gateway
  - AWS Backup

- Storage concepts:
  - Storage Classes
  - Lifecycle management
  - Glacier storage

- Deployments:
  - Static Website Hosting
  - CloudFront CDN

- Migration workflow:
  - VM Import/Export
  - On-premises ↔ AWS

- Data management:
  - Versioning
  - Replication
  - Backup & Restore

- Storage optimization:
  - Data Deduplication
  - Storage Quotas
  - Performance scaling

---