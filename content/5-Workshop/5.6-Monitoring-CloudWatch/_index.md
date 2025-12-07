---
title : "Monitoring with CloudWatch"
date: 2025-09-09
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

AWS Lambda automatically integrates with Amazon CloudWatch to provide monitoring and logging for your serverless applications. In this section, you'll learn how to view and analyze your chatbot's logs.

**1. Navigate to Lambda Function**

Open your Lambda function `BedrockChatbotHandler` in the AWS Console.

**2. View Logs in Monitor Tab**

- Click on the **Monitor** tab
- Click **View CloudWatch logs**

This will take you to CloudWatch Logs where all your Lambda execution logs are stored.

**3. Explore Log Streams**

- Each Lambda invocation creates log entries in log streams
- Click on a log stream to view detailed execution logs
- You can see:
  - Request/response data
  - Execution duration
  - Memory usage
  - Any errors or exceptions

**4. Useful CloudWatch Features**

**Search Logs:**
- Use the search bar to filter logs
- Search for specific error messages or patterns

**Set Up Alerts:**
- Create CloudWatch Alarms for error rates
- Get notified when errors exceed threshold

**View Metrics:**
- Invocation count
- Error rate
- Duration
- Throttles

**5. Common Debugging Scenarios**

**If chatbot doesn't respond:**
- Check CloudWatch logs for error messages
- Verify IAM role has Bedrock permissions
- Check if model ID is correct

**If API Gateway returns 502:**
- Lambda function timeout (increase timeout)
- Lambda function error (check logs)

**If CORS errors in browser:**
- Verify CORS is enabled in API Gateway
- Check Lambda response includes CORS headers

**6. Best Practices**

- Regularly review CloudWatch logs
- Set up alarms for error rates
- Monitor Lambda costs and execution time
- Use structured logging for better analysis

CloudWatch is essential for maintaining and troubleshooting your serverless chatbot!