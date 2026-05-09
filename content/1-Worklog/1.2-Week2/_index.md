---
title: "Week 2 Worklog"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Understand AWS VPC architecture in depth.
* Learn traffic flow and routing mechanisms.
* Practice Hybrid Networking and Multi-VPC connectivity.

---

### Weekly Tasks:

| Day | Tasks | Start | End |
|-----|------|------|-----|
| Mon | VPC fundamentals | 27/04 | 27/04 |
| Tue | Security (SG vs NACL) | 28/04 | 28/04 |
| Wed | VPN, Direct Connect | 29/04 | 29/04 |
| Thu | Lab 03 | 30/04 | 30/04 |
| Fri | Lab 10 | 01/05 | 01/05 |
| Sat | Lab 19 & 20 | 02/05 | 02/05 |

---

##  Lab Details

---

### 🔹 Lab 03 – VPC + VPN

#### VPC Setup

- Create VPC & Subnets
- Configure Internet Gateway
- Route Tables
- Security Groups
- Enable Flow Logs

 Learned:
- Traffic flow inside VPC
- Public vs Private subnet behavior

---

#### EC2 Deployment

- Launch EC2
- Test connectivity
- Setup NAT Gateway
- Use Reachability Analyzer
- Use SSM Session Manager

 Learned:
- Private subnet outbound access
- Network troubleshooting

---

#### Monitoring

- CloudWatch metrics & alerts

---

#### Site-to-Site VPN

- Create:
  - Virtual Private Gateway
  - Customer Gateway
- Configure VPN tunnels

 Learned:
- AWS ↔ On-prem connectivity

---

#### (Optional) Transit Gateway VPN

- TGW + VPN integration

---

### 🔹 Lab 10 – Hybrid DNS

- CloudFormation deployment
- Microsoft AD setup

#### DNS:

- Outbound Endpoint
- Inbound Endpoint
- Resolver Rules

 Learned:
- Hybrid DNS resolution

---

### 🔹 Lab 19 – VPC Peering

- Create 2 VPCs
- Peering connection
- Route table updates
- NACL updates

 Learned:
- VPC-to-VPC communication
- No transitive routing

---

### 🔹 Lab 20 – Transit Gateway

- Create TGW
- Attach VPCs
- Configure routing

 Learned:
- Hub-and-Spoke architecture
- Scalable network design

---

##  Achievements:

- Deep understanding of VPC:
  - CIDR, Subnets, Routing
  - IGW vs NAT

- Network Security:
  - SG vs NACL

- Advanced Networking:
  - VPN
  - Hybrid DNS

- Multi-VPC:
  - Peering vs Transit Gateway

- Monitoring & Debug:
  - Flow Logs
  - Reachability Analyzer
  - CloudWatch