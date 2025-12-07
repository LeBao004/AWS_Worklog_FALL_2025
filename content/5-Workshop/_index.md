---
title: "Workshop"
date: 2025-09-09
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# Building a Serverless AI Chatbot with Amazon Bedrock

#### Overview

Amazon Bedrock provides access to leading foundation models (LLMs) from Anthropic, Meta, AI21 Labs and other providers through a simple API, allowing you to build AI applications without managing complex infrastructure.

In this workshop, you will learn how to build, deploy, and test a complete AI Chatbot using serverless architecture that allows users to interact with Claude Haiku 4.5 without managing servers or worrying about scaling.

We will create a system with 5 main components to build the chatbot: Amazon Bedrock (AI engine), AWS Lambda (backend logic), API Gateway (REST API endpoint), Amazon S3 (frontend hosting), and CloudWatch (monitoring). These components provide a complete serverless architecture with low cost and automatic scaling capabilities.

#### Main Components:

+ **Amazon Bedrock (AI Engine)** - Provides Claude Haiku 4.5 model through simple API
+ **AWS Lambda (Backend Logic)** - Runs Node.js code to process requests from API Gateway
+ **API Gateway (REST API Endpoint)** - Creates public HTTPS endpoint for frontend calls
+ **Amazon S3 (Frontend Hosting)** - Hosts static website for chatbot UI
+ **CloudWatch (Monitoring & Debugging)** - Automatically collects logs from Lambda execution

#### Content

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Setup Amazon Bedrock](5.3-Setup-Amazon-Bedrock/)
4. [Setup Lambda Function](5.4-Setup_Lambda/)
5. [Setup API Gateway](5.5-Setup-API-gateway/)
6. [Monitoring with CloudWatch](5.6-Monitoring-CloudWatch/)
7. [Setup S3 Static Website](5.7-Setup-S3/)
6. [Clean up](5.6-Cleanup/)
