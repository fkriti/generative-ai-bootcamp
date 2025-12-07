# Create an Agent in Azure AI Foundry - Complete Guide

This guide walks you through creating your first agent in Azure AI Foundry from start to finish. We will be building a basic agentic system using three agents.

## Prerequisites

✅ Azure subscription with access to Azure AI Foundry  
✅ Azure OpenAI resource deployed  
✅ Basic understanding of AI concepts  

## Step 1: Access Azure AI Foundry

1. Navigate to [https://ai.azure.com](https://ai.azure.com)
2. Sign in with your Azure credentials
3. Select your subscription and resource group

## Step 2: Create or select a project

Select an existing project or create a new project using the instructions (here)[https://learn.microsoft.com/en-us/azure/ai-foundry/how-to/create-projects?view=foundry-classic&tabs=foundry].

## Step 3: Create a model deployment

If do not have a gpt-4o deployment, create it following the instucutions (here)[https://learn.microsoft.com/en-us/azure/ai-foundry/quickstarts/get-started-code?view=foundry-classic&tabs=python%2Cpython2].

The instructions in the guide use gpt-4o, but you can try any other model. 

## Step 3: Navigate to Agent Creation

1. In your project, look for **"Agents"** in the left navigation
![Agent on left nav](image.png)
2. Click **"New agent"**

## Step 4: Configure Agent Settings
We will be creating three agents.
### Router Agent
Select the newly created agent and fill below information on the right panel.
1. `SFI-helper-agent` in `Agent name` field
2. Select `gpt-4o` in `Deployment` field
3. Fill belo text in Instructions field:
```md
    You are the Router Agent. Your job is to decide:
    - If the user asks for a summary → route to Summarizer.
    - If the user asks a question → route to Q&A.
    If unclear, ask one short clarifying question.
    Output: route only (Summarizer or Q&A).

```
### Summarizer Agent
Select the newly created agent and fill below information on the right panel.
1. `SFI-summarizer-agent` in `Agent name` field
2. Select `gpt-4o` in `Deployment` field
3. Fill below text in Instructions field:
```md
    You are the Summarizer Agent. Summarize the provided text clearly and concisely.
    - Use bullet points for key ideas.
    - Keep it short and easy to read.
    - Use only the given text. If info is missing, say so.

```
4. Add Knowledge Source
- Click `Add` in **"Knowledge"** section
- Click on `files` tile
- Select `Create a new vector store` under Vector store and name it `SFIVectorStore`
- Click `Select local files` to upload the file which you were asked to download during bootcamp. If you do not have that file, you can download a file from (this link)[https://arxiv.org/pdf/2402.06196] or choose any file of your choice.
- Click `upload and save`

### Q&A Agent
Select the newly created agent and fill below information on the right panel.
1. `SFI-qna-agent` in `Agent name` field
2. Select `gpt-4o` in `Deployment` field
3. Fill below text in Instructions field:
```md
    You are the Q&A Agent. Answer the user’s question using only the provided text.
    - Be clear and direct.
    - If the answer is not in the text, say: “The document does not contain that information.”
```
4. Add Knowledge Source
- Click `Add` in **"Knowledge"** section
- Click on `files` tile
- Select `Select an existing vector store` under Vector store and choose `SFIVectorStore` created during summarizer agent creation.
- Click `select`


## Step 5: Set up connected agents for orchestration

Learn more about connected agents in Azure AI Foundry (here)[https://learn.microsoft.com/en-us/azure/ai-foundry/agents/how-to/connected-agents?view=foundry-classic&pivots=portal].

### Add Summarizer agent
1. Select the `SFI-helper-agent` agent and scroll down in the right panel to find `Connect agents` field and click `Add`

2. Select the `SFI-summarizer-agent` in `Agent` and `summarizer` in `Unique name`.
3. Fill below text in `Detail the steps to activate the agent`:

```md
If the user asks for summary, this agent should be invoked.
```

4. Click `Add`.

![alt text](image-3.png)

### Add Q&A agent
1. Select the `SFI-helper-agent` agent and scroll down in the right panel to find `Connect agents` field and click `Add`

2. Select the `SFI-qna-agent` in `Agent` and `qna` in `Unique name`.
3. Fill below text in `Detail the steps to activate the agent`:

```md
If the user asks any question other than summary, this agent should be invoked.
```

4. Click `Add`.

![alt text](image-4.png)

## Step 6: Test Your Agentic system

1. Select the `SFI-helper-agent` agent and click `Try in playground`.

## Best Practices for Agent Creation

### 1. Clear Instructions
```text
✅ Good: "You are a customer service agent for TechCorp. Help customers with orders, returns, and product questions."

❌ Poor: "You are helpful."
```

### 2. Specific Guidelines
```text
✅ Include specific do's and don'ts
✅ Provide example responses
✅ Define escalation criteria
✅ Set tone and personality
```

### 3. Quality Knowledge Base
- Keep information current and accurate
- Organize content logically
- Use consistent terminology
- Include comprehensive FAQs

### 4. Test Thoroughly
- Test happy path scenarios
- Test edge cases and errors
- Verify escalation triggers
- Check response accuracy

## Troubleshooting Common Issues

### Agent Not Responding Properly
- ✅ Check system instructions clarity
- ✅ Verify model configuration
- ✅ Review knowledge base content
- ✅ Test with simpler queries

### Poor Response Quality
- ✅ Adjust temperature settings
- ✅ Improve prompt engineering
- ✅ Add more training examples
- ✅ Update knowledge sources

### Slow Performance
- ✅ Optimize knowledge base size
- ✅ Reduce max response length
- ✅ Use caching for common queries
- ✅ Consider model selection

## Next Steps

Once your agent is working well:

1. **Scale Up**: Add more knowledge sources
2. **Integrate**: Connect to business systems (CRM, ERP)
3. **Customize**: Add custom functions and workflows
4. **Analyze**: Use analytics to continuously improve
5. **Expand**: Create specialized agents for different departments

**🎉 Congratulations!** You've successfully created your first agent in Azure AI Foundry. 