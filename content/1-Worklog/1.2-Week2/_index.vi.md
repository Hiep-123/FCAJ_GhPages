---
title: "Worklog Tuần 2"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Hiểu và triển khai kiến trúc mạng trong AWS (VPC).
* Nắm rõ luồng traffic và cơ chế routing.
* Thực hành Hybrid Network, DNS, và Multi-VPC connectivity.

---

### Các công việc cần triển khai:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
|-----|----------|-------------|-----------------|--------|
| 2 | Module 02-01: AWS VPC (CIDR, Subnet, IP) | 27/04/2026 | 27/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 3 | Module 02-02: VPC Security (SG, NACL) | 28/04/2026 | 28/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 4 | Module 02-03: VPN, Direct Connect, LB | 29/04/2026 | 29/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | Lab 03: VPC + VPN | 30/04/2026 | 30/04/2026 | https://cloudjourney.awsstudygroup.com/ |
| 6 | Lab 10: Hybrid DNS | 01/05/2026 | 01/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 7 | Lab 19 & 20: Peering & Transit Gateway | 02/05/2026 | 02/05/2026 | https://cloudjourney.awsstudygroup.com/ |

---

##  Chi tiết Lab đã thực hành

---

### 🔹 Lab 03 – Amazon VPC + VPN

#### 1. Xây dựng VPC cơ bản

- Tạo VPC với CIDR block
- Tạo Subnet (public/private)
- Gắn Internet Gateway
- Cấu hình Route Table:
  - Public subnet → route 0.0.0.0/0 → IGW
- Tạo Security Group
- Bật VPC Flow Logs

 Hiểu:
- Flow traffic trong VPC
- Cách subnet quyết định public/private

---

#### 2. Deploy EC2 & kiểm tra kết nối

- Tạo EC2 instance
- SSH / connect test
- Tạo NAT Gateway cho private subnet
- Dùng Reachability Analyzer để kiểm tra network path
- Dùng:
  - EC2 Instance Connect Endpoint
  - Session Manager (SSM)

 Hiểu:
- Private subnet ra internet qua NAT
- Debug network bằng Reachability Analyzer

---

#### 3. Monitoring & Logging

- CloudWatch Monitoring
- Alerting cơ bản

 Hiểu:
- Quan sát trạng thái network & EC2

---

#### 4. Site-to-Site VPN

- Tạo:
  - Virtual Private Gateway (AWS side)
  - Customer Gateway (giả lập on-prem bằng EC2)
- Tạo VPN Connection
- Cấu hình tunnel

 Hiểu:
- Kết nối AWS ↔ On-premise
- IPSec tunnel hoạt động

---

#### 5. (Optional) VPN với Transit Gateway

- Tạo Transit Gateway
- Attach VPN
- Cấu hình routing

 Hiểu:
- Mô hình scalable hơn VGW

---

### 🔹 Lab 10 – Hybrid DNS

- Tạo Key Pair
- Deploy hạ tầng bằng CloudFormation
- Setup Microsoft AD

#### DNS Setup:

- Tạo Outbound Endpoint (DNS query từ AWS → on-prem)
- Tạo Inbound Endpoint (on-prem → AWS)
- Tạo Resolver Rules

 Hiểu:
- DNS resolution cross environment
- Hybrid DNS architecture

---

### 🔹 Lab 19 – VPC Peering

- Tạo EC2 ở 2 VPC
- Update NACL
- Tạo Peering Connection
- Cấu hình Route Tables
- Enable Cross-VPC DNS

 Hiểu:
- VPC ↔ VPC communication
- Không có transitive routing

---

### 🔹 Lab 20 – Transit Gateway

- Tạo Transit Gateway
- Attach nhiều VPC
- Tạo Route Tables riêng cho TGW
- Thêm route vào VPC route table

 Hiểu:
- Kiến trúc Hub-and-Spoke
- Thay thế VPC Peering khi scale lớn

---

## ✅ Kết quả đạt được:

- Hiểu sâu VPC:
  - CIDR, Subnet, Routing
  - IGW vs NAT Gateway

- Network security:
  - Security Group vs NACL

- Networking nâng cao:
  - VPN Site-to-Site
  - Hybrid DNS

- Multi-VPC:
  - VPC Peering (non-transitive)
  - Transit Gateway (scalable)

- Debug & Monitoring:
  - Reachability Analyzer
  - VPC Flow Logs
  - CloudWatch

---