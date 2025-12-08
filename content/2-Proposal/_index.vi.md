---
title: "Proposal"
date: 2025-11-11
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# AWS First Cloud AI Journey – Kế hoạch Dự án Thương mại Điện tử Leaf

## 1. Bối cảnh và động lực

## 1.1 Tóm tắt điều hành
Leaf là một nền tảng thương mại điện tử chuyên về các sản phẩm thời trang nam nữ, bao gồm các phụ kiện thời trang như trang sức, giày dép, mũ và dây da. Website tích hợp các dịch vụ AWS để tối ưu hóa chi phí và nâng cao trải nghiệm người dùng.

## 1.2 Tiêu chí thành công của dự án
- Nền tảng thương mại điện tử hoạt động đầy đủ với tích hợp AWS.
- Tối ưu hóa chi phí và hiệu suất sử dụng kiến trúc serverless.
- Tốc độ tải trang nhanh với CDN (CloudFront) và S3 hosting.
- Thông báo liền mạch sử dụng SNS/SES.
- Hỗ trợ dịch thuật và trợ lý AI (tùy chọn) qua Amazon Translate & Bedrock.

## 1.3 Các giả định
- Khách hàng có kiến thức cơ bản về dịch vụ đám mây và tài khoản AWS.
- Chấp nhận phương pháp serverless; không yêu cầu máy chủ riêng.
- Lưu lượng truy cập ở mức vừa phải (~vài nghìn người dùng/tháng) và chi phí dự kiến thấp.
- Các dịch vụ cần thiết (S3, Lambda, DynamoDB, v.v.) có thể truy cập được ở các khu vực AWS đã chọn.
- Hình ảnh và tài nguyên tĩnh sẽ được lưu trữ trong S3/CDN để tối ưu hiệu suất.

---

# 2. KIẾN TRÚC GIẢI PHÁP / SƠ ĐỒ KIẾN TRÚC

## 2.1 Sơ đồ kiến trúc kỹ thuật
Nền tảng áp dụng **kiến trúc AWS Serverless** để quản lý dữ liệu.  
![](https://paperkite-master.github.io/AWS_FCJ/images/2-Proposal/AWS1.drawio.png)

### Các thành phần và vai trò trong kiến trúc AWS

#### A. Lớp giao diện người dùng
| Dịch vụ | Vai trò | Mô tả chi tiết |
|---------|---------|----------------|
| **AWS Amplify** | Triển khai website | Lưu trữ **website tĩnh** (React, Vue, Next.js) và **tự động xây dựng/triển khai** khi đẩy code lên GitHub. |
| **Amazon CloudFront (CDN)** | Cải thiện tốc độ tải trang | Lưu cache nội dung tĩnh gần người dùng để giảm độ trễ. |
| **Amazon S3** | Lưu trữ file tĩnh & hình ảnh sản phẩm | Hoạt động như kho lưu trữ nội dung cho hình ảnh, banner, file CSS/JS. |

#### B. Lớp logic ứng dụng
| Dịch vụ | Vai trò | Mô tả chi tiết |
|---------|---------|----------------|
| **Amazon API Gateway** | Cổng API | Nhận yêu cầu từ frontend và chuyển tiếp đến các hàm Lambda để xử lý. |
| **AWS Lambda** | Logic phía server | Xử lý đơn hàng, thanh toán, xác thực, email mà không cần máy chủ riêng. |
| **Amazon DynamoDB** | Cơ sở dữ liệu NoSQL | Lưu trữ sản phẩm, tài khoản, đơn hàng, giỏ hàng. |
| **AWS Secrets Manager** | Bảo mật dữ liệu nhạy cảm | Lưu trữ khóa API, token thanh toán, mật khẩu cơ sở dữ liệu. |

#### C. Lớp quản lý người dùng & bảo mật
| Dịch vụ | Vai trò | Mô tả chi tiết |
|---------|---------|----------------|
| **AWS WAF** | Bảo vệ web | Chống lại SQL Injection, XSS, DDoS. |
| **Amazon Route 53** | DNS & tên miền | Quản lý tên miền. |

#### D. Lớp thông báo & giao tiếp
| Dịch vụ | Vai trò | Mô tả chi tiết |
|---------|---------|----------------|
| **Amazon SNS** | Thông báo hệ thống | Gửi thông báo cho quản trị viên hoặc người dùng. |
| **Amazon SES** | Email giao dịch | Gửi xác nhận đơn hàng, khuyến mãi, email đặt lại mật khẩu. |

#### E. Lớp AI & học máy
| Dịch vụ | Vai trò | Mô tả chi tiết |
|---------|---------|----------------|
| **Amazon Translate** | Dịch nội dung | Dịch mô tả sản phẩm sang các ngôn ngữ khác. |
| **Amazon Bedrock** | Tạo nội dung AI | Tạo chatbot hỗ trợ mua sắm. |

#### F. Lớp giám sát & quản trị
| Dịch vụ | Vai trò | Mô tả chi tiết |
|---------|---------|----------------|
| **Amazon CloudWatch** | Giám sát hệ thống | Theo dõi log, hiệu suất, cảnh báo lỗi hoặc tăng chi phí. |
| **AWS CloudTrail** | Ghi log quản trị | Theo dõi các thay đổi cấu hình để kiểm toán. |

## 2.2 Kế hoạch kỹ thuật
- Thu thập yêu cầu hệ thống và các tính năng.  
- Ước tính chi phí và kiểm tra tính khả thi.  
- Thiết kế giao diện mẫu bằng Figma.  
- Xây dựng schema cơ sở dữ liệu và API backend.  
- Phát triển giao diện frontend.  
- Tích hợp các dịch vụ AWS (S3, Lambda, DynamoDB,  v.v.).  
- Kiểm thử và triển khai hệ thống sử dụng kiến trúc serverless.

## 2.3 Kế hoạch dự án
- Khung làm việc Agile Scrum, 8 × 2 tuần sprint.  
- Sprint Reviews và Retrospectives được tiến hành với các bên liên quan.  
- Các buổi chuyển giao kiến thức được lên lịch vào cuối mỗi sprint.

## 2.4 Các cân nhắc về bảo mật
- Kích hoạt MFA khi truy cập tài khoản.  
- Cấu hình AWS CloudTrail & Config để giám sát.  
- Áp dụng WAF để chặn các yêu cầu độc hại.  
- Mã hóa dữ liệu nhạy cảm sử dụng Secrets Manager & AWS KMS.  

---

# 3. CÁC HOẠT ĐỘNG VÀ SẢN PHẨM BÀN GIAO

## 3.1 Các hoạt động và sản phẩm bàn giao

| Giai đoạn dự án | Thời gian | Hoạt động | Sản phẩm bàn giao/Mốc quan trọng | Tổng công sức |
|-----------------|-----------|-----------|----------------------------------|---------------|
| Đánh giá | Tuần 1-2 | Thu thập yêu cầu, ước tính chi phí | Tài liệu yêu cầu | 12 ngày công |
| Thiết lập hạ tầng cơ bản | Tuần 3-4 | Cung cấp S3, Amplify, CloudFront | Môi trường cơ bản hoạt động | 12 ngày công |
| Thiết lập các thành phần | Tuần 5-6 | API Gateway, Lambda, DynamoDB | Backend & xác thực sẵn sàng | 12 ngày công |
| Kiểm thử & Triển khai | Tuần 7-8 | Kiểm thử tích hợp đầy đủ | Hệ thống được triển khai | 12 ngày công |
| Bàn giao | Tuần 8-12 | Chuyển giao kiến thức & tài liệu | Sản phẩm cuối cùng được chấp nhận | 25 ngày công |

## 3.2 Ngoài phạm vi
- Lưu trữ không phải AWS.  
- Di chuyển hệ thống cũ.  
- Phát triển AI/ML tùy chỉnh ngoài Translate/Bedrock.  

## 3.3 Lộ trình đưa vào sản xuất
- POC được xây dựng cho các trường hợp sử dụng chính.  
- Thiết lập sản xuất yêu cầu điều chỉnh để đạt hiệu quả vận hành tối ưu.  
- Xử lý lỗi, ghi log và kiểm thử được triển khai đầy đủ.

---

# 4. DỰ TOÁN CHI PHÍ AWS THEO DỊCH VỤ

| Nhóm dịch vụ | Tổng chi phí (USD/tháng) |
|--------------|--------------------------|
| Lưu trữ & Dữ liệu | 3.55 |
| Backend & Xử lý | 0.75 |
| Giao diện & Bảo mật | 8.20 |
| Email & Thông báo | 0.20 |
| AI & ML (Tùy chọn) | 0.25 |
| Giám sát & Log | 1.50 |
| **Tổng cộng (Thực tế)** | **≈ 14.45 USD / tháng** |

[Xem AWS Pricing Calculator](https://calculator.aws/#/estimate?id=7484f3cafbe4877fbcc9ac7f379d0911891f4a9e)

---

# 5. NHÓM THỰC HIỆN

| Họ và tên | Mã số sinh viên |
|-----------|-----------------|
| Nguyễn Tuấn Kiệt | SE182120 |
| Nguyễn Thanh Sơn | SE183379 |
| Trương Minh Khánh| SE182131 |
| Nguyễn Văn Thành | SE193632 |
| Lê Hồ Gia Bảo    | SE184518 |