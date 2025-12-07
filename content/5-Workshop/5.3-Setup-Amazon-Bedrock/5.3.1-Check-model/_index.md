---
title : "Enable and Test Claude Haiku 4.5"
date: 2025-09-09 
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

**1. Navigate to Amazon Bedrock Console**

Open the [Amazon Bedrock Console](https://console.aws.amazon.com/bedrock/)

**2. Click on Model Catalog and Search for Claude Haiku 4.5**

In the Model Catalog, search for "Claude" to find the Claude Haiku 4.5 model.

**3. Click on Claude Haiku 4.5 and Find the Model ID**

Note the Model ID - you will need this for your Lambda function later.

**4. Test the Model in Playground (Optional)**

You can click "Open in playground" to test the model before integrating it into your application.

{{% notice note %}}
**Important:** You no longer need to request model access separately. With an IAM account that has AWS Marketplace permissions, you can directly use the API of any model in Amazon Bedrock. The model will be activated automatically upon first invocation.
{{% /notice %}}

**Reference Documentation:**
- [Claude Model Parameters](https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters-claude.html)
- [Bedrock API Reference](https://docs.aws.amazon.com/bedrock/latest/APIReference/welcome.html)

![endpoint](/images/5-Workshop/5.3-S3-vpc/vpc.png)

+ **For Policy**, leave the default option, **Full Access**, to allow full access to the service. You will deploy **a VPC endpoint policy** in a later lab module to demonstrate restricting access to **S3 buckets** based on policies.

![endpoint](/images/5-Workshop/5.3-S3-vpc/policy.png)

+ Do not add a tag to the VPC endpoint at this time.
+ Click **Create endpoint**, then click x after receiving a successful creation message.

![endpoint](/images/5-Workshop/5.3-S3-vpc/complete.png)
