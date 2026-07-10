---
title: "Worklog Tuần 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---


### Mục tiêu tuần 12 (06/07/2026 - 12/07/2026):

* Tối ưu các triển khai AWS theo 5 trụ cột: Vận hành, Bảo mật, Độ tin cậy, Hiệu năng và Tối ưu chi phí.
* Thực hành các giải pháp cụ thể: Lambda tự động, CloudWatch + Grafana, Systems Manager (SSM), CloudFormation (IaC), SSO, ECS, phân tích chi phí.

### Công việc triển khai trong tuần:
| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu / Tham khảo |
|------|----------|--------------|-----------------|----------------------|
| Thứ Hai (06/07/2026) | Operate: Tự động tắt server & gửi Slack bằng **AWS Lambda** | 06/07/2026 | 06/07/2026 | https://000022.awsstudygroup.com/ |
| Thứ Ba (07/07/2026) | Operate: Tạo dashboard giám sát với **CloudWatch + Grafana** | 07/07/2026 | 07/07/2026 | https://000029.awsstudygroup.com/ |
| Thứ Tư (08/07/2026) | Operate: Dùng **AWS Systems Manager (Session Manager)** để truy cập instance an toàn | 08/07/2026 | 08/07/2026 | https://000058.awsstudygroup.com/ |
| Thứ Năm (09/07/2026) | Operate/IaC: Khởi tạo template **CloudFormation** đơn giản để provision tài nguyên | 09/07/2026 | 09/07/2026 | https://000037.awsstudygroup.com/ |
| Thứ Sáu (10/07/2026) | Security: Bảo vệ ứng dụng và API bằng **AWS WAF** | 10/07/2026 | 10/07/2026 | https://000026.awsstudygroup.com/ |
| Thứ Bảy (11/07/2026) | Performance: Containerize và deploy ứng dụng lên **Amazon ECS** | 11/07/2026 | 11/07/2026 | https://000016.awsstudygroup.com/ |
| Chủ Nhật (12/07/2026) | Cost Optimization: So sánh Savings Plans / RIs và visualise chi phí | 12/07/2026 | 12/07/2026 | https://000042.awsstudygroup.com/ |

### Kết quả đạt được:

- Vận hành: Thử nghiệm kịch bản Lambda tự động tắt server và gửi Slack; cấu hình dashboard CloudWatch → Grafana. (Tham khảo: https://000022.awsstudygroup.com/ , https://000029.awsstudygroup.com/)
- Operate: Dùng **Session Manager (SSM)** để truy cập instance an toàn. (Tham khảo: https://000058.awsstudygroup.com/)
- IaC: Tạo template CloudFormation đơn giản để provision môi trường thử nghiệm. (Tham khảo: https://000037.awsstudygroup.com/)
- Bảo mật: Cấu hình rule **AWS WAF** để bảo vệ ứng dụng và API (proof-of-concept). (Tham khảo: https://000026.awsstudygroup.com/)
- Hiệu năng: Containerize và deploy ứng dụng mẫu lên Amazon ECS. (Tham khảo: https://000016.awsstudygroup.com/)
- Tối ưu chi phí: So sánh Savings Plans và Reserved Instances; visualise xu hướng chi phí. (Tham khảo: https://000042.awsstudygroup.com/)



