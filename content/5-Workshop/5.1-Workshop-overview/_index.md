---
title : "Workshop Overview"
date: 2025-09-09 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

## **Workshop Overview**

In this workshop, you will build a complete AI Chatbot using serverless architecture on AWS. The chatbot uses Claude Haiku 4.5 and is deployed completely serverless with low cost and automatic scaling capabilities.

### Workshop Modules

**Module 1**: Setup Amazon Bedrock
- Enable Claude Haiku 4.5 model access
- Understand inference profiles
- Test model via AWS Console

**Module 2**: Create Lambda Function
- Create Node.js 24 Lambda function
- Deploy chatbot backend code
- Configure IAM role with Bedrock permissions
- Set environment variables

**Module 3**: Configure API Gateway
- Create REST API
- Configure POST /chat endpoint
- Enable CORS
- Test API with Postman

**Module 4**: Deploy Frontend to S3
- Create S3 bucket
- Enable static website hosting
- Upload HTML chatbot UI
- Configure public access

**Module 5**: Testing & Debugging
- Test end-to-end flow
- View CloudWatch logs

### Architecture Overview

```
┌─────────────┐
│   Browser   │
│  (HTML/JS)  │
└──────┬──────┘
       │ HTTPS
       ▼
┌─────────────────────┐
│   Amazon S3         │ ← Static Website Hosting
│  (Frontend HTML)    │
└──────┬──────────────┘
       │ API Call (POST /chat)
       ▼
┌─────────────────────┐
│   API Gateway       │ ← REST API Endpoint
│  (HTTPS Endpoint)   │
└──────┬──────────────┘
       │ Invoke
       ▼
┌─────────────────────┐
│   AWS Lambda        │ ← Backend Logic (Node.js 24)
│  (Chatbot Handler)  │
└──────┬──────────────┘
       │ InvokeModel API
       ▼
┌─────────────────────┐
│  Amazon Bedrock     │ ← AI Engine
│  (Claude Haiku 4.5) │
└─────────────────────┘
       │
       ▼
┌─────────────────────┐
│   CloudWatch        │ ← Monitoring & Logs
│  (Logs & Metrics)   │
└─────────────────────┘
```

### Key Components

**Amazon Bedrock (AI Engine)** - Provides Claude Haiku 4.5 model through simple API. You call InvokeModel API to send messages and receive intelligent AI responses.

**AWS Lambda (Backend Logic)** - Runs Node.js 24 code to process requests from API Gateway. Lambda validates input (message length, history limits), formats prompts for Bedrock, calls Bedrock API, and handles errors.

**API Gateway (REST API Endpoint)** - Creates public HTTPS endpoint (POST /chat) for frontend calls. API Gateway handles CORS configuration, routes requests to Lambda, and provides throttling to protect backend from abuse.

**Amazon S3 (Frontend Hosting)** - Hosts static website (HTML) for chatbot UI. Users access chatbot via browser, interface sends messages to API Gateway, and displays responses from AI.

**CloudWatch (Monitoring & Debugging)** - Automatically collects logs from Lambda execution, allowing you to debug errors.

### Workflow

1. User enters message into chatbot UI (hosted on S3)
2. JavaScript sends POST request to API Gateway endpoint
3. API Gateway invokes Lambda function
4. Lambda validates input, formats prompt, calls Bedrock InvokeModel API
5. Bedrock processes with Claude Haiku 4.5, returns AI response
6. Lambda returns response to API Gateway → Browser
7. CloudWatch logs entire process
