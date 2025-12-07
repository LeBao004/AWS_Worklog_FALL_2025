---
title : "Setup Lambda Function"
date: 2025-09-09
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

**1. Navigate to AWS Lambda**

Open the [AWS Lambda Console](https://console.aws.amazon.com/lambda/). Lambda supports multiple programming languages. For this workshop, we will use Node.js.

**2. Click Create Function**

- Enter function name: `BedrockChatbotHandler`
- Select runtime: **Node.js 24.x**
- Click **Change default execution role**
- Select **Use an existing role**
- Choose the IAM role you created in Prerequisites (with AmazonBedrockFullAccess)
- Click **Create function**

**3. Configure Function Settings**

Navigate to the **Configuration** tab:
- Set Memory to **512 MB**
- Set Timeout to **2 minutes**

**4. Deploy Function Code**

Go to the **Code** tab and paste the following code:

```javascript
const { BedrockRuntimeClient, InvokeModelCommand } = require("@aws-sdk/client-bedrock-runtime");

const client = new BedrockRuntimeClient({ region: "us-east-1" });

exports.handler = async (event) => {
    try {
        // Parse request body
        const body = JSON.parse(event.body || '{}');
        const userMessage = body.message;
        const conversationHistory = body.history || [];
        
        // Validate input
        if (!userMessage || userMessage.trim().length === 0) {
            return {
                statusCode: 400,
                headers: {
                    'Content-Type': 'application/json',
                    'Access-Control-Allow-Origin': '*'
                },
                body: JSON.stringify({ error: 'Message is required' })
            };
        }
        
        // Build conversation for Claude
        const messages = [
            ...conversationHistory,
            { role: "user", content: userMessage }
        ];
        
        // Prepare Bedrock request
        const input = {
            modelId: "us.anthropic.claude-3-5-haiku-20241022-v1:0",
            contentType: "application/json",
            accept: "application/json",
            body: JSON.stringify({
                anthropic_version: "bedrock-2023-05-31",
                max_tokens: 1024,
                messages: messages
            })
        };
        
        // Invoke Bedrock
        const command = new InvokeModelCommand(input);
        const response = await client.send(command);
        
        // Parse response
        const responseBody = JSON.parse(new TextDecoder().decode(response.body));
        const assistantMessage = responseBody.content[0].text;
        
        return {
            statusCode: 200,
            headers: {
                'Content-Type': 'application/json',
                'Access-Control-Allow-Origin': '*'
            },
            body: JSON.stringify({
                message: assistantMessage,
                conversationHistory: [
                    ...messages,
                    { role: "assistant", content: assistantMessage }
                ]
            })
        };
        
    } catch (error) {
        console.error('Error:', error);
        return {
            statusCode: 500,
            headers: {
                'Content-Type': 'application/json',
                'Access-Control-Allow-Origin': '*'
            },
            body: JSON.stringify({ 
                error: 'Internal server error',
                details: error.message 
            })
        };
    }
};
```

**5. Click Deploy**

After pasting the code, click the **Deploy** button to save your Lambda function.

**Key Points:**
- The function validates user input
- Builds conversation history for context
- Calls Bedrock's Claude model
- Returns AI response with updated conversation history
- Includes CORS headers for browser access



