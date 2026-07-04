---
title: "Workshop"
date: 2026-07-04
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Nền tảng thương mại điện tử Serverless trên AWS — Workshop triển khai

Workshop này hướng dẫn bạn triển khai hoàn chỉnh nền tảng thương mại điện tử AWS Serverless từ đầu. Sau khi hoàn thành, bạn sẽ có một ứng dụng e-commerce hoạt động đầy đủ, có thể truy cập công khai trên **ap-southeast-1 (Singapore)**.

**Thời gian ước tính:** 90–120 phút  
**Region triển khai:** ap-southeast-1 (Singapore)  
**Region WAF:** us-east-1 (bắt buộc cho CloudFront)

---

## Tổng quan kiến trúc

> **Lưu ý:** Đây là sơ đồ triển khai đơn giản hóa. Tham khảo Proposal Phần 5 để xem kiến trúc sản xuất đầy đủ bao gồm chi tiết WAF rule, X-Ray tracing, log retention và cấu hình security headers.

Đây là sơ đồ triển khai đơn giản hóa. Tham khảo Proposal Phần 5 để xem kiến trúc sản xuất đầy đủ.

```
Trình duyệt
  └── CloudFront (HTTPS, HTTP/2+3, WAF, OAC)
        └── S3 FrontendBucket (private, React SPA)

API Gateway REST (100 rps / 200 burst)
  ├── Cognito Authorizer (JWT)
  ├── GET /products       → ProductServiceFunction  (public)
  ├── GET/POST/PUT/DELETE /cart → CartServiceFunction (auth)
  └── POST /orders, GET /orders, GET /orders/{id} → OrderServiceFunction (auth)
                                    │ PutEvents
                                    ▼
                    EcommerceEventBus (EventBridge)
                          └── Rule: OrderCreated
                                └── OrderQueue (SQS, maxReceive=3)
                                      ├── OrderProcessorFunction
                                      └── OrderDLQ (dead-letter)

EcommerceTable (DynamoDB, PAY_PER_REQUEST, PITR, 3 GSIs)
CloudWatch Dashboard + 6 Alarms → SNS → Email
WAF WebACL: IP Reputation + OWASP CRS + Rate Limit
```

---

## Nội dung workshop

1. [Chuẩn bị môi trường](5.1-environment-setup/)
2. [Triển khai các Backend Stack](5.2-deploy-backend/)
3. [Triển khai Frontend Stack](5.3-deploy-frontend/)
4. [Seed dữ liệu & Tạo người dùng](5.4-seed-and-users/)
5. [Xác minh & Kiểm thử](5.5-verify-and-test/)
6. [Dọn dẹp tài nguyên](5.6-cleanup/)
