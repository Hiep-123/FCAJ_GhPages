---
title: "Blog 3"
date: 2026-07-08
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---


# Tăng cường bảo mật AWS Management Console với Sign-in Resource-based Policies và RCPs

Xin chào mọi người trong cộng đồng AWS Study Group VN!

AWS vừa giới thiệu một tính năng mới giúp tăng cường bảo mật cho AWS Management Console và AWS CLI thông qua Sign-in Resource-based Policies và Resource Control Policies (RCPs).

Giải pháp này cho phép doanh nghiệp chỉ cho phép người dùng đăng nhập AWS từ những mạng được tin cậy, giúp giảm nguy cơ truy cập trái phép và đáp ứng các yêu cầu về bảo mật.

Trong bài viết này, chúng ta sẽ cùng tìm hiểu:

- Sign-in Resource-based Policies hoạt động như thế nào
- RCPs giúp quản lý quyền truy cập ra sao
- Lợi ích của giải pháp này đối với doanh nghiệp

## 1. Sign-in Resource-based Policies là gì?

Trước đây, việc kiểm soát đăng nhập thường dựa vào IAM hoặc các chính sách xác thực. Với tính năng mới này, AWS cho phép áp dụng policy ngay tại quá trình đăng nhập, giúp kiểm soát nguồn truy cập trước khi người dùng vào được AWS Management Console.

Ví dụ, doanh nghiệp có thể chỉ cho phép đăng nhập từ:

- mạng nội bộ của công ty
- VPN doanh nghiệp
- Amazon VPC đã được chỉ định

Mọi yêu cầu đến từ mạng công cộng hoặc các địa điểm không nằm trong danh sách cho phép sẽ bị từ chối ngay từ bước đăng nhập.

## 2. RCPs giúp quản lý tập trung

Khi sử dụng AWS Organizations, Resource Control Policies (RCPs) giúp áp dụng cùng một quy tắc bảo mật cho nhiều tài khoản AWS.

Điều này giúp các tổ chức duy trì một network perimeter thống nhất, giảm sai sót khi cấu hình riêng lẻ và đảm bảo tất cả tài khoản đều tuân thủ cùng một chính sách bảo mật.

## 3. Những lợi ích nổi bật

Giải pháp mới mang lại nhiều lợi ích như:

- chỉ cho phép đăng nhập từ các mạng đáng tin cậy
- giảm nguy cơ truy cập từ Wi-Fi công cộng hoặc thiết bị không được kiểm soát
- cho phép chỉ định tài khoản quản trị luôn có quyền truy cập để tránh bị khóa ngoài
- ghi lại đầy đủ các lần đăng nhập thành công hoặc bị từ chối thông qua AWS CloudTrail, hỗ trợ kiểm toán và đáp ứng yêu cầu tuân thủ

## Kết luận

Với Sign-in Resource-based Policies và Resource Control Policies, AWS bổ sung thêm một lớp bảo vệ ngay từ quá trình đăng nhập, giúp doanh nghiệp kiểm soát chặt chẽ nguồn truy cập vào AWS Management Console.

Kết hợp cùng AWS Organizations, AWS CloudTrail và các dịch vụ bảo mật khác, giải pháp này giúp:

- tăng cường bảo mật tài khoản AWS
- thiết lập ranh giới mạng (network perimeter) hiệu quả
- quản lý chính sách tập trung trên nhiều tài khoản
- hỗ trợ đáp ứng các yêu cầu về kiểm toán và tuân thủ

Đối với các doanh nghiệp vận hành hạ tầng trên AWS, đây là một tính năng mới đáng cân nhắc để nâng cao mức độ an toàn cho môi trường đám mây.

Nguồn tham khảo: https://aws.amazon.com/vi/blogs/security/restrict-aws-management-console-access-to-expected-networks-with-sign-in-resource-based-policies-and-rcps/
