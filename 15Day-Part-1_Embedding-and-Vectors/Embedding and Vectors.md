# **Day 15 Part 1: AI Agents Masterclass - RAG, Embedding & Vectors** 🧠💡

This notes is a deep dive into Embedding Models and Vector Databases, crucial components for building smart AI agents with your personal data using RAG (Retrieval Augmented Generation).

---

### **1. What is Embedding?** 📚🔢

Imagine your personal data (notes, files, PDFs) as a vast library. Your chatbot struggles to find specific information within it.

- **The Solution: Embedding** 💡
  - Embedding converts all your data (words, sentences, documents) into **meaningful numerical codes (vectors)**.
  - These numbers capture the meaning and context of your information.
  - Similar meanings get similar, but distinct, vectors.
  - The embedding process automatically categorizes data into "genres," keywords, or topics that AI can understand.
  - Your questions are also converted into these "secret code points" (vectors) using the same embedding model.
  - This allows the chatbot to understand your query in the "language" of vectors and find relevant answers efficiently.

Essentially, **Embedding = Meaningful Number Codes that help RAG fetch the right answer!**

---

### **2. Embedding Models: OpenAI's Choice** 🚀

The video recommends using OpenAI's Embedding Models due to their effectiveness and widespread use in large applications.

- **How Pricing Works** 💸

  - OpenAI charges based on the number of **input tokens** you send.
  - **Tokens** are small chunks of text (like words, but smaller pieces).
  - Roughly 800 tokens ≈ 1 page of text.
  - Detailed information is available on the OpenAI platform documentation.

- **Types of OpenAI Embedding Models** 📊
  - **Small Model**:
    - **Pages/Dollar**: ~62,500 pages for $1 🤑
    - **Performance**: 62.3%
    - **Max Input**: 8192 tokens
    - **Recommendation**: Super cheap and very powerful for most projects. Recommended for general use.
  - **Large Model**:
    - **Pages/Dollar**: ~965 pages for $1
    - **Recommendation**: Higher cost but offers better understanding and accuracy for very complex projects or demanding clients.
  - **Medium Model**:
    - **Pages/Dollar**: ~2,000 pages for $1
    - **Recommendation**: Decent performance, suitable for mid-level projects.

---

### **3. Vector Databases: Storing Your Smart Data** 🗄️💾

Once your data is converted into vectors, you need a special database to store and efficiently retrieve them.

- **Pinecone** 🌲

  - A cloud-based vector database.
  - Converts data into vectors (small particles).
  - **Pricing Overview**:
    - **Starter Plan**: Free, good for testing and one project (up to 2GB storage).
    - **Standard Plan**: $25/month for multiple projects and unlimited storage (usage credits apply).
    - **Enterprise Plan**: $500/month (for very high-level use cases only).
  - The starter plan is often sufficient for initial work and testing.

- **Qdrant** 🌐
  - An alternative local system / offline vector database (also has native cloud).
  - Considered more complex than Pinecone by the speaker.
