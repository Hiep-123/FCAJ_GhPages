---
title: "Xác minh & Kiểm thử"
date: 2026-07-04
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Xác minh & Kiểm thử toàn bộ

Xác minh từng dịch vụ đã triển khai và kiểm thử tất cả các luồng khách hàng từ đầu đến cuối.

---

### 5.5.1 Lấy JWT Token

Tất cả API test cần xác thực đều yêu cầu JWT Cognito. Chạy một lần và tái sử dụng `$TOKEN` trong suốt quá trình test.

> **Quan trọng:** Cognito ID Token hết hạn sau khoảng **một giờ**. Nếu quá trình xác minh mất hơn một giờ, hãy chạy lại lệnh này để lấy token mới trước khi tiếp tục.

> Thay `<your-user-pool-client-id>` bằng giá trị `AuthStack.UserPoolClientId` từ outputs ở bước 5.2.1.

```bash
TOKEN=$(aws cognito-idp initiate-auth \
  --auth-flow USER_PASSWORD_AUTH \
  --client-id <your-user-pool-client-id> \
  --auth-parameters USERNAME=customer@demo.com,PASSWORD=Demo@Pass2024! \
  --region ap-southeast-1 \
  --query "AuthenticationResult.IdToken" \
  --output text)

echo "Token acquired: ${TOKEN:0:60}..."
```

---

### 5.5.2 Xác minh CloudFront

```bash
CF="https://dXXXXXXXXXXXXXX.cloudfront.net"

# Homepage trả về 200
curl -o /dev/null -s -w "%{http_code}\n" "$CF"
# Kết quả mong đợi: 200

# Security headers có mặt
curl -sI "$CF" | grep -iE "x-frame|strict-transport|x-content-type"
# Kết quả mong đợi:
# x-frame-options: SAMEORIGIN
# strict-transport-security: max-age=31536000; includeSubDomains
# x-content-type-options: nosniff

# SPA routing — đường dẫn bất kỳ trả về 200 (không phải 404)
curl -o /dev/null -s -w "%{http_code}\n" "$CF/orders/some-nonexistent-id"
# Kết quả mong đợi: 200

# Runtime config đúng
curl -s "$CF/config.json" | python3 -m json.tool | grep -E "apiUrl|userPoolId"
# Kết quả mong đợi:
# "apiUrl": "https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod/",
# "userPoolId": "ap-southeast-1_XXXXXXXXX",

# Static asset được cache dài hạn
curl -sI "$CF/assets/index-XXXXXXXX.js" | grep cache-control
# Kết quả mong đợi: max-age=31536000
```

---

### 5.5.3 Xác minh DynamoDB

```bash
# Bảng đang ACTIVE
aws dynamodb describe-table \
  --table-name EcommerceTable \
  --region ap-southeast-1 \
  --query "Table.TableStatus" --output text
# Kết quả mong đợi: ACTIVE

# 12 sản phẩm tồn tại qua GSI3
aws dynamodb query \
  --table-name EcommerceTable \
  --index-name GSI3 \
  --key-condition-expression "GSI3PK = :pk" \
  --expression-attribute-values '{":pk":{"S":"PRODUCT"}}' \
  --select COUNT \
  --region ap-southeast-1 \
  --query "Count"
# Kết quả mong đợi: 12

# Lọc theo danh mục qua GSI1
aws dynamodb query \
  --table-name EcommerceTable \
  --index-name GSI1 \
  --key-condition-expression "GSI1PK = :pk" \
  --expression-attribute-values '{":pk":{"S":"CATEGORY#gaming"}}' \
  --select COUNT \
  --region ap-southeast-1 \
  --query "Count"
# Kết quả mong đợi: 2

# PITR đã được bật
aws dynamodb describe-continuous-backups \
  --table-name EcommerceTable \
  --region ap-southeast-1 \
  --query "ContinuousBackupsDescription.PointInTimeRecoveryDescription.PointInTimeRecoveryStatus" \
  --output text
# Kết quả mong đợi: ENABLED
```

---

### 5.5.4 Xác minh EventBridge

```bash
# Custom bus tồn tại
aws events describe-event-bus \
  --name EcommerceEventBus \
  --region ap-southeast-1 \
  --query "Name" --output text
# Kết quả mong đợi: EcommerceEventBus

# Rule OrderCreated ENABLED và nhắm tới SQS
aws events list-targets-by-rule \
  --rule EcommerceOrderCreatedRule \
  --event-bus-name EcommerceEventBus \
  --region ap-southeast-1 \
  --query "Targets[0].Arn" --output text
# Kết quả mong đợi: arn:aws:sqs:ap-southeast-1:...:EcommerceOrderQueue
```

---

### 5.5.5 Xác minh SQS

```bash
# Visibility timeout OrderQueue = 180s (6 lần Lambda timeout)
aws sqs get-queue-attributes \
  --queue-url $(aws sqs get-queue-url \
    --queue-name EcommerceOrderQueue \
    --region ap-southeast-1 \
    --query QueueUrl --output text) \
  --attribute-names VisibilityTimeout \
  --region ap-southeast-1 \
  --query "Attributes.VisibilityTimeout" --output text
# Kết quả mong đợi: 180

# Lambda trigger ENABLED với batchSize=1
aws lambda list-event-source-mappings \
  --function-name OrderProcessorFunction \
  --region ap-southeast-1 \
  --query "EventSourceMappings[0].{State:State,BatchSize:BatchSize}"
# Kết quả mong đợi: {"State":"Enabled","BatchSize":1}

# DLQ trống
aws sqs get-queue-attributes \
  --queue-url $(aws sqs get-queue-url \
    --queue-name EcommerceOrderDLQ \
    --region ap-southeast-1 \
    --query QueueUrl --output text) \
  --attribute-names ApproximateNumberOfMessages \
  --region ap-southeast-1 \
  --query "Attributes.ApproximateNumberOfMessages" --output text
# Kết quả mong đợi: 0
```

---

### 5.5.6 Xác minh SNS Alarm

```bash
# Kích hoạt alarm thủ công
aws cloudwatch set-alarm-state \
  --alarm-name EcommerceOrderDLQMessages \
  --state-value ALARM \
  --state-reason "Kiểm tra xác minh workshop" \
  --region ap-southeast-1

# Đợi ~60 giây — kiểm tra hộp thư đến email alarm
# Tiêu đề: ALARM: "EcommerceOrderDLQMessages" in Asia Pacific (Singapore)

# Reset alarm
aws cloudwatch set-alarm-state \
  --alarm-name EcommerceOrderDLQMessages \
  --state-value OK \
  --state-reason "Kiểm tra xác minh workshop — đặt lại" \
  --region ap-southeast-1

# Xác minh 6 alarm tất cả OK
aws cloudwatch describe-alarms \
  --region ap-southeast-1 \
  --query "MetricAlarms[?starts_with(AlarmName,'Ecommerce')].{Alarm:AlarmName,State:StateValue}" \
  --output table
```

---

### 5.5.7 Xác minh tất cả Lambda Function

```bash
for fn in ProductServiceFunction CartServiceFunction OrderServiceFunction OrderProcessorFunction; do
  echo "--- $fn ---"
  aws lambda get-function-configuration \
    --function-name $fn \
    --region ap-southeast-1 \
    --query "{Runtime:Runtime,Arch:Architectures[0],Memory:MemorySize,Tracing:TracingConfig.Mode,State:State}"
done
```

Kết quả mong đợi cho tất cả:
```json
{
    "Runtime": "nodejs22.x",
    "Arch": "arm64",
    "Memory": 512,
    "Tracing": "Active",
    "State": "Active"
}
```

---

### 5.5.8 Kiểm thử duyệt sản phẩm (Public)

```bash
API="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"

# Liệt kê tất cả sản phẩm
curl -s "$API/products" | python3 -m json.tool | grep '"count"'
# Kết quả mong đợi: "count": 12

# Lọc theo danh mục
curl -s "$API/products?category=laptops" | python3 -m json.tool | grep '"count"'
# Kết quả mong đợi: "count": 3

# Tìm kiếm theo từ khóa
curl -s "$API/products?search=headphones" | python3 -m json.tool | grep '"name"'
# Kết quả mong đợi: "name": "SoundMax ANC Headphones",

# Sắp xếp theo giá tăng dần
curl -s "$API/products?sort=price_asc" | python3 -m json.tool | grep '"price"' | head -3
# Kết quả mong đợi: giá thấp nhất xuất hiện đầu tiên

# Lấy sản phẩm theo ID
curl -s "$API/products/prod-laptop-001" | python3 -m json.tool | grep -E '"name"|"price"'
# Kết quả mong đợi:
# "name": "ProBook X15 Laptop",
# "price": 1299.99,

# Lấy sản phẩm theo slug
curl -s "$API/products/probook-x15-laptop" | python3 -m json.tool | grep '"productId"'
# Kết quả mong đợi: "productId": "prod-laptop-001",
```

---

### 5.5.9 Kiểm thử luồng giỏ hàng (Có xác thực)

```bash
API="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"

# Giỏ hàng trống
curl -s -H "Authorization: $TOKEN" "$API/cart" | python3 -m json.tool
# Kết quả mong đợi: {"items":[],"count":0}

# Thêm sản phẩm
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"productId":"prod-laptop-001","quantity":1,"price":1299.99}' \
  "$API/cart" | python3 -m json.tool | grep -E '"productId"|"quantity"'
# Kết quả mong đợi: "productId":"prod-laptop-001", "quantity":1

# Thêm cùng sản phẩm — số lượng tăng (DynamoDB ADD)
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"productId":"prod-laptop-001","quantity":1,"price":1299.99}' \
  "$API/cart" | python3 -m json.tool | grep '"quantity"'
# Kết quả mong đợi: "quantity": 2

# Cập nhật số lượng
curl -s -X PUT \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"productId":"prod-laptop-001","quantity":3}' \
  "$API/cart" | python3 -m json.tool | grep '"quantity"'
# Kết quả mong đợi: "quantity": 3

# Xóa sản phẩm
curl -s -X DELETE \
  -H "Authorization: $TOKEN" \
  "$API/cart/prod-laptop-001" | python3 -m json.tool
# Kết quả mong đợi: {"message":"Item removed from cart"}

# Giỏ hàng trống trở lại
curl -s -H "Authorization: $TOKEN" "$API/cart" | python3 -m json.tool
# Kết quả mong đợi: {"items":[],"count":0}
```

---

### 5.5.10 Kiểm thử xử lý đơn hàng (E2E hoàn chỉnh)

Kiểm thử này xác minh toàn bộ pipeline event-driven: API → EventBridge → SQS → Lambda → DynamoDB.

```bash
API="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"

# Đặt đơn hàng
ORDER=$(curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "items": [{"productId":"prod-phone-001","quantity":1,"price":799.99}],
    "shippingAddress": "123 AWS Way, Singapore 123456"
  }' \
  "$API/orders")

echo $ORDER | python3 -m json.tool
# Kết quả mong đợi:
# {
#   "message": "Order accepted for processing",
#   "orderId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
#   "status": "PENDING"
# }

# Lấy orderId
ORDER_ID=$(echo $ORDER | python3 -c "import sys,json; print(json.load(sys.stdin)['orderId'])")
echo "Order ID: $ORDER_ID"

# Poll cho đến khi COMPLETED (EventBridge → SQS → Lambda xử lý trong ~10 giây)
for i in $(seq 1 15); do
  STATUS=$(curl -s -H "Authorization: $TOKEN" "$API/orders/$ORDER_ID" \
    | python3 -c "import sys,json; print(json.load(sys.stdin).get('status','unknown'))")
  echo "Lần $i: $STATUS"
  if [ "$STATUS" = "COMPLETED" ]; then
    echo "✅ Xử lý đơn hàng hoàn thành"
    break
  fi
  sleep 3
done
# Kết quả mong đợi: đạt COMPLETED trong ~10–15 giây

# Xác minh trực tiếp trong DynamoDB
aws dynamodb get-item \
  --table-name EcommerceTable \
  --region ap-southeast-1 \
  --key "{\"PK\":{\"S\":\"ORDER#$ORDER_ID\"},\"SK\":{\"S\":\"METADATA\"}}" \
  --query "Item.{status:status.S,total:totalAmount.N}"
# Kết quả mong đợi: {"status":"COMPLETED","total":"799.99"}

# DLQ vẫn trống sau khi xử lý
aws sqs get-queue-attributes \
  --queue-url $(aws sqs get-queue-url \
    --queue-name EcommerceOrderDLQ \
    --region ap-southeast-1 \
    --query QueueUrl --output text) \
  --attribute-names ApproximateNumberOfMessages \
  --region ap-southeast-1 \
  --query "Attributes.ApproximateNumberOfMessages" --output text
# Kết quả mong đợi: 0
```

---

### 5.5.11 Kiểm thử quyền sở hữu đơn hàng (Bảo mật)

```bash
# Lấy token admin
ADMIN_TOKEN=$(aws cognito-idp initiate-auth \
  --auth-flow USER_PASSWORD_AUTH \
  --client-id <your-user-pool-client-id> \
  --auth-parameters USERNAME=admin@demo.com,PASSWORD=Admin@Pass2024! \
  --region ap-southeast-1 \
  --query "AuthenticationResult.IdToken" \
  --output text)

# Truy cập đơn hàng của customer bằng token admin — phải trả về 404
curl -s \
  -H "Authorization: $ADMIN_TOKEN" \
  "$API/orders/$ORDER_ID" | python3 -m json.tool
# Kết quả mong đợi: {"error":"Order not found"}
# Trả về 404 để tránh lộ thông tin về sự tồn tại của đơn hàng
```

---

### 5.5.12 Kiểm thử xác thực đầu vào

```bash
# Thiếu mảng items
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"shippingAddress":"123 Test"}' \
  "$API/orders"
# Kết quả mong đợi: {"error":"items array is required and must not be empty"}

# Giá âm
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"items":[{"productId":"prod-laptop-001","quantity":1,"price":-10}],"shippingAddress":"123 Test"}' \
  "$API/orders"
# Kết quả mong đợi: {"error":"items[0].price must be a non-negative number"}

# Số lượng bằng 0
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"items":[{"productId":"prod-laptop-001","quantity":0,"price":100}],"shippingAddress":"123 Test"}' \
  "$API/orders"
# Kết quả mong đợi: {"error":"items[0].quantity must be a positive integer"}
```

---

### 5.5.13 Kiểm thử trên trình duyệt

Mở `https://dXXXXXXXXXXXXXX.cloudfront.net` trong trình duyệt và xác minh:

| Tính năng | Kết quả mong đợi |
|-----------|-----------------|
| Trang chủ tải | 12 thẻ sản phẩm hiển thị |
| Lọc danh mục | Click "Laptops" hiển thị 3 sản phẩm |
| Thanh tìm kiếm | Gõ "headphones" hiển thị 1 kết quả |
| Đăng nhập với `customer@demo.com` | Chuyển về trang chủ; header hiển thị tên + link My Orders |
| Thêm vào giỏ hàng | Badge giỏ hàng hiển thị số lượng |
| Form thanh toán | Điền địa chỉ giao hàng, đặt đơn hàng |
| Trang chi tiết đơn hàng | Trạng thái chuyển Pending → Processing → Delivered trong ~15 giây |
| Trang My Orders | Hiển thị các đơn đã đặt với badge trạng thái |
| Đăng xuất | Header trở về Login/Register |
| `/orders` khi chưa đăng nhập | Chuyển hướng về `/login` |

---

### Xử lý lỗi thường gặp

| Lỗi | Giải pháp |
|-----|----------|
| `{"message":"Unauthorized"}` | JWT hết hạn; lấy lại token từ bước 5.5.1 |
| `{"message":"Internal Server Error"}` | Kiểm tra CloudWatch Logs: `aws logs tail /aws/lambda/OrderServiceFunction --region ap-southeast-1 --since 10m` |
| Trạng thái đơn hàng không chuyển từ `Pending` | Kiểm tra số tin nhắn DLQ; kiểm tra logs `/aws/lambda/OrderProcessorFunction` |
| Trình duyệt hiển thị trang trắng | Mở DevTools (F12) kiểm tra lỗi console; khả năng cao là vấn đề `config.json` |
| Lỗi CORS trong trình duyệt | Làm lại bước 5.3.4 — `ALLOWED_ORIGIN` chưa được đặt đúng |
