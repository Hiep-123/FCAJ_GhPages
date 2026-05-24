---
title: "Worklog Tuần 5"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Hiểu các dịch vụ bảo mật và quản lý quyền trên AWS.
* Thực hành IAM, KMS, Security Hub và Resource Tagging.
* Tìm hiểu cơ chế phân quyền, mã hóa dữ liệu và quản lý tài nguyên trên AWS.

---

### Các công việc cần triển khai:

| Thứ | Nội dung học & thực hành | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|--------------------------|--------------|-----------------|--------------------|
| 2 | Module 05-01 → 05-03: Shared Responsibility Model, IAM, Cognito | 18/05/2026 | 18/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Module 05-04 → 05-06: AWS Organizations, Identity Center, AWS KMS | 19/05/2026 | 19/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Module 05-07 & 05-08: Security Hub, Hands-on Research | 20/05/2026 | 20/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 18 & Lab 22: Security Hub, Optimizing EC2 Costs with Lambda | 21/05/2026 | 21/05/2026 | AWS Study Group Labs |
| 6 | Lab 27, 28 & 30: Tags, IAM Policy, Permission Boundary | 22/05/2026 | 22/05/2026 | AWS Study Group Labs |
| 7 | Lab 33, 44 & 48: AWS KMS, IAM Role & Condition, IAM Role for EC2 | 23/05/2026 | 23/05/2026 | AWS Study Group Labs |

---

# 🧪 Chi tiết Lab đã thực hành

---

## 🔹 Lab 18 – Getting Started with AWS Security Hub

- Enable AWS Security Hub
- Kiểm tra Security Standards
- Theo dõi Security Score
- Clean up resources

👉 Hiểu:
- Centralized security monitoring
- Security compliance & recommendations

---

## 🔹 Lab 22 – Optimizing EC2 Costs with Lambda

- Tạo EC2 instance và Lambda Function
- Tự động Start/Stop EC2 bằng Lambda
- Tích hợp Slack Webhook notifications

👉 Hiểu:
- Cost optimization automation
- Event-driven architecture với Lambda

---

## 🔹 Lab 27 – Manage Resources Using Tags and Resource Groups

- Gắn Tags cho EC2 và AWS resources
- Filter resources bằng Tags
- Sử dụng Tags với AWS CLI
- Tạo Resource Groups

👉 Hiểu:
- Resource organization & management
- Quản lý tài nguyên theo môi trường / project

---

## 🔹 Lab 28 – Manage Access to EC2 Services with Resource Tags through IAM

- Tạo IAM User, Role, Policy
- Restrict EC2 access dựa trên Tags
- Test IAM permissions theo Region & Tags

👉 Hiểu:
- Attribute-Based Access Control (ABAC)
- Fine-grained access control với IAM

---

## 🔹 Lab 30 – IAM Permission Boundary

- Tạo Restriction Policy
- Tạo IAM Limited User
- Test quyền bị giới hạn

👉 Hiểu:
- Permission Boundary hoạt động như guardrail
- Giới hạn maximum permissions cho IAM User/Role

---

## 🔹 Lab 33 – Encrypt at Rest with AWS KMS

- Tạo AWS KMS Key
- Upload encrypted data lên S3
- Logging với CloudTrail
- Query logs bằng Athena

👉 Hiểu:
- Data encryption at rest
- Audit logging & monitoring

---

## 🔹 Lab 44 – IAM Role & Condition

- Tạo IAM Users, Groups, Roles
- Configure Switch Role
- Restrict role access theo:
  - IP Address
  - Time condition

👉 Hiểu:
- IAM Role Assume process
- Conditional access control

---

## 🔹 Lab 48 – IAM Role for Applications

- Tạo EC2 & S3 Bucket
- Sử dụng Access Key
- Gắn IAM Role vào EC2

👉 Hiểu:
- Best practice:
  - dùng IAM Role thay vì hardcode Access Key
- Secure application access tới AWS services

---

# ✅ Kết quả đạt được tuần 5:

- Hiểu các dịch vụ bảo mật AWS:
  - IAM
  - Cognito
  - KMS
  - Security Hub

- Thực hành:
  - IAM Policy & Role
  - Permission Boundary
  - Resource Tags
  - Security Monitoring

- Hiểu:
  - Encryption at rest
  - Access Control
  - Assume Role
  - Conditional IAM Policy

- Tự động hóa:
  - Start/Stop EC2 với Lambda
  - Cost optimization workflow

---