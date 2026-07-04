---
title: "Verify & Test Everything"
date: 2026-07-04
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Verify & Test Everything

Verify every deployed service and test all customer-facing flows end-to-end.

---

### 5.5.1 Acquire a JWT Token

All authenticated API tests require a Cognito JWT. Run this once and reuse `$TOKEN` throughout.

> **Important:** Cognito ID Tokens expire after approximately **one hour**. If verification takes longer than one hour, re-run this command to get a fresh token before continuing.

> Replace `<your-user-pool-client-id>` with the `AuthStack.UserPoolClientId` value from the outputs in step 5.2.1.

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

### 5.5.2 Verify CloudFront

> Replace `dXXXXXXXXXXXXXX.cloudfront.net` with your `FrontendStack.CloudFrontDomainName` output from step 5.3.2.
> On **Linux/macOS** use `python3`. On **Windows** use `python`.

```bash
CF="https://dXXXXXXXXXXXXXX.cloudfront.net"

# Homepage returns 200
curl -o /dev/null -s -w "%{http_code}\n" "$CF"
# Expected: 200

# Security headers are present
curl -sI "$CF" | grep -iE "x-frame|strict-transport|x-content-type"
# Expected:
# x-frame-options: SAMEORIGIN
# strict-transport-security: max-age=31536000; includeSubDomains
# x-content-type-options: nosniff

# SPA routing — any deep path returns 200 (not 404)
curl -o /dev/null -s -w "%{http_code}\n" "$CF/orders/some-nonexistent-id"
# Expected: 200

# Runtime config is correct
curl -s "$CF/config.json" | python3 -m json.tool | grep -E "apiUrl|userPoolId"
# Expected:
# "apiUrl": "https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod/",
# "userPoolId": "ap-southeast-1_XXXXXXXXX",

# Static assets are long-cached
curl -sI "$CF/assets/index-XXXXXXXX.js" | grep cache-control
# Expected: max-age=31536000
```

---

### 5.5.3 Verify DynamoDB

```bash
# Table is ACTIVE
aws dynamodb describe-table \
  --table-name EcommerceTable \
  --region ap-southeast-1 \
  --query "Table.TableStatus" --output text
# Expected: ACTIVE

# 12 products exist via GSI3
aws dynamodb query \
  --table-name EcommerceTable \
  --index-name GSI3 \
  --key-condition-expression "GSI3PK = :pk" \
  --expression-attribute-values '{":pk":{"S":"PRODUCT"}}' \
  --select COUNT \
  --region ap-southeast-1 \
  --query "Count"
# Expected: 12

# Category filter via GSI1 works
aws dynamodb query \
  --table-name EcommerceTable \
  --index-name GSI1 \
  --key-condition-expression "GSI1PK = :pk" \
  --expression-attribute-values '{":pk":{"S":"CATEGORY#gaming"}}' \
  --select COUNT \
  --region ap-southeast-1 \
  --query "Count"
# Expected: 2

# PITR is enabled
aws dynamodb describe-continuous-backups \
  --table-name EcommerceTable \
  --region ap-southeast-1 \
  --query "ContinuousBackupsDescription.PointInTimeRecoveryDescription.PointInTimeRecoveryStatus" \
  --output text
# Expected: ENABLED
```

---

### 5.5.4 Verify EventBridge

```bash
# Custom bus exists
aws events describe-event-bus \
  --name EcommerceEventBus \
  --region ap-southeast-1 \
  --query "Name" --output text
# Expected: EcommerceEventBus

# OrderCreated rule is ENABLED and targets SQS
aws events list-targets-by-rule \
  --rule EcommerceOrderCreatedRule \
  --event-bus-name EcommerceEventBus \
  --region ap-southeast-1 \
  --query "Targets[0].Arn" --output text
# Expected: arn:aws:sqs:ap-southeast-1:...:EcommerceOrderQueue
```

---

### 5.5.5 Verify SQS

```bash
# OrderQueue visibility timeout = 180s (6x Lambda timeout)
aws sqs get-queue-attributes \
  --queue-url $(aws sqs get-queue-url \
    --queue-name EcommerceOrderQueue \
    --region ap-southeast-1 \
    --query QueueUrl --output text) \
  --attribute-names VisibilityTimeout \
  --region ap-southeast-1 \
  --query "Attributes.VisibilityTimeout" --output text
# Expected: 180

# Lambda trigger is ENABLED with batchSize=1
aws lambda list-event-source-mappings \
  --function-name OrderProcessorFunction \
  --region ap-southeast-1 \
  --query "EventSourceMappings[0].{State:State,BatchSize:BatchSize}"
# Expected: {"State":"Enabled","BatchSize":1}

# DLQ is empty
aws sqs get-queue-attributes \
  --queue-url $(aws sqs get-queue-url \
    --queue-name EcommerceOrderDLQ \
    --region ap-southeast-1 \
    --query QueueUrl --output text) \
  --attribute-names ApproximateNumberOfMessages \
  --region ap-southeast-1 \
  --query "Attributes.ApproximateNumberOfMessages" --output text
# Expected: 0
```

---

### 5.5.6 Verify SNS Alarm

```bash
# Trigger an alarm manually
aws cloudwatch set-alarm-state \
  --alarm-name EcommerceOrderDLQMessages \
  --state-value ALARM \
  --state-reason "Workshop verification test" \
  --region ap-southeast-1

# Wait ~60 seconds — check your inbox for alarm email
# Subject: ALARM: "EcommerceOrderDLQMessages" in Asia Pacific (Singapore)

# Reset the alarm
aws cloudwatch set-alarm-state \
  --alarm-name EcommerceOrderDLQMessages \
  --state-value OK \
  --state-reason "Workshop verification test — resetting" \
  --region ap-southeast-1

# Verify all 6 alarms are OK
aws cloudwatch describe-alarms \
  --region ap-southeast-1 \
  --query "MetricAlarms[?starts_with(AlarmName,'Ecommerce')].{Alarm:AlarmName,State:StateValue}" \
  --output table
```

---

### 5.5.7 Verify All Lambda Functions

```bash
for fn in ProductServiceFunction CartServiceFunction OrderServiceFunction OrderProcessorFunction; do
  echo "--- $fn ---"
  aws lambda get-function-configuration \
    --function-name $fn \
    --region ap-southeast-1 \
    --query "{Runtime:Runtime,Arch:Architectures[0],Memory:MemorySize,Tracing:TracingConfig.Mode,State:State}"
done
```

Expected for all:
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

### 5.5.8 Test Product Browsing (Public)

> Replace `xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com` with your `ApiStack.ApiUrl` output from step 5.2.4.
> On **Linux/macOS** use `python3`. On **Windows** use `python`.

```bash
API="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"

# List all products
curl -s "$API/products" | python3 -m json.tool | grep '"count"'
# Expected: "count": 12

# Filter by category
curl -s "$API/products?category=laptops" | python3 -m json.tool | grep '"count"'
# Expected: "count": 3

# Search by keyword
curl -s "$API/products?search=headphones" | python3 -m json.tool | grep '"name"'
# Expected: "name": "SoundMax ANC Headphones",

# Sort by price ascending
curl -s "$API/products?sort=price_asc" | python3 -m json.tool | grep '"price"' | head -3
# Expected: lowest price appears first

# Get product by ID
curl -s "$API/products/prod-laptop-001" | python3 -m json.tool | grep -E '"name"|"price"'
# Expected:
# "name": "ProBook X15 Laptop",
# "price": 1299.99,

# Get product by slug
curl -s "$API/products/probook-x15-laptop" | python3 -m json.tool | grep '"productId"'
# Expected: "productId": "prod-laptop-001",
```

---

### 5.5.9 Test Cart Flow (Authenticated)

> On **Linux/macOS** use `python3`. On **Windows** use `python`.

```bash
API="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"

# Empty cart
curl -s -H "Authorization: $TOKEN" "$API/cart" | python3 -m json.tool
# Expected: {"items":[],"count":0}

# Add item
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"productId":"prod-laptop-001","quantity":1,"price":1299.99}' \
  "$API/cart" | python3 -m json.tool | grep -E '"productId"|"quantity"'
# Expected: "productId":"prod-laptop-001", "quantity":1

# Add same item again — quantity increments (DynamoDB ADD)
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"productId":"prod-laptop-001","quantity":1,"price":1299.99}' \
  "$API/cart" | python3 -m json.tool | grep '"quantity"'
# Expected: "quantity": 2

# Update quantity
curl -s -X PUT \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"productId":"prod-laptop-001","quantity":3}' \
  "$API/cart" | python3 -m json.tool | grep '"quantity"'
# Expected: "quantity": 3

# Remove item
curl -s -X DELETE \
  -H "Authorization: $TOKEN" \
  "$API/cart/prod-laptop-001" | python3 -m json.tool
# Expected: {"message":"Item removed from cart"}

# Cart is empty again
curl -s -H "Authorization: $TOKEN" "$API/cart" | python3 -m json.tool
# Expected: {"items":[],"count":0}
```

---

### 5.5.10 Test Order Processing (Full E2E)

This test verifies the complete event-driven pipeline: API → EventBridge → SQS → Lambda → DynamoDB.

> On **Linux/macOS** use `python3`. On **Windows** use `python`.

```bash
API="https://xxxxxxxxxx.execute-api.ap-southeast-1.amazonaws.com/prod"

# Place an order
ORDER=$(curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "items": [{"productId":"prod-phone-001","quantity":1,"price":799.99}],
    "shippingAddress": "123 AWS Way, Singapore 123456"
  }' \
  "$API/orders")

echo $ORDER | python3 -m json.tool
# Expected:
# {
#   "message": "Order accepted for processing",
#   "orderId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
#   "status": "PENDING"
# }

# Extract orderId
ORDER_ID=$(echo $ORDER | python3 -c "import sys,json; print(json.load(sys.stdin)['orderId'])")
echo "Order ID: $ORDER_ID"

# Poll for COMPLETED status (EventBridge → SQS → Lambda processes in ~10 seconds)
for i in $(seq 1 15); do
  STATUS=$(curl -s -H "Authorization: $TOKEN" "$API/orders/$ORDER_ID" \
    | python3 -c "import sys,json; print(json.load(sys.stdin).get('status','unknown'))")
  echo "Attempt $i: $STATUS"
  if [ "$STATUS" = "COMPLETED" ]; then
    echo "✅ Order processing complete"
    break
  fi
  sleep 3
done
# Expected: reaches COMPLETED within ~10–15 seconds

# Verify directly in DynamoDB (status stored as COMPLETED in uppercase)
aws dynamodb get-item \
  --table-name EcommerceTable \
  --region ap-southeast-1 \
  --key "{\"PK\":{\"S\":\"ORDER#$ORDER_ID\"},\"SK\":{\"S\":\"METADATA\"}}" \
  --query "Item.{status:status.S,total:totalAmount.N}"
# Expected: {"status":"COMPLETED","total":"799.99"}

# DLQ still empty after processing
aws sqs get-queue-attributes \
  --queue-url $(aws sqs get-queue-url \
    --queue-name EcommerceOrderDLQ \
    --region ap-southeast-1 \
    --query QueueUrl --output text) \
  --attribute-names ApproximateNumberOfMessages \
  --region ap-southeast-1 \
  --query "Attributes.ApproximateNumberOfMessages" --output text
# Expected: 0
```

---

### 5.5.11 Test Order Ownership (Security)

```bash
# Get admin token
# Replace <your-user-pool-client-id> with AuthStack.UserPoolClientId from step 5.2.1
ADMIN_TOKEN=$(aws cognito-idp initiate-auth \
  --auth-flow USER_PASSWORD_AUTH \
  --client-id <your-user-pool-client-id> \
  --auth-parameters USERNAME=admin@demo.com,PASSWORD=Admin@Pass2024! \
  --region ap-southeast-1 \
  --query "AuthenticationResult.IdToken" \
  --output text)

# Try to access customer's order with admin token — must return 404
curl -s \
  -H "Authorization: $ADMIN_TOKEN" \
  "$API/orders/$ORDER_ID" | python3 -m json.tool
# Expected: {"error":"Order not found"}
# Returns 404 to avoid leaking whether the order exists
```

---

### 5.5.12 Test Input Validation

```bash
# Missing items
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"shippingAddress":"123 Test"}' \
  "$API/orders"
# Expected: {"error":"items array is required and must not be empty"}

# Negative price
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"items":[{"productId":"prod-laptop-001","quantity":1,"price":-10}],"shippingAddress":"123 Test"}' \
  "$API/orders"
# Expected: {"error":"items[0].price must be a non-negative number"}

# Zero quantity
curl -s -X POST \
  -H "Authorization: $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"items":[{"productId":"prod-laptop-001","quantity":0,"price":100}],"shippingAddress":"123 Test"}' \
  "$API/orders"
# Expected: {"error":"items[0].quantity must be a positive integer"}
```

---

### 5.5.13 Test in the Browser

Open your `FrontendStack.FrontendUrl` (e.g. `https://dXXXXXXXXXXXXXX.cloudfront.net`) in your browser and verify:

| Feature | Expected |
|---------|---------|
| Homepage loads | 12 product cards visible |
| Category filter | Clicking "Laptops" shows 3 products |
| Search bar | Typing "headphones" shows 1 result |
| Login with `customer@demo.com` | Redirects to homepage; header shows name + My Orders link |
| Add to cart | Cart badge shows item count |
| Checkout form | Fills shipping details, places order |
| Order detail page | Status transitions Pending → Processing → Delivered within ~15 seconds |
| My Orders page | Shows placed orders with status badges |
| Logout | Header reverts to Login/Register |
| `/orders` without login | Redirects to `/login` |

---

### Troubleshooting

| Problem | Solution |
|---------|---------|
| `{"message":"Unauthorized"}` | JWT expired; re-acquire token from step 5.5.1 |
| `{"message":"Internal Server Error"}` | Check CloudWatch Logs: `aws logs tail /aws/lambda/OrderServiceFunction --region ap-southeast-1 --since 10m` |
| Order status stays at `Pending` | Check DLQ count; check `/aws/lambda/OrderProcessorFunction` logs |
| Browser shows blank page | Open DevTools (F12) and check console errors; likely a `config.json` issue |
| CORS error in browser | Redo step 5.3.4 — `ALLOWED_ORIGIN` not set correctly |
