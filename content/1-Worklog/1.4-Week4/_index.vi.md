---
title: "Worklog Tuần 4"
date: 2026-05-16
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Hiểu sâu các dịch vụ lưu trữ trên AWS.
* Thực hành triển khai Backup, Storage Gateway, FSx và Amazon S3.
* Nắm được cơ chế migration, replication và storage optimization.

---

### Các công việc cần triển khai:
---

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|--------------------------|--------------|-----------------|--------------------|
| 2 | Module 04-01: Dịch vụ lưu trữ trên AWS | 11/05/2026 | 11/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Module 04-02: Amazon S3 - Access Point - Storage Class | 12/05/2026 | 12/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Module 04-03 & 04-04: S3 Static Website, Glacier, Snow Family, Storage Gateway, Backup | 13/05/2026 | 13/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 13: Deploy AWS Backup to the System <br> Lab 14: VM Import/Export | 14/05/2026 | 14/05/2026 | https://000013.awsstudygroup.com/ |
| 6 | Lab 24: Using File Storage Gateway <br> Lab 25: Amazon FSx for Windows File Server | 15/05/2026 | 15/05/2026 | https://000024.awsstudygroup.com/ |
| 7 | Lab 57: Starting with Amazon S3 & CloudFront | 16/05/2026 | 16/05/2026 | https://000057.awsstudygroup.com/ |

---

#  Chi tiết Lab đã thực hành

---

## Lab 13 – Deploy AWS Backup to the System

### Các bước thực hiện:

- Tạo S3 Bucket
- Deploy infrastructure
- Tạo Backup Plan
- Thiết lập notifications
- Test restore dữ liệu

### Hiểu được:

- Cơ chế centralized backup trên AWS
- Retention policy & lifecycle
- Disaster recovery workflow
- Tự động hóa backup tài nguyên AWS

---

## Lab 14 – VM Import/Export

### Import VM từ On-premises lên AWS

- Export VM từ VMware Workstation
- Upload VM lên S3
- Import VM thành AMI
- Deploy EC2 từ imported AMI

### Export VM từ AWS

- Export instance / AMI
- Thiết lập ACL cho S3 Bucket
- Download VM về On-premises

### Hiểu được:

- Migration workload từ On-premises → AWS
- Chuyển đổi virtual machine thành AMI
- Hybrid migration workflow

---

## Lab 24 – Using File Storage Gateway

### Các bước thực hiện:

- Tạo S3 Bucket
- Tạo EC2 cho Storage Gateway
- Tạo File Gateway
- Tạo File Shares
- Mount file shares từ máy On-premises

### Hiểu được:

- Hybrid storage architecture
- Đồng bộ dữ liệu On-premises ↔ AWS
- File Gateway hoạt động như NAS sử dụng S3 backend

---

## Lab 25 – Amazon FSx for Windows File Server

### Các bước thực hiện:

- Tạo:
  - SSD Multi-AZ file system
  - HDD Multi-AZ file system
- Tạo file shares
- Test & monitor performance
- Enable:
  - Data Deduplication
  - Shadow Copies
  - Storage Quotas
  - Continuous Availability

### Scale hệ thống:

- Scale throughput capacity
- Scale storage capacity

### Hiểu được:

- Managed Windows File Server trên AWS
- High Availability với Multi-AZ
- File sharing cho enterprise workloads
- Storage optimization & monitoring

---

## Lab 57 – Starting with Amazon S3

### Static Website Hosting

- Tạo S3 Bucket
- Upload dữ liệu website
- Enable static website hosting
- Cấu hình public access
- Test website

### CloudFront Integration

- Block public access
- Tạo CloudFront distribution
- Test CDN delivery

### Versioning & Replication

- Enable Bucket Versioning
- Move objects
- Configure Cross-Region Replication

### Hiểu được:

- Static website hosting trên S3
- CDN acceleration với CloudFront
- Data protection bằng Versioning
- Disaster Recovery với Replication Multi-Region

---

#  Kết quả đạt được tuần 4:

- Hiểu sâu các dịch vụ Storage trên AWS:
  - Amazon S3
  - FSx
  - Storage Gateway
  - AWS Backup

- Nắm được cơ chế:
  - Storage Classes
  - Lifecycle management
  - Glacier storage

- Triển khai:
  - Static Website Hosting
  - CloudFront CDN

- Hiểu migration workflow:
  - VM Import/Export
  - On-premises ↔ AWS

- Quản lý dữ liệu:
  - Versioning
  - Replication
  - Backup & Restore

- Storage optimization:
  - Data Deduplication
  - Storage Quotas
  - Performance scaling

---