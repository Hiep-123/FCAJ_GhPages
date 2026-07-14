---
title: "Worklog Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Hiểu các khái niệm cơ bản về cơ sở dữ liệu trên AWS.
* Thực hành triển khai Amazon RDS và Amazon Aurora.
* Tìm hiểu quy trình migration và chuyển đổi cơ sở dữ liệu trên AWS.

---

### Các công việc cần triển khai:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|--------------------------|--------------|-----------------|--------------------|
| 2 | Module 06-01: Database Concepts Review | 25/05/2026 | 25/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Module 06-02: Amazon RDS & Amazon Aurora | 26/05/2026 | 26/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Module 06-03: Amazon Redshift & ElastiCache | 27/05/2026 | 27/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 05: Amazon RDS | 28/05/2026 | 28/05/2026 |  https://cloudjourney.awsstudygroup.com/ |
| 6 | Lab 43: Database Schema Conversion & Migration (Phần 1) | 29/05/2026 | 29/05/2026 |  https://cloudjourney.awsstudygroup.com/ |
| 7 | Lab 43: Database Schema Conversion & Migration (Phần 2) | 30/05/2026 | 30/05/2026 |  https://cloudjourney.awsstudygroup.com/ |

---

# Chi tiết Lab đã thực hành

---

## Lab 05 – Amazon Relational Database Service (Amazon RDS)

### Các bước thực hiện:

- Tạo VPC và Security Groups
- Tạo DB Subnet Group
- Deploy EC2 Instance
- Tạo Amazon RDS Database
- Kết nối ứng dụng với RDS
- Thực hiện Backup và Restore

### Hiểu được:

- Kiến trúc Amazon RDS
- Kết nối ứng dụng tới cơ sở dữ liệu
- Cơ chế Backup và Restore dữ liệu
- Database networking và security

---

## Lab 43 – Chuyển đổi lược đồ và di dời cơ sở dữ liệu

### Các bước thực hiện:

- Kết nối và cấu hình MSSQL, Oracle Source Database
- Sử dụng AWS Schema Conversion Tool (SCT)
- Chuyển đổi Schema:
  - MSSQL → Aurora MySQL
  - Oracle → MySQL
- Tạo Migration Project
- Tạo Migration Task và Endpoint
- Kiểm tra dữ liệu trên S3
- Tạo Serverless Migration
- Thiết lập Event Notifications
- Theo dõi Logs và Troubleshooting

### Hiểu được:

- Quy trình Database Migration trên AWS
- Schema Conversion giữa các hệ quản trị CSDL
- AWS Database Migration Service (DMS)
- Giám sát và xử lý lỗi trong quá trình migration

---

# Kết quả đạt được tuần 6:

- Hiểu các khái niệm cơ bản về cơ sở dữ liệu trên AWS
- Thực hành Amazon RDS và Amazon Aurora
- Tìm hiểu Amazon Redshift và ElastiCache
- Thực hiện Backup & Restore cơ sở dữ liệu
- Thực hành Schema Conversion và Database Migration với AWS SCT và DMS
- Theo dõi, kiểm tra và xử lý lỗi trong quá trình di chuyển dữ liệu