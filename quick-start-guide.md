# Azure AI Foundry Agent Quick Start

## 🚀 Create Your First Agent in 10 Minutes

### Step 1: Access Azure AI Foundry
- Go to [ai.azure.com](https://ai.azure.com)
- Sign in with Azure credentials

### Step 2: Create Project
1. Click **"+ New project"**
2. Name: `my-agent-project`
3. Select or create Hub
4. Click **"Create"**

### Step 3: Create Agent
1. Navigate to **"Agents"** → **"+ Create agent"**
2. Choose template or start blank

### Step 4: Configure Agent
```yaml
Name: Support Bot
Instructions: |
  You are a helpful customer support agent.
  Be professional, friendly, and concise.
  If you don't know something, offer to escalate.
Model: gpt-35-turbo
Temperature: 0.3
```

### Step 5: Test & Deploy
1. Test in chat panel
2. Click **"Deploy"** → **"Web chat"**
3. Copy embed code

**🎉 Done!** Your agent is live and ready to help users.

---

## Real-World Example: Customer Service Bot

### Agent Instructions Template
```text
You are a customer service representative for [COMPANY NAME].

CAPABILITIES:
- Answer product questions
- Check order status  
- Explain policies (shipping, returns, warranty)
- Help with account issues

GUIDELINES:
- Be professional and empathetic
- Ask clarifying questions when needed
- Provide accurate information only
- Escalate complex issues to humans

ESCALATION TRIGGERS:
- Billing disputes
- Technical issues requiring specialist
- Complaints requiring manager attention
- Requests outside your knowledge

SAMPLE RESPONSES:
User: "What are your hours?"
You: "We're open Monday-Friday 9 AM to 6 PM EST. Is there something specific I can help you with today?"

User: "I want a refund!"
You: "I understand you'd like to return something. Could you please provide your order number so I can look into this for you?"
```

### Knowledge Base Setup
1. **Upload key documents**:
   - Product catalog
   - FAQ document
   - Shipping policy
   - Return policy

2. **Organize by categories**:
   ```
   📁 Products (specifications, pricing)
   📁 Orders (tracking, modifications)
   📁 Support (troubleshooting, warranty)
   📁 Policies (shipping, returns, privacy)
   ```

### Testing Checklist
- ✅ Greeting and introduction
- ✅ Product information requests  
- ✅ Order status inquiries
- ✅ Return/refund questions
- ✅ Unknown/out-of-scope queries
- ✅ Escalation scenarios

---

## Advanced Configuration Tips

### Model Selection Guide
```yaml
gpt-35-turbo:
  Best for: Fast responses, cost-effective
  Use when: High volume, simple queries
  
gpt-4:
  Best for: Complex reasoning, accuracy
  Use when: Quality is critical, nuanced responses needed
```

### Parameter Optimization
```yaml
Customer Service (Consistent):
  temperature: 0.2-0.4
  max_tokens: 500-800
  
Creative Content:
  temperature: 0.7-0.9
  max_tokens: 1000-1500
```

### Function Calling Example
```json
{
  "name": "check_order_status",
  "description": "Look up current status of customer order",
  "parameters": {
    "type": "object", 
    "properties": {
      "order_id": {
        "type": "string",
        "description": "Customer's order ID number"
      }
    },
    "required": ["order_id"]
  }
}
```

---

## Deployment Options

### 1. Web Chat Integration
```html
<!-- Embed in your website -->
<iframe 
  src="https://your-agent.azurewebsites.net/chat"
  width="400" 
  height="600"
  style="border: none;">
</iframe>
```

### 2. Microsoft Teams
1. Go to Deploy → Teams
2. Follow setup wizard  
3. Add to Teams channels

### 3. Custom API Integration
```python
import requests

# Call your agent API
response = requests.post(
    "https://your-agent-endpoint.com/api/chat",
    headers={"Authorization": "Bearer YOUR_TOKEN"},
    json={
        "message": "Hello, I need help",
        "user_id": "user123",
        "session_id": "session456"
    }
)

agent_response = response.json()["message"]
```

---

## Monitoring & Analytics

### Key Metrics to Track
- **Resolution Rate**: % resolved without human handoff
- **Response Time**: Average time to respond
- **User Satisfaction**: Feedback scores
- **Top Intents**: Most common user questions
- **Escalation Rate**: % requiring human assistance

### Performance Dashboard
```yaml
Daily Metrics:
  - Total conversations: 150
  - Avg response time: 2.1 seconds  
  - Resolution rate: 87%
  - User satisfaction: 4.2/5.0
  - Top queries: ["order status", "shipping", "returns"]
```

---

## Common Issues & Solutions

### Issue: Agent gives generic responses
**Solution**: 
- Add more specific instructions
- Include example conversations
- Provide detailed context about your business

### Issue: Slow response times  
**Solution**:
- Optimize knowledge base size
- Use faster model (gpt-35-turbo)
- Implement response caching

### Issue: Agent can't find information
**Solution**:
- Verify knowledge base is uploaded correctly
- Check search relevance thresholds  
- Test with various query phrasings

---

Ready to create your agent? Start with the [complete step-by-step guide](create-azure-ai-foundry-agent.md) or dive into the [examples](examples/) directory for working code samples!