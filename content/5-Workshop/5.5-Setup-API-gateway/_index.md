---
title : "Setup API Gateway"
date: 2025-09-09
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

In this section, you will create a REST API using Amazon API Gateway that will serve as the entry point for your chatbot. The API will receive requests from the frontend and invoke your Lambda function.

**1. Navigate to API Gateway Console**

Open the [API Gateway Console](https://console.aws.amazon.com/apigateway/)

**2. Create REST API**

- Click **Create API**
- Choose **REST API** (not Private or HTTP API)
- Click **Build**
- Select **New API**
- Enter API name: `BedrockChatbotAPI`
- Click **Create API**

**3. Create Resource**

- Click **Actions** → **Create Resource**
- Resource Name: `chat`
- Click **Create Resource**

**4. Create POST Method**

- Select the `/chat` resource
- Click **Actions** → **Create Method**
- Select **POST** from dropdown
- Click the checkmark
- Integration type: **Lambda Function**
- Enable **Lambda Proxy Integration**
- Select your Lambda function: `BedrockChatbotHandler`
- Click **Save**
- Click **OK** to grant API Gateway permission

**5. Enable CORS**

- Select the `/chat` resource
- Click **Actions** → **Enable CORS**
- Keep default settings
- Click **Enable CORS and replace existing CORS headers**
- Click **Yes, replace existing values**

**6. Deploy API**

- Click **Actions** → **Deploy API**
- Deployment stage: **[New Stage]**
- Stage name: `prod`
- Click **Deploy**

**7. Save Your API Endpoint**

After deployment, you will see an **Invoke URL** at the top of the page. It will look like:
```
https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/prod
```

Copy this URL - you will need it for your frontend configuration. Your complete endpoint will be:
```
https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/prod/chat
```

**8. Test Your API (Optional)**

You can test using curl or Postman:

```bash
curl -X POST https://your-api-id.execute-api.us-east-1.amazonaws.com/prod/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello, who are you?"}'
```

Expected response:
```json
{
  "message": "Hello! I'm Claude, an AI assistant created by Anthropic...",
  "conversationHistory": [...]
}
```

**Key Points:**
- REST API provides HTTPS endpoint for frontend
- CORS enabled for browser access
- Lambda proxy integration passes entire request to Lambda
- API Gateway handles authentication and throttling

#### Connect to an EC2 instance and verify connectivity to S3

1. Start a new AWS Session Manager session on the instance named Test-Gateway-Endpoint. From the session, verify that you can list the contents of the bucket you created in Part 1: Access S3 from VPC:

```
aws s3 ls s3://\<your-bucket-name\>
```
![test](/images/5-Workshop/5.5-Policy/test1.png)

The bucket contents include the two 1 GB files uploaded in earlier.

2. Create a new S3 bucket; follow the naming pattern you used in Part 1, but add a '-2' to the name. Leave other fields as default and click create

![create bucket](/images/5-Workshop/5.5-Policy/create-bucket.png)

Successfully create bucket

![Success](/images/5-Workshop/5.5-Policy/create-bucket-success.png)

3. Navigate to: Services > VPC > Endpoints, then select the Gateway VPC endpoint you created earlier. Click the Policy tab. Click Edit policy.

![policy](/images/5-Workshop/5.5-Policy/policy1.png)

The default policy allows access to all S3 Buckets through the VPC endpoint.

4. In Edit Policy console, copy & Paste the following policy, then replace yourbucketname-2 with your 2nd bucket name. This policy will allow access through the VPC endpoint to your new bucket, but not any other bucket in Amazon S3. Click Save to apply the policy.

```
{
  "Id": "Policy1631305502445",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1631305501021",
      "Action": "s3:*",
      "Effect": "Allow",
      "Resource": [
      				"arn:aws:s3:::yourbucketname-2",
       				"arn:aws:s3:::yourbucketname-2/*"
       ],
      "Principal": "*"
    }
  ]
}
```

![custom policy](/images/5-Workshop/5.5-Policy/policy2.png)

Successfully customize policy

![success](/static/images/5-Workshop/5.5-Policy/success.png)

5. From your session on the Test-Gateway-Endpoint instance, test access to the S3 bucket you created in Part 1: Access S3 from VPC
```
aws s3 ls s3://<yourbucketname>
```

This command will return an error because access to this bucket is not permitted by your new VPC endpoint policy:

![error](/static/images/5-Workshop/5.5-Policy/error.png)

6. Return to your home directory on your EC2 instance ` cd~ `

+ Create a file ```fallocate -l 1G test-bucket2.xyz ```
+ Copy file to 2nd bucket ```aws s3 cp test-bucket2.xyz s3://<your-2nd-bucket-name>```

![success](/static/images/5-Workshop/5.5-Policy/test2.png)

This operation succeeds because it is permitted by the VPC endpoint policy.

![success](/static/images/5-Workshop/5.5-Policy/test2-success.png)

+ Then we test access to the first bucket by copy the file to 1st bucket `aws s3 cp test-bucket2.xyz s3://<your-1st-bucket-name>`

![fail](/static/images/5-Workshop/5.5-Policy/test2-fail.png)

This command will return an error because access to this bucket is not permitted by your new VPC endpoint policy.

#### Part 3 Summary:

In this section, you created a VPC endpoint policy for Amazon S3, and used the AWS CLI to test the policy. AWS CLI actions targeted to your original S3 bucket failed because you applied a policy that only allowed access to the second bucket you created. AWS CLI actions targeted for your second bucket succeeded because the policy allowed them. These policies can be useful in situations where you need to control access to resources through VPC endpoints.


