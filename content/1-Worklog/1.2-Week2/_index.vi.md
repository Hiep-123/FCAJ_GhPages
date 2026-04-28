---
title: "Worklog Tuần 2"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Hiểu sâu về AWS Networking (VPC).
* Nắm được cách thiết kế mạng trong AWS.
* Thực hành triển khai các thành phần mạng: Subnet, Route Table, IGW, NAT Gateway.
* Làm quen với Hybrid Network, VPC Peering, Transit Gateway.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|----------|-------------|-----------------|----------------|
| 2 | - Module 02-01: AWS VPC <br> - Hiểu CIDR, Subnet, IP | 27/04/2026 | 27/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | - Module 02-02: VPC Security & Multi-VPC <br> - Security Group vs NACL | 28/04/2026 | 28/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | - Module 02-03 <br> - VPN, Direct Connect, Load Balancer | 29/04/2026 | 29/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Lab 03: VPC cơ bản (Subnet, Route Table, IGW, NAT) | 30/04/2026 | 30/04/2026 | https://000003.awsstudygroup.com/ |
| 6 | - Lab 10: Hybrid DNS (Route 53 Resolver) | 01/05/2026 | 01/05/2026 | https://000010.awsstudygroup.com/ |
| 7 | - Lab 19 + 20: VPC Peering & Transit Gateway | 02/05/2026 | 02/05/2026 | https://000019.awsstudygroup.com/ |

---

### Nội dung Lab đã thực hành:

#### 🔹 Lab 03 – Amazon VPC

- Tạo VPC, Subnet (Public/Private)
- Cấu hình Route Table
- Gắn Internet Gateway
- Tạo NAT Gateway
- Cấu hình Security Group, NACL
- Tạo EC2 và test kết nối

 Hiểu:
- Luồng traffic trong VPC
- Public vs Private subnet

---

#### 🔹 Lab 10 – Hybrid DNS

- Deploy CloudFormation
- Tạo Resolver Endpoint (Inbound/Outbound)
- Tạo Resolver Rules
- Test DNS

 Hiểu:
- Hybrid DNS hoạt động
- Kết nối On-premise với AWS

---

#### 🔹 Lab 19 – VPC Peering

- Tạo 2 VPC
- Tạo Peering Connection
- Update Route Table, NACL
- Enable DNS

 Hiểu:
- Kết nối giữa các VPC

---

#### 🔹 Lab 20 – Transit Gateway

- Tạo Transit Gateway
- Attach nhiều VPC
- Cấu hình Route

 Hiểu:
- Kiến trúc Hub-Spoke

---

### Kết quả đạt được tuần 2:

- Hiểu sâu về AWS VPC:
  - CIDR, Subnet, Routing
  - IGW, NAT Gateway

- Nắm rõ bảo mật:
  - Security Group vs NACL

- Thiết kế mạng:
  - Public / Private subnet

- Kết nối hệ thống:
  - VPC Peering
  - Transit Gateway
  - Hybrid DNS

- Thực hành:
  - Deploy EC2 trong nhiều subnet
  - Cấu hình routing