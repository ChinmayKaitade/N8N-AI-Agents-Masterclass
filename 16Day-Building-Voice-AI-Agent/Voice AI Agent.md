# **DAY 16: Building Your First Voice AI Agent - Simplest Way** 🗣️🤖

This guide walks you through building a **Voice AI Agent** by integrating it with a RAG (Retrieval Augmented Generation) system using **11 Labs** and **N8N**. The goal is to create a smart agent that can answer questions verbally based on your specific knowledge base. This example is tailored for the portfolio of Chinmay Kaitade.

---

### **1. The Challenge: A Voice Agent That Knows Nothing** 🤷‍♀️

Initially, a simple voice agent on 11 Labs might not have access to specific information, leading to generic or incomplete responses (e.g., failing to provide project details for "Chinmay's portfolio" because it's not connected to a knowledge base).

---

### **2. The Solution: Voice Agent + RAG Integration** 💡

The core idea is to connect a voice agent with a RAG system. This allows the agent to:
* **Hear** and understand the user's verbal query.
* **Retrieve** relevant information from a custom knowledge base (like the Pinecone-backed RAG agent from a previous video).
* **Generate** a verbal answer using the retrieved context.

*If you haven't built the RAG agent yet, the video emphasizes revisiting that process first.*

---

### **3. Building the Voice Agent with 11 Labs** 🎤

This section details the steps to set up the voice agent on 11 Labs.

#### **A. 11 Labs Dashboard Setup** 🖥️
* **Login to 11 Labs**: You'll get 10,000 free credits to start.
* **Navigate to Conversational AI**: Go to "Conversational AI" > "Agents" > "New Agent".
* **Choose Blank Template**: Select a blank template to start customizing your agent.
* **Name Your Agent**: Give it a descriptive name (e.g., "Chinmay's Portfolio Agent").

#### **B. Agent Configuration** ⚙️
* **Language**: Set the primary language (e.g., English) and add additional languages (e.g., Hindi).
* **First Message**: Define the agent's opening greeting (e.g., "Hey, how can I help you?").
* **System Prompt**: This is crucial for defining the agent's persona and rules.
    * **Personality**: Describe the agent (e.g., "You are an AI assistant named Sunny, working for Chinmay Kaitade's portfolio. You are friendly, patient, and efficient.").
    * **Goal**: Define its primary objective (e.g., "Answer queries about Chinmay's skills, experience, and projects.").
    * **Guard Rails**: Set strict rules to prevent undesirable behavior (e.g., "Do not provide information that is not accurate or verified. Do not ask sensitive information. Do not make promises that cannot be kept. Do not engage in arguments.").
    * **Tools (Initial Placeholder)**: Initially, it has an "End Call" tool. The video also shows how to add a "Webook" tool later.
* **LLM (Large Language Model)**: Select your preferred LLM (e.g., Gemini Flash 2.0 is used for its conversational flow, but OpenAI or others can be selected).
    * **Temperature**: Adjust this setting to control the randomness/creativity of the agent's responses (e.g., setting it between 20-30 for balanced creativity).
* **Knowledge Base / RAG**: While 11 Labs has its own RAG option, this video focuses on integrating an *external* N8N RAG system.

---

### **4. Integrating 11 Labs Voice Agent with N8N RAG** 🔗

This is the advanced part, connecting 11 Labs to your N8N RAG workflow.

#### **A. N8N Workflow Modifications (RAG Agent)** 🛠️
* **Replace Chat Trigger with Webhook**: In your existing N8N RAG workflow, remove the chat trigger and add a **Webhook node**.
* **Webhook Configuration**:
    * Set the Webhook method to **POST**.
    * Enable "Respond to Webhook" to send the AI's answer back.
    * Copy the Test URL of this Webhook.

#### **B. 11 Labs Custom Tool (Connecting to N8N)** 🎤
* In your 11 Labs agent, go to **Tools** and add a **Custom Tool**.
* **Name**: `n8n`.
* **Description**: "Call this tool to send the user's question to N8N to get the perfect answer."
* **Method**: Set to **POST**.
* **URL**: Paste the N8N Webhook Test URL you copied.
* **Body Parameters**: Enable "Body Parameters" and add a string property named question.
    * **Description**: "The question the user needs the answer for."
    * **Extract from transcript**: "Extract the question that the user is asking about the company and knowledge base."

#### **C. Testing the Integrated Voice Agent** ✅
* **Activate N8N Workflow**: Ensure your N8N RAG workflow with the Webhook is active.
* **Test on 11 Labs**: Call the AI agent from the 11 Labs "Test AI Agent" interface.
* **Ask Questions**: Ask questions that require knowledge from Chinmay's portfolio (e.g., "What are Chinmay's key skills?", "Tell me about the Google Gemini Clone project.").
* The agent should now correctly retrieve information via N8N and respond verbally.
* **Multilingual Support**: If you added Hindi as an additional language, test the agent's ability to understand and respond in Hindi.

---

### **5. Future Enhancements** 🚀

The video teases future updates for this voice agent, including:
* Integrating a calendar tool to enable booking appointments directly through voice commands.
* Sending confirmation emails to both the customer and the business.

---

### **6. N8N Hosting with Hostinger VPS (Reminder)** ☁️💰

For building scalable and reliable AI agents with N8N, hosting your N8N instance on a Virtual Private Server (VPS) like those offered by Hostinger is highly recommended over limited free plans. This provides unlimited executions and full control, which is essential for business-level operations.