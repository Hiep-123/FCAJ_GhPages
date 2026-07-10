---
title: "Blog 1"
date: 2026-07-08
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Xây dựng cơ chế xác thực hai lớp cho Nakama Game Server với Amazon Cognito trên AWS

Chào mọi người trong cộng đồng AWS Study Group VN!

Hôm nay mình muốn chia sẻ một kiến trúc khá thú vị từ AWS dành cho các hệ thống game multiplayer sử dụng **Nakama**.

Trong các game trực tuyến, việc quản lý **tài khoản người chơi** và **phiên kết nối trong game** thường là hai bài toán riêng biệt. Nếu không được thiết kế hợp lý, người chơi có thể phải xác thực nhiều lần hoặc gặp gián đoạn khi chuyển giữa các dịch vụ.

Để giải quyết vấn đề này, AWS giới thiệu mô hình **Dual-token Authentication**, kết hợp **Amazon Cognito** và **Nakama** nhằm đảm bảo vừa an toàn, vừa mang lại trải nghiệm đăng nhập liền mạch.

Bài viết sẽ giúp chúng ta hiểu:

- Dual-token Authentication là gì
- Kiến trúc hoạt động trên AWS như thế nào
- Vì sao mô hình này phù hợp với các hệ thống game multiplayer

## 1. Dual-token Authentication là gì?

Thay vì chỉ sử dụng một token cho toàn bộ hệ thống, giải pháp này chia quá trình xác thực thành hai bước.

Đầu tiên, **Amazon Cognito** xác minh danh tính người chơi và cấp **JWT Access Token**. Sau đó, khi người chơi kết nối đến **Nakama**, một **Go Runtime Hook** sẽ kiểm tra tính hợp lệ của JWT và tạo **Session Token** riêng để quản lý phiên chơi.

Nhờ việc tách biệt hai loại token, hệ thống vừa đảm bảo tính bảo mật, vừa giúp người chơi đăng nhập và tham gia game một cách liền mạch.

## 2. Kiến trúc trên AWS

Để triển khai giải pháp này, AWS sử dụng nhiều dịch vụ phối hợp với nhau:

- **Amazon CloudFront** và **AWS WAF** bảo vệ điểm vào và lọc lưu lượng độc hại.
- **Application Load Balancer** và **Network Load Balancer** định tuyến truy cập đến các dịch vụ phù hợp.
- **Amazon ECS** triển khai các dịch vụ game và runtime của Nakama.
- **Amazon Cognito** xử lý xác thực danh tính và phát hành token.
- **Nakama** sử dụng JWT đã được xác minh để tạo session token cho phiên chơi.

Sự kết hợp này tạo nên một kiến trúc vừa an toàn, vừa dễ mở rộng khi số lượng người chơi tăng lên.

{{< img src="images/3-BlogsTranslated/3.1-Blog1/blog3_1.jpg" alt="Kiến trúc tổng quan" >}}
## 3. Điểm nổi bật của mô hình

Một điểm đáng chú ý là AWS sử dụng đồng thời **ALB** và **NLB** thay vì chỉ một Load Balancer.

Toàn bộ lưu lượng vẫn đi qua **Amazon CloudFront**, vì vậy người chơi chỉ cần truy cập một endpoint duy nhất trong khi hệ thống tự động định tuyến đến dịch vụ phù hợp.

Mô hình này đặc biệt phù hợp với các game cần:

- xác thực nhanh và an toàn
- giao tiếp latency thấp
- mở rộng linh hoạt khi lưu lượng tăng đột biến

## Kết luận

Dual-token Authentication là một giải pháp đáng cân nhắc khi xây dựng game online trên AWS. Việc kết hợp **Amazon Cognito**, **Amazon CloudFront**, **AWS WAF**, **Application Load Balancer**, **Network Load Balancer** và **Amazon ECS** giúp tạo ra một kiến trúc hiện đại, cân bằng giữa bảo mật, hiệu năng và trải nghiệm người dùng.

Nguồn tham khảo: https://aws.amazon.com/vi/blogs/architecture/dual-token-authentication-for-nakama-game-servers-with-amazon-cognito-on-aws/
