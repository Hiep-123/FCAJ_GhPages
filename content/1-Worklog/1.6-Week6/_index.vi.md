---
title: "Worklog Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---
{{% notice warning %}}
**Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

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
| 5 | Lab 05: Amazon RDS | 28/05/2026 | 28/05/2026 | AWS Study Group Labs |
| 6 | Lab 43: Database Schema Conversion & Migration (Phần 1) | 29/05/2026 | 29/05/2026 | AWS Study Group Labs |
| 7 | Lab 43: Database Schema Conversion & Migration (Phần 2) | 30/05/2026 | 30/05/2026 | AWS Study Group Labs |

---

# Chi tiết Lab đã thực hành

---

## 🔹 Lab 05 – Amazon Relational Database Service (Amazon RDS)

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

## 🔹 Lab 43 – Chuyển đổi lược đồ và di dời cơ sở dữ liệu

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

---ành viên trong First Cloud Journey.
* Hiểu dịch vụ AWS cơ bản, cách dùng console & CLI.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Làm quen với các thành viên FCJ <br> - Đọc và lưu ý các nội quy, quy định tại đơn vị thực tập                                                                                             | 11/08/2025   | 11/08/2025      |
| 3   | - Tìm hiểu AWS và các loại dịch vụ <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... <br>                                            | 12/08/2025   | 12/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Tạo AWS Free Tier account <br> - Tìm hiểu AWS Console & AWS CLI <br> - **Thực hành:** <br>&emsp; + Tạo AWS account <br>&emsp; + Cài AWS CLI & cấu hình <br> &emsp; + Cách sử dụng AWS CLI | 13/08/2025   | 13/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Tìm hiểu EC2 cơ bản: <br>&emsp; + Instance types <br>&emsp; + AMI <br>&emsp; + EBS <br>&emsp; + ... <br> - Các cách remote SSH vào EC2 <br> - Tìm hiểu Elastic IP   <br>                  | 14/08/2025   | 15/08/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** <br>&emsp; + Tạo EC2 instance <br>&emsp; + Kết nối SSH <br>&emsp; + Gắn EBS volume                                                                                         | 15/08/2025   | 15/08/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 6:
* Hiểu AWS là gì và nắm được các nhóm dịch vụ cơ bản: 
  * Compute
  * Storage
  * Networking 
  * Database
  * ...

* Đã tạo và cấu hình AWS Free Tier account thành công.

* Làm quen với AWS Management Console và biết cách tìm, truy cập, sử dụng dịch vụ từ giao diện web.

* Cài đặt và cấu hình AWS CLI trên máy tính bao gồm:
  * Access Key
  * Secret Key
  * Region mặc định
  * ...

* Sử dụng AWS CLI để thực hiện các thao tác cơ bản như:

  * Kiểm tra thông tin tài khoản & cấu hình
  * Lấy danh sách region
  * Xem dịch vụ EC2
  * Tạo và quản lý key pair
  * Kiểm tra thông tin dịch vụ đang chạy
  * ...

* Có khả năng kết nối giữa giao diện web và CLI để quản lý tài nguyên AWS song song.
* ...


