---
title: "Worklog Tuần 3"
date: 2026-05-09
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Hiểu sâu về dịch vụ Compute và Storage trên AWS.
* Thực hành triển khai EC2, Backup, Storage Gateway và Amazon S3.
* Hiểu cơ chế backup, restore, static website hosting và replication.

---

### Các công việc cần triển khai:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|----------|-------------|-----------------|--------|
| 2 | Module 03-01: EC2 Fundamentals (Instance Type, AMI, EBS, Instance Store) | 04/05/2026 | 04/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Module 03-01-05 → 03-01-07: User Data, Metadata, Auto Scaling | 05/05/2026 | 05/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Module 03-02: EFS, FSx, Lightsail, MGN | 06/05/2026 | 06/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 13: AWS Backup | 07/05/2026 | 07/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Lab 24: AWS Storage Gateway | 08/05/2026 | 08/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 7 | Lab 57: Amazon S3 + CloudFront | 09/05/2026 | 09/05/2026 | https://cloudjourney.awsstudygroup.com/ |

---

# 🧪 Chi tiết Lab đã thực hành

---

## 🔹 Lab 13 – Deploy AWS Backup to the System

### Các bước thực hiện:

- Tạo S3 Bucket để lưu trữ backup
- Deploy infrastructure
- Tạo Backup Plan:
  - Backup frequency
  - Retention policy
- Cấu hình notifications
- Test restore dữ liệu

### Hiểu được:

- Cơ chế backup tập trung trên AWS
- Lifecycle & retention policy
- Khả năng restore khi gặp sự cố
- Tự động hóa backup cho tài nguyên AWS

---

## 🔹 Lab 24 – Using AWS Storage Gateway

### Các bước thực hiện:

- Tạo S3 Bucket
- Tạo EC2 để chạy Storage Gateway
- Tạo File Storage Gateway
- Tạo File Shares
- Mount File Share từ máy On-premises

### Hiểu được:

- Hybrid storage architecture
- Đồng bộ dữ liệu On-premises ↔ AWS
- File Gateway hoạt động như NAS nhưng backend lưu trên S3
- Luồng upload:
  - Client → Gateway → S3

---

## 🔹 Lab 57 – Starting with Amazon S3

### 1. Static Website Hosting

- Tạo S3 Bucket
- Upload website data
- Enable static website hosting
- Cấu hình public access
- Test website

### Hiểu được:

- Hosting website tĩnh bằng S3
- Bucket policy & object permissions

---

### 2. CloudFront Integration

- Block public access
- Tạo CloudFront distribution
- Test CDN access

### Hiểu được:

- CDN caching
- Tăng tốc truy cập website toàn cầu
- Ẩn trực tiếp S3 origin

---

### 3. Bucket Versioning & Replication

- Enable Versioning
- Move objects
- Replication multi-region

### Hiểu được:

- Data protection với Versioning
- Disaster Recovery với Cross-Region Replication
- Đồng bộ object giữa nhiều region

---

# ✅ Kết quả đạt được tuần 3:

- Hiểu sâu Amazon EC2:
  - Instance Types
  - AMI
  - EBS vs Instance Store
  - User Data & Metadata

- Hiểu Auto Scaling:
  - Scale in/out
  - High availability

- Nắm được Storage Services:
  - S3
  - EFS
  - FSx
  - Storage Gateway

- Thực hành Backup & Restore:
  - AWS Backup
  - Retention policy

- Triển khai Static Website:
  - S3 Website Hosting
  - CloudFront CDN

- Hiểu bảo vệ dữ liệu:
  - Versioning
  - Replication Multi-Region

---