# Customer Support Bot Tutorial

A complete step-by-step guide to creating a customer support bot using Azure AI Foundry.

## Overview

This tutorial walks you through creating a professional customer support bot that can:
- Answer product questions
- Help with order inquiries
- Provide shipping and return information
- Escalate complex issues to human agents

## Prerequisites

- ✅ Azure subscription with AI Foundry access
- ✅ Azure OpenAI resource deployed
- ✅ Sample knowledge base documents (we'll create these)

## Step 1: Prepare Your Knowledge Base

First, let's create the essential documents your support bot will need.

### Create FAQ Document
Create a file called `customer-support-faq.txt`:

```text
BUSINESS HOURS
We are open Monday through Friday from 8 AM to 8 PM EST.
Weekend support is available via email with responses within 24 hours.

SHIPPING INFORMATION
- Standard shipping: 5-7 business days ($4.99)
- Express shipping: 2-3 business days ($9.99)
- Overnight shipping: Next business day ($19.99)
- Free shipping on orders over $75

RETURN POLICY
- Returns accepted within 30 days of purchase
- Items must be in original condition with tags attached
- Return shipping is free for defective items
- Refunds processed within 5-7 business days

PAYMENT METHODS
We accept:
- All major credit cards (Visa, MasterCard, American Express)
- PayPal
- Apple Pay
- Google Pay
- Buy now, pay later options available

WARRANTY INFORMATION
- Standard 1-year manufacturer warranty on all products
- Extended warranty options available at checkout
- Warranty covers manufacturing defects
- Does not cover damage from misuse or normal wear
```

### Create Product Information Document
Create `product-catalog.txt`:

```text
LAPTOPS
- UltraBook Pro 15": $1,299 - High-performance laptop with 16GB RAM, 512GB SSD
- BusinessBook 14": $899 - Reliable business laptop with 8GB RAM, 256GB SSD
- GamerX 17": $1,899 - Gaming laptop with RTX graphics, 32GB RAM, 1TB SSD

ACCESSORIES
- Wireless Mouse: $29.99 - Ergonomic design with 6-month battery life
- USB-C Hub: $49.99 - 7-port hub with 4K HDMI, USB 3.0, and fast charging
- Laptop Stand: $39.99 - Adjustable aluminum stand for better ergonomics

SUPPORT SERVICES
- Setup assistance: Free for 30 days after purchase
- Technical support: Available via phone, chat, or email
- On-site repair: Available in major metropolitan areas
```

## Step 2: Access Azure AI Foundry

1. Navigate to [https://ai.azure.com](https://ai.azure.com)
2. Sign in with your Azure credentials
3. Select your subscription and resource group

## Step 3: Create a New Project

1. Click **"+ New project"**
2. Configure project settings:
   ```yaml
   Project name: "Customer Support Bot"
   Description: "AI-powered customer support assistant"
   Hub: Select existing or create new
   Region: East US (or your preferred region)
   ```
3. Click **"Create"**

## Step 4: Create Your Support Bot Agent

1. In your project, navigate to **"Agents"** in the left sidebar
2. Click **"+ Create agent"**
3. Choose **"Blank agent"** for full customization

## Step 5: Configure Agent Basic Settings

### Agent Information
```yaml
Name: TechCorp Support Assistant
Description: Professional customer support bot for TechCorp products and services
```

### System Instructions
Copy and paste these instructions:

```text
You are a professional customer support representative for TechCorp, a technology company specializing in laptops and accessories.

ROLE & RESPONSIBILITIES:
- Provide accurate information about products, shipping, returns, and policies
- Help customers track orders and resolve account issues
- Maintain a friendly, professional, and empathetic tone
- Escalate complex issues to human agents when necessary

COMMUNICATION STYLE:
- Be concise but thorough
- Use bullet points for lists when helpful
- Always acknowledge the customer's concern
- Offer multiple solutions when possible
- End responses by asking if there's anything else you can help with

ESCALATION CRITERIA:
Escalate to human agent for:
- Billing disputes or refund requests over $100
- Technical issues requiring advanced troubleshooting
- Complaints about product defects
- Requests for manager/supervisor
- Account security issues

SAMPLE RESPONSES:

Customer: "What are your hours?"
You: "We're here to help Monday through Friday from 8 AM to 8 PM EST. For weekend inquiries, you can email us and we'll respond within 24 hours. What can I assist you with today?"

Customer: "I want to return something"
You: "I'd be happy to help with your return. We accept returns within 30 days of purchase. Could you please provide your order number so I can look up the details and guide you through the process?"

Customer: "This is ridiculous, I demand a refund!"
You: "I understand your frustration, and I want to make this right for you. Let me look into your situation immediately. Could you please share your order number and tell me more about the issue you're experiencing?"
```

## Step 6: Configure Model Settings

Select your model and parameters:

```yaml
Model: gpt-4 (recommended for accuracy)
Temperature: 0.3 (for consistent, reliable responses)
Max response length: 600 tokens
Top P: 0.9
Stop sequences: (leave empty)
```

## Step 7: Add Knowledge Sources

1. Click **"Add data source"** or **"Knowledge"**
2. Select **"Upload files"**
3. Upload your prepared documents:
   - `customer-support-faq.txt`
   - `product-catalog.txt`
4. Configure indexing settings:
   ```yaml
   Chunk size: 800 tokens
   Chunk overlap: 100 tokens
   Search type: Semantic + Keyword hybrid
   Top-k results: 5
   ```

## Step 8: Test Your Support Bot

Use the test panel to validate your bot with these scenarios:

### Test 1: Basic Greeting
**Input:** "Hi there!"
**Expected:** Friendly greeting + offer to help

### Test 2: Hours Inquiry
**Input:** "What time do you close?"
**Expected:** Business hours information

### Test 3: Shipping Question
**Input:** "How much is overnight shipping?"
**Expected:** Overnight shipping cost ($19.99)

### Test 4: Return Request
**Input:** "I need to return my laptop"
**Expected:** Request for order number + return policy info

### Test 5: Product Information
**Input:** "Tell me about the UltraBook Pro"
**Expected:** Product details and pricing

### Test 6: Escalation Trigger
**Input:** "This is terrible service, I want to speak to your manager!"
**Expected:** Empathetic response + offer to escalate

## Step 9: Add Advanced Features

### Conversation Starters
Add these suggested conversation starters:

- "Check my order status"
- "Return or exchange a product"
- "Product information and pricing"
- "Shipping and delivery questions"
- "Technical support"

### Function Calling (Optional)
If you have order management systems, add function calling:

```json
{
  "name": "lookup_order_status",
  "description": "Look up the current status of a customer order",
  "parameters": {
    "type": "object",
    "properties": {
      "order_number": {
        "type": "string",
        "description": "The customer's order number"
      }
    },
    "required": ["order_number"]
  }
}
```

## Step 10: Deploy Your Support Bot

### Web Chat Deployment
1. Go to the **"Deploy"** tab
2. Select **"Web chat"**
3. Customize appearance:
   ```yaml
   Bot name: "TechCorp Support"
   Welcome message: "Hello! I'm here to help with your TechCorp questions. How can I assist you today?"
   Theme: Corporate (or match your brand)
   Primary color: #0066cc (or your brand color)
   ```
4. Generate and copy the embed code

### Teams Deployment (Optional)
1. Select **"Microsoft Teams"**
2. Follow the configuration wizard
3. Install in your organization's Teams

### Custom API Integration
1. Choose **"Custom application"**
2. Copy the endpoint URL and authentication details
3. Implement in your website or application

## Step 11: Test in Production Environment

Before going live, test these real-world scenarios:

### Happy Path Testing
```
✅ "What laptops do you sell?" → Product catalog info
✅ "How do I return an item?" → Return process explanation
✅ "What are your hours?" → Business hours
✅ "How much is shipping?" → Shipping options and costs
```

### Edge Case Testing
```
✅ "I ordered but never got confirmation" → Request order details + escalation offer
✅ "My laptop is broken" → Troubleshooting + warranty info
✅ "You guys suck!" → Professional response + de-escalation
✅ "Can you help me with taxes?" → Polite redirect to appropriate resource
```

## Step 12: Monitor and Optimize

### Key Metrics to Track
- **Resolution Rate**: % of queries resolved without human handoff
- **Customer Satisfaction**: Feedback scores (implement rating system)
- **Response Accuracy**: Regular audit of agent responses
- **Common Queries**: Identify knowledge gaps

### Weekly Optimization Tasks
1. Review conversation logs
2. Update knowledge base with new information
3. Refine system instructions based on performance
4. Add new conversation starters for trending topics

## Troubleshooting Common Issues

### Issue: Bot gives generic responses
**Solution:** 
- Add more specific examples in system instructions
- Expand knowledge base with detailed information
- Lower temperature setting for more focused responses

### Issue: Bot can't find product information
**Solution:**
- Verify knowledge base upload completed successfully
- Check search relevance thresholds
- Add more product keywords and descriptions

### Issue: Bot doesn't escalate when it should
**Solution:**
- Review and clarify escalation criteria in system instructions
- Add specific trigger phrases for escalation
- Test escalation scenarios regularly

## Success Metrics

Your customer support bot is successful when:
- ✅ 80%+ customer queries resolved without escalation
- ✅ Average response time under 3 seconds
- ✅ Customer satisfaction score above 4.0/5.0
- ✅ Reduction in human support ticket volume

## Next Steps

1. **Integrate with CRM**: Connect to your customer management system
2. **Add Multilingual Support**: Expand to support multiple languages
3. **Implement Voice**: Add voice capabilities for phone support
4. **Create Specialized Bots**: Develop bots for specific product lines
5. **Analytics Dashboard**: Build comprehensive reporting and analytics

---

**🎉 Congratulations!** You've successfully created a professional customer support bot. Your bot is now ready to help customers 24/7 with consistent, accurate information.

Remember to regularly update your knowledge base and refine the bot based on real customer interactions for continuous improvement.