---
title : "Setup S3 Static Website"
date: 2025-09-09
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

In this final section, you will deploy your chatbot frontend to Amazon S3 as a static website. This provides a cost-effective way to host your web application.

**1. Create S3 Bucket**

- Open the [S3 Console](https://s3.console.aws.amazon.com/s3/)
- Click **Create bucket**
- Enter bucket name: `my-bedrock-chatbot-frontend` (must be globally unique)
- Select your region
- **Uncheck** "Block all public access"
- Acknowledge the warning about public access
- Click **Create bucket**

**2. Enable Static Website Hosting**

- Click on your bucket name
- Go to **Properties** tab
- Scroll down to **Static website hosting**
- Click **Edit**
- Select **Enable**
- Index document: `index.html`
- Click **Save changes**
- Note the **Bucket website endpoint** URL

**3. Add Bucket Policy for Public Access**

- Go to **Permissions** tab
- Scroll to **Bucket policy**
- Click **Edit**
- Paste the following policy (replace `YOUR-BUCKET-NAME`):

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
        }
    ]
}
```

- Click **Save changes**

**4. Create Frontend HTML File**

Create a file named `index.html` with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Chatbot with Claude</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .container {
            width: 90%;
            max-width: 800px;
            height: 90vh;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            display: flex;
            flex-direction: column;
        }
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 20px 20px 0 0;
            text-align: center;
        }
        .chat-container {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            background: #f5f5f5;
        }
        .message {
            margin-bottom: 15px;
            display: flex;
            align-items: flex-start;
        }
        .message.user { justify-content: flex-end; }
        .message-content {
            max-width: 70%;
            padding: 12px 18px;
            border-radius: 18px;
            word-wrap: break-word;
        }
        .message.user .message-content {
            background: #667eea;
            color: white;
        }
        .message.assistant .message-content {
            background: white;
            color: #333;
            border: 1px solid #e0e0e0;
        }
        .input-container {
            padding: 20px;
            background: white;
            border-radius: 0 0 20px 20px;
            display: flex;
            gap: 10px;
        }
        #userInput {
            flex: 1;
            padding: 12px 18px;
            border: 2px solid #e0e0e0;
            border-radius: 25px;
            font-size: 16px;
            outline: none;
        }
        #userInput:focus { border-color: #667eea; }
        #sendButton {
            padding: 12px 30px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
        }
        #sendButton:hover { transform: translateY(-2px); }
        #sendButton:disabled {
            background: #ccc;
            cursor: not-allowed;
        }
        .loading {
            display: none;
            text-align: center;
            padding: 10px;
            color: #667eea;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🤖 AI Chatbot with Claude</h1>
            <p>Powered by Amazon Bedrock</p>
        </div>
        
        <div class="chat-container" id="chatContainer">
            <div class="message assistant">
                <div class="message-content">
                    Hello! I'm Claude, your AI assistant. How can I help you today?
                </div>
            </div>
        </div>
        
        <div class="loading" id="loading">Claude is thinking...</div>
        
        <div class="input-container">
            <input type="text" id="userInput" placeholder="Type your message..." 
                   onkeypress="if(event.key==='Enter') sendMessage()">
            <button id="sendButton" onclick="sendMessage()">Send</button>
        </div>
    </div>

    <script>
        // IMPORTANT: Replace with your API Gateway endpoint
        const API_ENDPOINT = 'https://YOUR-API-ID.execute-api.us-east-1.amazonaws.com/prod/chat';
        
        let conversationHistory = [];

        function addMessage(role, content) {
            const chatContainer = document.getElementById('chatContainer');
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${role}`;
            messageDiv.innerHTML = `<div class="message-content">${content}</div>`;
            chatContainer.appendChild(messageDiv);
            chatContainer.scrollTop = chatContainer.scrollHeight;
        }

        async function sendMessage() {
            const userInput = document.getElementById('userInput');
            const sendButton = document.getElementById('sendButton');
            const loading = document.getElementById('loading');
            const message = userInput.value.trim();
            
            if (!message) return;
            
            // Disable input
            userInput.disabled = true;
            sendButton.disabled = true;
            loading.style.display = 'block';
            
            // Display user message
            addMessage('user', message);
            userInput.value = '';
            
            try {
                const response = await fetch(API_ENDPOINT, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        message: message,
                        history: conversationHistory
                    })
                });
                
                const data = await response.json();
                
                if (response.ok) {
                    addMessage('assistant', data.message);
                    conversationHistory = data.conversationHistory;
                } else {
                    addMessage('assistant', `Error: ${data.error || 'Something went wrong'}`);
                }
            } catch (error) {
                addMessage('assistant', `Error: ${error.message}`);
            } finally {
                userInput.disabled = false;
                sendButton.disabled = false;
                loading.style.display = 'none';
                userInput.focus();
            }
        }
    </script>
</body>
</html>
```

**5. Update API Endpoint**

In the `index.html` file, replace:
```javascript
const API_ENDPOINT = 'https://YOUR-API-ID.execute-api.us-east-1.amazonaws.com/prod/chat';
```

With your actual API Gateway endpoint from section 5.5.

**6. Upload to S3**

- Go back to your S3 bucket
- Click **Upload**
- Drag and drop your `index.html` file
- Click **Upload**

**7. Access Your Chatbot**

- Go to **Properties** tab
- Find **Static website hosting**
- Click on the **Bucket website endpoint** URL
- Your chatbot is now live! 🎉

**8. Test Your Chatbot**

Try asking questions like:
- "What is Amazon Bedrock?"
- "Explain AWS Lambda in simple terms"
- "Tell me a joke"

**Congratulations!** You have successfully built and deployed a serverless AI chatbot using Amazon Bedrock, Lambda, API Gateway, and S3!

**Next Steps:**
- Add authentication with Amazon Cognito
- Implement conversation memory with DynamoDB
- Add file upload capabilities
- Deploy with custom domain using Route 53
