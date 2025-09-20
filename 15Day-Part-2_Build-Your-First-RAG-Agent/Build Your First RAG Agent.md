### **Day 15: Building Your First RAG Agent** 🛠️🤖

This guide focuses on building a functional RAG (Retrieval Augmented Generation) agent from scratch, covering the practical steps for data pre-processing and creating a retrieval workflow. This time, we'll use a personal portfolio website as our knowledge base.

---

#### **1. Building Your First RAG Agent: Six Steps!** 🚀

The process of building a RAG agent can be broken down into six main steps:

##### **Step 1: Create Your Knowledge Base** 📚📝
* Your knowledge base is the central repository of your data (e.g., portfolio details, work experience, projects) on which the RAG agent will operate.
* **Example**: Use the content from a portfolio website like `chinmaykaitadeportfolio.vercel.app` to create a Q&A document in PDF or Google Docs format. The document would contain details about skills, projects (e.g., "Google Gemini Clone," "Paste Application"), and work experience.
* Convert your data into a PDF or similar document format.

##### **Step 2: Upload to Google Drive** ☁️📂
* Upload your knowledge base document to a dedicated folder in your Google Drive (e.g., "Chinmay Portfolio Knowledge Base").
* Ensure the folder is well-organized for easy management.

##### **Step 3: Connect Google Drive Credentials (using N8N)** 🔗🔑
* Create a new workflow in N8N (e.g., "Pre-Data Processing").
* Add a Google Drive node to monitor changes in a specific folder.
* **Connecting Google Drive API**:
    * Go to Google Cloud Console and log in with the account you want to connect.
    * Create a New Project (e.g., "N8N Test RAG Workflow").
    * Enable the Google Drive API for this project.
    * Go to Credentials and Create Credentials -> OAuth client ID -> Web application.
    * Name your app (e.g., "N8N Portfolio Agent").
    * Set the Authorized redirect URIs by copying the URL from N8N's Google Drive credential setup.
    * Copy the generated Client ID and Client Secret from Google Cloud Console and paste them into N8N.
    * **Troubleshooting "Access Blocked"**: If you encounter this, go to the OAuth Consent Screen in Google Cloud Console, then Audience, and Publish your app to production.
    * Once connected, select your Google Drive folder and set it to "Watch for file created" to automatically process new files.
    * Add another Google Drive node to "Download a File" from the connected folder, mapping the file ID from the previous step's JSON output.

##### **Step 4: Connect Pinecone Credentials** 🌲🔐
* Go to Pinecone and log in or sign up.
* Create an Index (e.g., "chinmay-portfolio-rag").
* Select your desired embedding model (e.g., "text-embedding-small" from OpenAI).
* In N8N, add a Pinecone Vector Store node.
* Create a new Pinecone credential by generating an API Key from your Pinecone dashboard and pasting it into N8N.

##### **Step 5: Add OpenAI Embedding Credentials** 🔑💬
* In N8N, within the Pinecone Vector Store node, add an Embedding option and select "Embeddings OpenAI."
* Generate an OpenAI API Key from your OpenAI dashboard.
* Add this API Key as a new credential in N8N.
* Select your desired embedding model (e.g., "text-embedding-3-small").
* Configure the Pinecone Vector Store node:
    * Select your Pinecone index (e.g., "chinmay-portfolio-rag").
    * Set the Document Dropdown to "Default Data Loader" and select "Binary File."
    * Set "Load all input data" and "Automatically detect MIME type."
    * Add a "Metadata" option with Property Name: "fileName" and Value: map it to the "Name" field from the Google Drive download step.
* Add a Text Splitter node:
    * Choose "Recursive Character Text Splitter."
    * Set Chunk Size (e.g., 500 characters) and Chunk Overlap (e.g., 200 characters). These values may require experimentation for optimal results.
* Test your workflow! After testing, verify that records have been created in your Pinecone index.
* Activate and Save the pre-processing workflow. Now, any new files added to your Google Drive folder will automatically be processed and added to your RAG agent's knowledge base.

##### **Step 6: Build the Retrieval Workflow (The Chatbot)** 💬➡️✅
* Create a new workflow for the RAG agent itself.
* Add a Chat Trigger node (e.g., for general chat, Telegram, WhatsApp, etc.). This is where the user's query will come in.
* Add an AI Agent node.
* Configure the Chat Model (e.g., OpenAI's GPT-4.4 Mini).
* Add a "Simple Memory" to the AI Agent for context.
* Add a Tool within the AI Agent, selecting "Pinecone Vector Store."
* Choose your Pinecone API account.
* Set Operation Mode to "Retrieve Documents as Tool for AI Agent."
* Give it a "Company" name (e.g., "Chinmay Portfolio") and a descriptive "Description" (e.g., "Retrieves data when the user asks for information about Chinmay's projects, skills, or experience.").
* Select your Pinecone index (e.g., "chinmay-portfolio-rag").
* Add an Embedding option within the Pinecone Vector Store, selecting "Embeddings OpenAI" and the "text-embedding-3-small" model.
* Test your RAG Agent! Open the chat and ask questions (e.g., "What are Chinmay's skills?", "Tell me about the Google Gemini Clone project.").
* The agent will retrieve information from your Pinecone knowledge base and provide accurate, context-aware answers, demonstrating the power of personalized AI.

---
This comprehensive guide enables you to create an AI agent that can intelligently answer questions based on your specific, pre-processed data, offering powerful automation and personalized interactions. 🚀💼 