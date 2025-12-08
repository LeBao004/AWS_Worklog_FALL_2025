---
title: "Proposal"
date: 2025-11-11
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# AWS First Cloud AI Journey – Leaf E-commerce Project Plan

## 1. BACKGROUND and Motivation

## 1.1 Executive Summary
Leaf is an e-commerce platform specializing in fashion products for men and women, including fashion accessories such as jewelry, shoes, hats, and leather straps. The website integrates AWS services to optimize costs and enhance the user experience.

## 1.2 Project Success Criteria
- Fully functional e-commerce platform with AWS integration.
- Optimized cost and performance using serverless architecture.
- Fast page load with CDN (CloudFront) and S3 hosting.
- Seamless notifications using SNS/SES.
- AI-powered translation and assistance (optional) via Amazon Translate & Bedrock.

## 1.3 Assumptions
- Customers have basic knowledge of cloud services and AWS accounts.
- Serverless approach is acceptable; no dedicated servers required.
- Traffic is moderate (~few thousand users/month) and costs are expected to be low.
- Required services (S3, Lambda, DynamoDB, etc.) are accessible in selected AWS regions.
- Images and static assets will be stored in S3/CDN for performance.

---

# 2. SOLUTION ARCHITECTURE / ARCHITECTURAL DIAGRAM

## 2.1 Technical Architecture Diagram
The platform applies an **AWS Serverless architecture** to manage data.  
![](https://paperkite-master.github.io/AWS_FCJ/images/2-Proposal/AWS1.drawio.png)

### Components and Roles in the AWS Architecture

#### A. User Interface Layer
| Service | Role | Detailed Description |
|---------|------|--------------------|
| **AWS Amplify** | Website deployment | Hosts **static websites** (React, Vue, Next.js) and **automatically builds/deploys** when code is pushed to GitHub. |
| **Amazon CloudFront (CDN)** | Improve page loading speed | Caches static content close to users to reduce latency. |
| **Amazon S3** | Store static files & product images | Acts as a content repository for images, banners, CSS/JS files. |

#### B. Application Logic Layer
| Service | Role | Detailed Description |
|---------|------|--------------------|
| **Amazon API Gateway** | API gateway | Receives requests from frontend and forwards them to Lambda functions for processing. |
| **AWS Lambda** | Server-side logic | Handles orders, payments, authentication, email without dedicated servers. |
| **Amazon DynamoDB** | NoSQL database | Stores products, accounts, orders, shopping carts. |
| **AWS Secrets Manager** | Secure sensitive data | Stores API keys, payment tokens, database passwords. |

#### C. User Management & Security Layer
| Service | Role | Detailed Description |
|---------|------|--------------------|
| **AWS WAF** | Web protection | Protects against SQL Injection, XSS, DDoS. |
| **Amazon Route 53** | DNS & domain | Manages domain names. |

#### D. Notification & Communication Layer
| Service | Role | Detailed Description |
|---------|------|--------------------|
| **Amazon SNS** | System notifications | Sends notifications to admins or users. |
| **Amazon SES** | Transactional emails | Sends order confirmations, promotions, password reset emails. |

#### E. AI & Machine Learning Layer
| Service | Role | Detailed Description |
|---------|------|--------------------|
| **Amazon Translate** | Content translation | Translates product descriptions to other languages. |
| **Amazon Bedrock** | AI content generation | Creates chatbots for shopping assistance. |

#### F. Monitoring & Management Layer
| Service | Role | Detailed Description |
|---------|------|--------------------|
| **Amazon CloudWatch** | System monitoring | Monitors logs, performance, alerts for errors or cost spikes. |
| **AWS CloudTrail** | Administrative logging | Tracks configuration changes for auditing purposes. |

## 2.2 Technical Plan
- Collect system requirements and features.  
- Estimate cost and check feasibility.  
- Design UI prototypes using Figma.  
- Build database schema and backend APIs.  
- Develop frontend interface.  
- Integrate AWS services (S3, Lambda, DynamoDB, etc.).  
- Test and deploy system using serverless architecture.

## 2.3 Project Plan
- Agile Scrum framework, 8 × 2-week sprints.  
- Sprint Reviews and Retrospectives conducted with stakeholders.  
- Knowledge transfer sessions scheduled at end of each sprint.

## 2.4 Security Considerations
- Enable MFA on account access.  
- Configure AWS CloudTrail & Config for monitoring.  
- Apply WAF to block malicious requests.  
- Encrypt sensitive data using Secrets Manager & AWS KMS.  

---

# 3. Activities AND Deliverables

## 3.1 Activities and Deliverables

| Project Phase | Timeline | Activities | Deliverables/Milestones | Total man-day |
|---------------|---------|-----------|------------------------|---------------|
| Assessment | Week 1-2 | Collect requirements, estimate costs | Requirement document | X man-day |
| Setup Base Infrastructure | Week 3-4 | Provision S3, Amplify, CloudFront | Working base environment | X man-day |
| Setup Components | Week 5-6 | API Gateway, Lambda, DynamoDB  | Backend & auth ready | X man-day |
| Testing & Go-live | Week 7 | Full integration testing | Live system deployed | X man-day |
| Handover | Week 8 | Knowledge transfer & documentation | Final deliverables accepted | X man-day |

## 3.2 Out of Scope
- Non-AWS hosting.  
- Legacy system migrations.  
- Custom AI/ML development beyond Translate/Bedrock.  

## 3.3 Path to Production
- POC built for main use-cases.  
- Production setup requires tuning for operational excellence.  
- Error handling, logging, and testing fully implemented.

---

# 4. EXPECTED AWS COST BREAKDOWN BY SERVICES

| Service Group | Total Cost (USD/month) |
|---------------|------------------------|
| Storage & Data | 3.55 |
| Backend & Processing | 0.75 |
| UI & Security | 8.20 |
| Email & Notifications | 0.20 |
| AI & ML (Optional) | 0.25 |
| Monitoring & Logs | 1.50 |
| **Total (Actual)** | **≈ 14.45 USD / month** |

[View AWS Pricing Calculator](https://calculator.aws/#/estimate?id=7484f3cafbe4877fbcc9ac7f379d0911891f4a9e)

---

# 5. TEAM


| Name | Student ID |
|---------------|------------------------|
| Nguyễn Tuấn Kiệt | SE182120 |
| Nguyễn Thanh Sơn | SE183379 |
| Trương Minh Khánh| SE182131 |
| Nguyễn Văn Thành | SE193632 |
| Lê Hồ Gia Bảo | SE184518 |