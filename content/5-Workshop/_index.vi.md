---
title: "Workshop"
date: 2025-09-09
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
## Tổng quan
Amazon Bedrock cung cấp khả năng tích hợp các foundation models (LLMs) hàng đầu từ Anthropic, Meta, AI21 Labs và các nhà cung cấp khác thông qua API đơn giản, cho phép bạn xây dựng ứng dụng AI mà không cần quản lý infrastructure phức tạp.

Trong workshop này, chúng ta sẽ học cách xây dựng, triển khai, và kiểm tra một AI Chatbot hoàn chỉnh sử dụng kiến trúc serverless để cho phép người dùng tương tác với Claude Haiku 4.5 mà không cần quản lý servers hay lo lắng về scaling.

Chúng ta sẽ tạo một hệ thống gồm 5 thành phần chính để xây dựng chatbot: Amazon Bedrock (AI engine), AWS Lambda (backend logic), API Gateway (REST API endpoint), Amazon S3 (frontend hosting), và CloudWatch (monitoring). Các thành phần này mang đến kiến trúc serverless hoàn chỉnh với chi phí thấp và khả năng tự động scale.

#### Các Thành Phần Chính:

**Amazon Bedrock (AI Engine)** - Cung cấp Claude Haiku 4.5 model thông qua API đơn giản. Bạn gọi InvokeModel API để gửi tin nhắn và nhận phản hồi AI thông minh.

**AWS Lambda (Backend Logic)** - Chạy Node.js 24 code để xử lý requests từ API Gateway. Lambda validate input (message length, history limits), format prompts cho Bedrock, gọi Bedrock API, và xử lý errors.

**API Gateway (REST API Endpoint)** - Tạo public HTTPS endpoint (POST /chat) để frontend có thể gọi. API Gateway handle CORS configuration, route requests đến Lambda, và cung cấp throttling để bảo vệ backend khỏi abuse.

**Amazon S3 (Frontend Hosting)** - Host static website (HTML) cho chatbot UI. Users truy cập chatbot qua browser, giao diện gửi messages đến API Gateway, và hiển thị responses từ AI.

**CloudWatch (Monitoring & Debugging)** - Tự động collect logs từ Lambda execution, cho phép bạn debug errors.

### Kiến Trúc Tổng Quan
User Browser → S3 (Static Website) → API Gateway → Lambda → Bedrock (Claude) → CloudWatch

Flow hoạt động:
- User nhập message vào chatbot UI (hosted trên S3)
- JavaScript gửi POST request đến API Gateway endpoint
- API Gateway invoke Lambda function
- Lambda validate input, format prompt, gọi Bedrock InvokeModel API
- Bedrock xử lý với Claude Haiku 4.5, trả về AI response
- Lambda trả response về API Gateway → Browser
- CloudWatch ghi logs toàn bộ quá trình

#### Nội dung Workshop

1. [Tổng quan Workshop](5.1-Workshop-overview/)
2. [Yêu cầu chuẩn bị](5.2-Prerequiste/)
3. [Thiết lập Amazon Bedrock](5.3-Setup-Amazon-Bedrock/)
4. [Thiết lập Lambda Function](5.4-Setup_Lambda/)
5. [Thiết lập API Gateway](5.5-Setup-API-gateway/)
6. [Giám sát với CloudWatch](5.6-Monitoring-CloudWatch/)
7. [Thiết lập S3 Static Website](5.7-Setup-S3/)

