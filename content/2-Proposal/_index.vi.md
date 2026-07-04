---
title: "Bản đề xuất"
date: 2026-07-04
draft: false
toc: true
weight: 2
chapter: false
pre: "2."
---

# Nền tảng thương mại điện tử Serverless trên AWS
## Hệ thống mua sắm cloud-native sẵn sàng cho môi trường sản xuất, xây dựng trên kiến trúc AWS Serverless



### 1. Tóm tắt điều hành

Dự án này xây dựng một nền tảng thương mại điện tử hoàn chỉnh, cấp độ sản xuất, dựa hoàn toàn trên các dịch vụ serverless và dịch vụ được quản lý của AWS. Hệ thống hỗ trợ toàn bộ vòng đời mua sắm của khách hàng — duyệt sản phẩm, quản lý giỏ hàng, đặt hàng và theo dõi đơn hàng theo thời gian thực — mà không cần quản lý hay duy trì bất kỳ cơ sở hạ tầng máy chủ nào.

Nền tảng được triển khai tại region **ap-southeast-1 (Singapore)** sử dụng **AWS Cloud Development Kit (CDK) với TypeScript** làm framework infrastructure-as-code. Dự án chứng minh khả năng áp dụng thực tế các nguyên tắc AWS Well-Architected Framework trên cả năm trụ cột: bảo mật, độ tin cậy, hiệu năng, tối ưu chi phí và xuất sắc vận hành.

Dự án được nghiên cứu và triển khai trong suốt kỳ thực tập ba tháng như một minh chứng thực tiễn về thiết kế kiến trúc cloud, phát triển serverless và triển khai trên AWS.



### 2. Tuyên bố vấn đề

#### Bối cảnh

Các doanh nghiệp thương mại điện tử hiện đại yêu cầu cơ sở hạ tầng có thể xử lý lưu lượng truy cập không thể dự đoán, duy trì tính sẵn sàng cao, thực thi bảo mật ở mọi lớp và tiết kiệm chi phí trong các giai đoạn hoạt động thấp. Các hệ thống triển khai truyền thống dựa trên máy chủ mang lại chi phí vận hành đáng kể: máy chủ phải được cấp phát, vá lỗi, mở rộng quy mô và giám sát liên tục bất kể lưu lượng thực tế.

#### Những thách thức chính

**Sự phức tạp trong vận hành:** Hệ thống dựa trên máy chủ đòi hỏi đội ngũ vận hành chuyên trách, cửa sổ bảo trì theo lịch định kỳ và các quyết định mở rộng quy mô thủ công gây ra rủi ro và chi phí.

**Kém hiệu quả về chi phí ở tải thay đổi:** Máy chủ cố định công suất phát sinh chi phí ngay cả khi nhàn rỗi. Một nền tảng thương mại điện tử tự nhiên có những khoảng thời gian lưu lượng rất thấp (ban đêm, mùa thấp điểm) khiến công suất nhàn rỗi bị lãng phí.

**Diện tích bề mặt bảo mật:** Máy chủ tiếp xúc công khai, dữ liệu không được mã hóa khi lưu trữ và truyền tải, cũng như cơ chế xác thực yếu vẫn là nguyên nhân hàng đầu dẫn đến vi phạm dữ liệu trong thương mại điện tử.

**Tốc độ phát triển:** Backend nguyên khối kết hợp chặt chẽ làm chậm quá trình lặp và khiến việc triển khai các cải tiến cho từng khu vực dịch vụ riêng lẻ trở nên khó khăn mà không gây rủi ro cho toàn bộ hệ thống.

#### Cơ hội

AWS cung cấp một hệ sinh thái serverless được quản lý hoàn toàn giải quyết tất cả những thách thức này. Bằng cách kết hợp API Gateway, Lambda, DynamoDB, EventBridge và CloudFront, hoàn toàn có thể xây dựng một backend thương mại điện tử có khả năng mở rộng, bảo mật và quan sát được — không tốn chi phí khi nhàn rỗi và tự động mở rộng quy mô dưới tải — mà không cần quản lý bất kỳ máy chủ nào.



### 3. Mục tiêu

1. Thiết kế và triển khai API thương mại điện tử serverless cấp độ sản xuất bao gồm sản phẩm, giỏ hàng và đơn hàng.
2. Triển khai xử lý đơn hàng bất đồng bộ theo hướng sự kiện sử dụng EventBridge và SQS để tách biệt việc tạo đơn hàng khỏi quy trình xử lý.
3. Thực thi xác thực và phân quyền sử dụng Amazon Cognito với xác minh JWT token tại lớp API.
4. Triển khai toàn bộ cơ sở hạ tầng dưới dạng code sử dụng AWS CDK TypeScript, đảm bảo triển khai có thể lặp lại và kiểm toán được.
5. Bảo mật ứng dụng hướng đến khách hàng bằng AWS WAF, CloudFront, TLS 1.2+ và IAM với quyền tối thiểu cần thiết.
6. Đạt khả năng quan sát đầy đủ với CloudWatch Dashboard, sáu cảnh báo vận hành, X-Ray tracing và thông báo email qua SNS.
7. Cung cấp ứng dụng React 19 single-page có khả năng phản hồi, phục vụ qua CloudFront với caching tài nguyên theo content-hash.
8. Chứng minh sự phù hợp với tất cả năm trụ cột của AWS Well-Architected Framework.



### 4. Giải pháp đề xuất

Giải pháp là một nền tảng thương mại điện tử cloud-native được tổng hợp từ các stack cơ sở hạ tầng có thể triển khai độc lập, mỗi stack chịu trách nhiệm cho một domain được xác định rõ ràng.

#### Triết lý kiến trúc

Hệ thống tuân theo mô hình thiết kế **serverless-first, event-driven**. Không có EC2 instance, không có container và không có tiến trình máy chủ nào liên tục. Mọi đơn vị tính toán đều là Lambda function được gọi theo yêu cầu. Mọi tài nguyên cơ sở hạ tầng đều được định nghĩa bằng TypeScript sử dụng AWS CDK và triển khai qua CloudFormation.

#### Luồng khách hàng

Khách hàng tương tác với ứng dụng React 19 single-page được phục vụ từ CloudFront. Các lời gọi API đi từ trình duyệt qua CloudFront đến API Gateway, nơi xác thực JWT Cognito và định tuyến yêu cầu đến Lambda function phù hợp. Lambda đọc và ghi vào DynamoDB sử dụng thiết kế single-table. Khi khách hàng đặt hàng, Order Service xuất bản sự kiện `OrderCreated` lên EventBridge, nơi định tuyến đến hàng đợi SQS. Lambda Order Processor tiêu thụ thông điệp hàng đợi bất đồng bộ, cập nhật trạng thái đơn hàng qua vòng đời `PENDING → PROCESSING → COMPLETED` và xuất bản sự kiện trạng thái trở lại EventBridge. Trình duyệt của khách hàng thực hiện polling endpoint chi tiết đơn hàng mỗi ba giây để hiển thị cập nhật trạng thái trực tiếp.

#### Các quyết định thiết kế chính

- **Thiết kế DynamoDB single-table** — tất cả các thực thể (sản phẩm, mục giỏ hàng, đơn hàng) chia sẻ một bảng với access pattern dựa trên GSI, loại bỏ nhu cầu join và cho phép đọc theo key O(1) cho tất cả các đường dẫn hot.
- **HTTP 202 Accepted khi tạo đơn hàng** — Order Service phản hồi ngay lập tức sau khi lưu trữ đơn hàng PENDING và xuất bản sự kiện, giữ thời gian phản hồi API xác định bất kể độ phức tạp xử lý downstream.
- **Tiêm cấu hình runtime** — ID pool Cognito và URL API được tiêm tại thời điểm triển khai qua file `/config.json` được phục vụ từ CloudFront, ngăn các giá trị đặc thù theo môi trường được baked vào JavaScript bundle.
- **WAF tại us-east-1** — WebACL WAF được triển khai tại us-east-1 theo yêu cầu đối với WebACL có phạm vi CloudFront, và ARN của nó được truyền cho FrontendStack như biến môi trường để giải quyết giới hạn cross-region của CloudFormation export.



### 5. Tổng quan kiến trúc AWS


```text
Trình duyệt └── CloudFront (HTTPS, HTTP/2+3, WAF, OAC, PRICE_CLASS_200) └── S3 FrontendBucket (private, SSE-S3, versioned)

API Gateway REST (ap-southeast-1, 100 rps / 200 burst) ├── Cognito Authorizer (cache 5 phút, xác thực JWT) ├── GET /products[?category][?search][?sort] → ProductServiceFunction ├── GET /products/{slugOrId} → ProductServiceFunction ├── GET /cart, POST /cart, PUT /cart, DELETE /cart/{productId} → CartServiceFunction └── POST /orders, GET /orders, GET /orders/{id} → OrderServiceFunction │ PutEvents │ ▼ EcommerceEventBus (EventBridge custom bus) │ └── Rule: OrderCreated └── OrderQueue (SQS, 180s visibility, maxReceiveCount=3) ├── OrderProcessorFunction (ARM64, Node22) │ ├── DynamoDB UpdateItem (PROCESSING/COMPLETED/FAILED) │ └── PutEvents (OrderProcessing/OrderCompleted/OrderFailed) └── OrderDLQ (SQS, lưu trữ 14 ngày)

EcommerceTable (DynamoDB, PAY_PER_REQUEST, PITR, SSE, TTL) ├── GSI1 — CATEGORY#{category} → sản phẩm theo danh mục ├── GSI2 — USER#{userId} → đơn hàng theo người dùng (mới nhất trước) └── GSI3 — PRODUCT → toàn bộ catalog sản phẩm

CloudWatch Dashboard + 6 Alarms → SNS Topic → Email WAF WebACL (us-east-1): IP Reputation + OWASP CRS + Known Bad Inputs + giới hạn 1000 req/5min Cognito UserPool (ap-southeast-1): xác thực email, SRP, nhóm CUSTOMER/ADMIN

```


### 6. Dịch vụ AWS

| Dịch vụ | Vai trò trong nền tảng |
|---------|----------------------|
| **Amazon Cognito** | Đăng ký và xác thực người dùng. Đăng ký qua email với xác minh, luồng xác thực SRP và USER_PASSWORD, nhóm CUSTOMER và ADMIN, JWT token đính kèm mọi yêu cầu API được bảo vệ. |
| **Amazon API Gateway** | Điểm vào REST API. Throttle 100 rps ổn định, burst 200. Cognito JWT authorizer với cache kết quả 5 phút. Nhật ký truy cập JSON có cấu trúc lưu trữ 30 ngày. Route public cho sản phẩm, route được bảo vệ cho giỏ hàng và đơn hàng. |
| **AWS Lambda** | Bốn function trên ARM64 Graviton2 (Node.js 22): ProductServiceFunction, CartServiceFunction, OrderServiceFunction, OrderProcessorFunction. Tất cả được bundle bằng esbuild (minified, source-mapped). Tất cả được trace bằng AWS X-Ray. |
| **Amazon DynamoDB** | Thiết kế single-table. Tính phí PAY_PER_REQUEST. Point-in-time recovery được bật. Mã hóa bằng khóa quản lý AWS. Thuộc tính TTL cho item giỏ hàng hết hạn. Ba GSI bao gồm truy vấn theo danh mục, lịch sử đơn hàng theo người dùng và truy cập toàn bộ catalog sản phẩm. |
| **Amazon EventBridge** | Custom event bus `EcommerceEventBus`. Sự kiện OrderCreated được định tuyến đến SQS qua pattern matching theo `source=ecommerce.orders, detail-type=OrderCreated`. |
| **Amazon SQS** | `EcommerceOrderQueue` (chính, visibility timeout 180s, lưu trữ 4 ngày) và `EcommerceOrderDLQ` (dead-letter, lưu trữ 14 ngày, maxReceiveCount=3). Mã hóa được quản lý bởi SQS. |
| **Amazon S3** | Bucket private (`ecommerce-frontend-{account}-ap-southeast-1`) lưu trữ React SPA. Chặn tất cả truy cập public, mã hóa SSE-S3, versioning được bật, chỉ cho phép HTTPS. Truy cập độc quyền qua CloudFront OAC. |
| **Amazon CloudFront** | CDN toàn cầu phục vụ React SPA. OAC (không dùng OAI legacy). HTTP/2+3. PRICE_CLASS_200. TLS 1.2 tối thiểu. Hai cache behavior: CACHING_DISABLED cho `index.html`/`config.json`, CachingOptimized cho `/assets/*` (Vite content-hashed bundle). Bảo mật header OWASP qua managed response headers policy. SPA routing qua 403/404 → `index.html`. |
| **AWS WAF v2** | WebACL đính kèm CloudFront (us-east-1). Bốn managed rule group: IP Reputation List, Common Rule Set (OWASP CRS), Known Bad Inputs (Log4j, Spring4Shell, SSRF). Rule rate-based: 1000 yêu cầu mỗi 5 phút mỗi IP. Nhật ký WAF ghi vào CloudWatch (lưu trữ 30 ngày). |
| **Amazon CloudWatch** | Dashboard (`EcommerceDashboard`) với năm hàng: API Gateway, EventBridge, OrderService, OrderProcessor, SQS. Sáu alarm bao gồm lỗi Lambda, throttle Lambda, tin nhắn DLQ và lỗi 5XX của API. Tất cả alarm xuất bản lên SNS khi vi phạm. |
| **Amazon SNS** | `EcommerceAlarmsTopic` nhận thông báo alarm. Subscription email gửi cảnh báo đến hộp thư vận hành. |
| **AWS CDK (TypeScript)** | Toàn bộ cơ sở hạ tầng được định nghĩa dưới dạng code trên tám stack: AuthStack, DatabaseStack, EventStack, ApiStack, MonitoringStack, SecurityStack, FrontendStack, InfrastructureStack. Triển khai tại ap-southeast-1. |
| **AWS X-Ray** | Active tracing được bật trên tất cả bốn Lambda function. Trace các lời gọi DynamoDB và EventBridge downstream từ đầu đến cuối. |



### 7. Cân nhắc theo AWS Well-Architected Framework

#### Xuất sắc vận hành (Operational Excellence)
Toàn bộ cơ sở hạ tầng được định nghĩa dưới dạng code trong AWS CDK TypeScript. Mỗi stack có thể triển khai độc lập bằng `npx cdk deploy <StackName>`. CloudWatch cung cấp dashboard vận hành năm hàng bao gồm tất cả các tầng dịch vụ. Sáu alarm với `TreatMissingData=NOT_BREACHING` ngăn cảnh báo sai trong các giai đoạn yên tĩnh. Lambda source map cho phép đọc stack trace trong CloudWatch. X-Ray active tracing trên tất cả các function cung cấp khả năng hiển thị yêu cầu từ đầu đến cuối.

#### Bảo mật (Security)
Xác thực được thực thi qua Amazon Cognito JWT trên tất cả các route không công khai. Cognito authorizer của API Gateway cache kết quả năm phút, giảm độ trễ mà không ảnh hưởng bảo mật. Chính sách IAM tuân theo quyền tối thiểu — mỗi Lambda function có role riêng chỉ với các action DynamoDB cụ thể mà nó cần (ví dụ OrderProcessorFunction chỉ có `GetItem` và `UpdateItem`, không có `PutItem` hay `Scan`). S3 là private với HTTPS được thực thi. CloudFront chuyển hướng tất cả HTTP sang HTTPS. WAF chặn các IP độc hại đã biết, pattern tấn công OWASP Top 10 và client lạm dụng tốc độ. CORS sử dụng allowed origin rõ ràng (domain CloudFront) thay vì wildcard. Không có thông tin đăng nhập được hardcode ở bất kỳ đâu trong codebase — tất cả giá trị nhạy cảm được đọc từ biến môi trường tại thời điểm CDK synth hoặc từ `config.json` runtime được tiêm tại thời điểm triển khai.

#### Độ tin cậy (Reliability)
SQS `maxReceiveCount=3` đảm bảo các lần thử xử lý đơn hàng thất bại được thử lại trước khi định tuyến đến DLQ. `visibilityTimeout=180s` là sáu lần Lambda timeout (30s), tuân theo best practice AWS. DLQ lưu trữ 14 ngày cung cấp đủ thời gian để điều tra và phát lại. `ConditionExpression: attribute_not_exists(PK)` khi tạo đơn hàng ngăn đơn hàng trùng lặp trong điều kiện retry. Order Processor kiểm tra `status !== 'PENDING'` trước khi xử lý, cung cấp idempotency trước việc SQS giao hàng trùng lặp. DynamoDB PITR cho phép khôi phục point-in-time đến bất kỳ giây nào trong 35 ngày qua.

#### Hiệu năng (Performance Efficiency)
Tất cả Lambda function chạy trên ARM64 Graviton2, cung cấp khoảng 20% hiệu năng trên đơn vị giá tốt hơn so với x86. Node.js 22 với esbuild bundling và minification giảm kích thước cold-start package. AWS SDK v3 được bundle trực tiếp, loại bỏ phụ thuộc phiên bản runtime. DynamoDB PAY_PER_REQUEST scale về zero khi không có traffic và xử lý bất kỳ burst nào tự động. Behavior CachingOptimized của CloudFront với filename content-hashed Vite cho phép cache trình duyệt giữ tài nguyên vô thời hạn, giảm tải origin. Behavior CACHING_DISABLED trên `index.html` và `config.json` đảm bảo việc triển khai được phản ánh ngay lập tức. HTTP/2 và HTTP/3 giảm chi phí kết nối cho SPA.

#### Tối ưu chi phí (Cost Optimization)
Toàn bộ nền tảng là serverless — không có chi phí khi nhàn rỗi. DynamoDB PAY_PER_REQUEST có nghĩa là không có capacity unit được cung cấp dư thừa. Lambda tính phí theo từng 100ms gọi. CloudFront PRICE_CLASS_200 giới hạn edge location ở Mỹ, Châu Âu và Israel, giảm chi phí CDN mà không ảnh hưởng đáng kể đến độ trễ cho region mục tiêu (ap-southeast-1 là origin). Các CloudWatch log group có chính sách lưu trữ 30 ngày rõ ràng, ngăn chi phí lưu trữ không giới hạn. Không có EC2, RDS, ALB và chi phí NAT Gateway.

#### Bền vững (Sustainability)
Bộ xử lý ARM64 Graviton2 tiêu thụ ít năng lượng hơn trên mỗi đơn vị tính toán so với x86. CloudFront caching giảm số lần gọi Lambda và đọc DynamoDB cần thiết để phục vụ các yêu cầu lặp lại. PAY_PER_REQUEST có nghĩa là tài nguyên tính toán chỉ được cấp phát khi thực sự cần, không tiêu thụ khi nhàn rỗi.



### 8. Lộ trình triển khai

| Giai đoạn | Mô tả | Thời gian |
|-----------|-------|----------|
| **Giai đoạn 1** | Nền tảng cơ sở hạ tầng: thiết lập dự án CDK, AuthStack (Cognito), DatabaseStack (thiết kế DynamoDB single-table với GSI1/GSI2/GSI3), cấu trúc dự án ban đầu | Tuần 1–2 |
| **Giai đoạn 2–4** | Phát triển API lõi: ProductServiceFunction (catalog công khai với lọc danh mục), CartServiceFunction (CRUD có xác thực), OrderServiceFunction (đặt hàng) | Tuần 3–4 |
| **Giai đoạn 5–6** | Xử lý đơn hàng theo hướng sự kiện: EventBridge custom bus, SQS OrderQueue + DLQ, OrderProcessorFunction (vòng đời PENDING → PROCESSING → COMPLETED), X-Ray tracing | Tuần 5–6 |
| **Giai đoạn 7** | Phát triển frontend: React 19 + Vite SPA, FrontendStack (S3 + CloudFront OAC), tiêm cấu hình runtime qua `config.json`, tích hợp Cognito SDK, SPA routing | Tuần 7–8 |
| **Giai đoạn 8** | Tăng cường bảo mật: WAF WebACL (SecurityStack tại us-east-1), IP reputation, OWASP CRS, Known Bad Inputs, rate limiting, HTTPS enforcement, security response headers | Tuần 9 |
| **Giai đoạn 9** | Quan sát hệ thống: MonitoringStack (CloudWatch Dashboard, 6 alarm, SNS email subscription), structured access log, wiring alarm action | Tuần 10 |
| **Giai đoạn 10** | Cải tiến sản phẩm và UX: tìm kiếm trực tiếp, sắp xếp theo giá, URL theo slug, làm phong phú tên sản phẩm trong giỏ hàng, polling trạng thái đơn hàng, dọn dẹp frontend | Tuần 11 |
| **Hoàn thiện** | Sửa bảo mật backend (kiểm tra quyền sở hữu đơn hàng, xác thực đầu vào, kiểm tra biến môi trường), dọn dẹp backend và frontend, tài liệu hóa | Tuần 12 |



### 9. Ước tính chi phí

Tất cả ước tính chi phí sử dụng region **AWS Asia Pacific (Singapore) ap-southeast-1** và phản ánh mức sử dụng dự kiến cho nền tảng ở quy mô demo với lưu lượng vừa phải (khoảng 1.000 yêu cầu API mỗi ngày).

| Dịch vụ | Giả định sử dụng | Chi phí ước tính/tháng |
|---------|----------------|----------------------|
| AWS Lambda | 30.000 lần gọi/tháng, 512 MB, trung bình 200ms | ~$0,00 (free tier: 1M lần gọi) |
| Amazon API Gateway | 30.000 lời gọi REST API/tháng | ~$0,11 |
| Amazon DynamoDB | PAY_PER_REQUEST, ~50.000 đọc + 10.000 ghi/tháng | ~$0,04 |
| Amazon SQS | ~1.000 tin nhắn đơn hàng/tháng | ~$0,00 (free tier: 1M request) |
| Amazon EventBridge | ~1.000 sự kiện tùy chỉnh/tháng | ~$0,00 (free tier: 1M sự kiện) |
| Amazon S3 | ~100 MB tài nguyên SPA, ~10.000 yêu cầu CloudFront | ~$0,01 |
| Amazon CloudFront | ~5 GB truyền dữ liệu/tháng, PRICE_CLASS_200 | ~$0,43 |
| AWS WAF | 1 WebACL, ~30.000 yêu cầu/tháng | ~$5,00 (WebACL: $5,00/tháng) |
| Amazon Cognito | <50.000 MAU | ~$0,00 (free tier: 50.000 MAU) |
| Amazon CloudWatch | 1 dashboard, 6 alarm, ~5 GB log/tháng | ~$3,50 |
| Amazon SNS | <1.000 thông báo email/tháng | ~$0,00 |
| **Tổng cộng** | | **~$9,09/tháng** |

Chi phí lớn nhất là phí cố định WAF WebACL ($5,00/tháng). Ở mức zero traffic, nền tảng tốn khoảng $5,00/tháng. Tất cả dịch vụ khác nằm trong giới hạn free tier AWS ở quy mô demo.

Đối với triển khai quy mô sản xuất với 100.000 yêu cầu/ngày và 10.000 người dùng hoạt động hàng tháng, chi phí ước tính sẽ vào khoảng $35–$60/tháng — vẫn thấp hơn đáng kể so với các triển khai dựa trên máy chủ tương đương.



### 10. Đánh giá rủi ro

#### Ma trận rủi ro

| Rủi ro | Khả năng xảy ra | Mức độ ảnh hưởng | Biện pháp giảm thiểu |
|--------|----------------|-----------------|---------------------|
| Lambda cold start ảnh hưởng độ trễ cảm nhận | Trung bình | Thấp | ARM64 Graviton2 giảm thời gian cold start; esbuild bundling thu nhỏ kích thước package; DynamoDB PAY_PER_REQUEST loại bỏ thời gian khởi động |
| DynamoDB hot partition khi ghi đồng thời cao | Thấp | Cao | Thiết kế single-table sử dụng `orderId` ngẫu nhiên (UUID v4) làm tiền tố partition key, phân phối lệnh ghi đều các partition |
| Lỗi xử lý SQS message khiến đơn hàng bị kẹt | Thấp | Cao | DLQ lưu trữ 14 ngày và `maxReceiveCount=3` ngăn mất message; visibility timeout 6× ngăn requeue quá sớm; CloudWatch alarm bật khi có tin nhắn DLQ đầu tiên |
| JWT Cognito hết hạn gây lỗi 401 trong phiên dài | Trung bình | Trung bình | Axios response interceptor thực hiện silent token refresh qua Cognito SDK khi nhận 401; chuyển hướng đến login chỉ khi refresh token cũng hết hạn |
| WAF false positive chặn yêu cầu hợp lệ | Thấp | Trung bình | Managed rule group được đặt ở chế độ block nhưng có thể chuyển sang COUNT mode qua CDK override nếu phát hiện false positive |
| Phụ thuộc WAF ARN cross-region (SecurityStack → FrontendStack) | Thấp | Trung bình | WAF ARN được truyền qua biến môi trường (`WAF_WEB_ACL_ARN`) thay vì `Fn.importValue` để giải quyết giới hạn cross-region của CloudFormation export; được tài liệu hóa trong `.env.example` |
| Cấu hình sai ALLOWED_ORIGIN gây lỗi CORS | Trung bình | Cao | `ALLOWED_ORIGIN` phải được đặt thành CloudFront URL sau khi deploy FrontendStack; được tài liệu hóa trong `.env.example`; API fallback về `localhost:5173` nếu để trống |
| Cạn kiệt Lambda concurrency cấp tài khoản | Thấp | Trung bình | Nền tảng serverless không có reserved concurrency chia sẻ pool tài khoản; thêm reserved concurrency cho OrderProcessorFunction sẽ cô lập pipeline xử lý đơn hàng |

#### Kế hoạch dự phòng

- Tất cả stack có thể triển khai lại độc lập qua `npx cdk deploy <StackName>`.
- DynamoDB PITR cho phép khôi phục đến bất kỳ giây nào trong 35 ngày qua.
- Thư mục build `dist/` và tất cả CDK stack đều có thể tái tạo hoàn toàn từ source code.



### 11. Kết quả kỳ vọng

#### Sản phẩm kỹ thuật

1. **Tám CDK stack có thể triển khai độc lập** bao gồm toàn bộ nền tảng — xác thực, cơ sở dữ liệu, API, xử lý sự kiện, giám sát, bảo mật và phân phối frontend.

2. **Ba Lambda function cấp sản xuất** xử lý duyệt catalog sản phẩm công khai (với lọc danh mục, tìm kiếm text, sắp xếp theo giá và URL theo slug) cùng quản lý giỏ hàng và đơn hàng có xác thực.

3. **Pipeline xử lý đơn hàng theo hướng sự kiện** chứng minh kiến trúc bất đồng bộ: API tách biệt khỏi xử lý, SQS là bộ đệm tin cậy, DLQ để cô lập lỗi và chuyển đổi trạng thái idempotent trong DynamoDB.

4. **SPA hướng đến khách hàng bảo mật** với xác thực Cognito, polling trạng thái đơn hàng thời gian thực (interval 3 giây với phát hiện trạng thái kết thúc) và thiết kế responsive.

5. **Stack quan sát đầy đủ** với CloudWatch Dashboard năm hàng, sáu alarm vận hành, thông báo email qua SNS và X-Ray trace trên tất cả Lambda function.

6. **Bảo vệ WAF** bao gồm IP reputation, OWASP Top 10, các pattern khai thác đã biết và giới hạn tốc độ theo IP.

#### Kết quả học tập

- Áp dụng AWS CDK TypeScript cho infrastructure-as-code trên 8 stack và khoảng 2.000 dòng định nghĩa CDK.
- Triển khai thiết kế DynamoDB single-table với access pattern dựa trên GSI và không có thao tác Scan.
- Xây dựng pipeline xử lý bất đồng bộ theo hướng sự kiện với EventBridge, SQS và Lambda.
- Áp dụng AWS Well-Architected Framework trên tất cả năm trụ cột trong triển khai thực tế.
- Hoàn thành ứng dụng fullstack serverless từ tài khoản AWS trống đến URL CloudFront có thể truy cập công khai.

#### Đánh giá theo AWS Well-Architected Framework

Hệ thống triển khai cuối cùng đạt được các tiêu chí sau theo AWS Well-Architected Framework:

| Trụ cột | Trạng thái |
|---------|-----------|
| Xuất sắc vận hành | ✅ IaC, structured logging, CloudWatch Dashboard, 6 alarm, X-Ray |
| Bảo mật | ✅ Cognito JWT, IAM quyền tối thiểu, WAF, S3 private, TLS 1.2+, không dùng wildcard |
| Độ tin cậy | ✅ DLQ, retry logic, PITR, idempotency, visibility timeout theo best practice SQS |
| Hiệu năng | ✅ ARM64, Node.js 22, esbuild, PAY_PER_REQUEST, CloudFront caching |
| Tối ưu chi phí | ✅ Zero idle cost, không có tài nguyên được cấp phát dư thừa, chính sách lưu trữ log |
| Bền vững | ✅ ARM64 tiết kiệm năng lượng, caching giảm tính toán, scale-to-zero |