# FAQ Bot Example

This example demonstrates how to create a simple FAQ bot using Azure AI Foundry.

## Overview

The FAQ Bot is designed to answer frequently asked questions about a company's products and services. It uses a knowledge base of common questions and provides accurate, consistent responses.

## Features

- **Instant Responses**: Quick answers to common questions
- **Fallback Handling**: Graceful handling of unknown queries
- **Context Awareness**: Maintains conversation context
- **Escalation**: Seamless handoff to human agents when needed

## Setup Instructions

### 1. Prepare Knowledge Base

Create a JSON file with your FAQ data:

```json
{
  "faqs": [
    {
      "id": "1",
      "category": "general",
      "question": "What are your business hours?",
      "answer": "We are open Monday through Friday from 9 AM to 6 PM EST. We are closed on weekends and major holidays.",
      "keywords": ["hours", "time", "open", "closed", "business hours"]
    },
    {
      "id": "2",
      "category": "shipping",
      "question": "How long does shipping take?",
      "answer": "Standard shipping takes 3-5 business days. Express shipping takes 1-2 business days. Free shipping is available on orders over $50.",
      "keywords": ["shipping", "delivery", "fast", "express", "standard"]
    },
    {
      "id": "3",
      "category": "returns",
      "question": "What is your return policy?",
      "answer": "We accept returns within 30 days of purchase. Items must be in original condition with tags attached. Refunds are processed within 5-7 business days.",
      "keywords": ["return", "refund", "exchange", "policy", "money back"]
    }
  ]
}
```

### 2. Agent Configuration

**System Instructions:**
```text
You are a helpful customer service FAQ bot for [Company Name]. Your primary role is to answer frequently asked questions quickly and accurately.

Guidelines:
- Provide clear, concise answers based on the knowledge base
- If you don't know the answer, politely say so and offer to connect with human support
- Always be professional and friendly
- Ask clarifying questions if the user's request is unclear
- Suggest related topics when appropriate

If a user asks about something not covered in the FAQ, respond with:
"I don't have specific information about that topic. Let me connect you with a human representative who can provide detailed assistance. Would you like me to do that?"
```

### 3. Implementation

See the Python implementation in `faq_bot.py` for a complete working example.

## Testing

Run the test cases in `test_faq_bot.py` to verify functionality.

## Deployment

Deploy using the provided Flask application in `app.py`.

For more details, refer to the individual files in this directory.