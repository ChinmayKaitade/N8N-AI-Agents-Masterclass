# 📱 Build Your First WhatsApp AI Agent with n8n 🤖💬

This project helps you create a **self-hosted, intelligent AI chatbot** that communicates directly with your **WhatsApp Business or personal number** — complete with **memory**, **AI logic**, and **smooth conversational flow** ⚡

---

## 🚀 Overview

Using **n8n** + **Evolution API (via CloudStation)**, this workflow connects your WhatsApp messages to an AI model (like OpenAI or Gemini), allowing your bot to:

- Reply intelligently to messages 💡
- Maintain conversation context 🧠
- Automate customer interactions 24/7 🌙
- Work seamlessly on your own number 📞

---

## 🧩 Step 1: Set Up the WhatsApp API (Evolution API)

1. **Create a CloudStation Project**

   - Go to **CloudStation**, sign up for a free trial, and create a new project (example: `WhatsApp Buddy`).

2. **Deploy the Evolution API**

   - In your project dashboard, click **Add New → Evolution API Template → Deploy**.
   - Wait until all services (**Redis, Postgres, Evolution API**) show ✅ green status.

3. **Get Server Details**

   - Open the **Evolution API service** → click **Connect** → copy the **Server URL**.

4. **Access the Manager Panel**

   - Paste the Server URL into your browser → tap **Pretty Print** → copy the **Manager Link**.

5. **Log In to the Manager**

   - Open the Manager link → enter the **Authentication API Key** (found in your CloudStation variables).
   - You’re now connected to the Evolution Manager dashboard! 🎉

---

## 📲 Step 2: Link Your WhatsApp Number

1. **Create an Instance**

   - In the **Evolution Manager**, click **Instance** → add your **Instance Name** (e.g., `whatsapp buddy`).

2. **Enter Your WhatsApp Number**

   - Add your number **with country code**, without the **plus sign or spaces**.
     Example: `919876543210` ✅

3. **Scan the QR Code**

   - Tap the ⚙️ Settings icon → choose **Get QR Code**.
   - On your phone, open **WhatsApp → Linked Devices → Scan QR Code**.
   - Once linked, messages will start routing through the Evolution API 💬

---

## 🔗 Step 3: Connect n8n to Evolution API

1. **Add Webhook Trigger in n8n**

   - Create a new workflow → add a **Webhook Node**.
   - Set **Method** to `POST` and define a custom **Path** (e.g., `/whatsappbuddy`).
   - Copy the **Production Webhook URL**.

2. **Integrate with Evolution Manager**

   - Go to **Manager → Integrations → Add Webhook**.
   - Paste your n8n Webhook URL.
   - Under **Events**, enable `message-upserts` to capture incoming messages.
   - Save and activate your n8n workflow ⚡

3. **Install Evolution API Node in n8n**

   - Go to **Settings → Community Nodes** → search for `evolution-api-node` → Install.

4. **Set Up Evolution API Credentials**

   - Add your **Server URL** and **Authentication API Key** (from CloudStation).
   - Test the connection to ensure it’s working ✅

---

## 🧠 Step 4: Build the AI Logic & Conversation Flow

1. **Add an AI Agent Node**

   - Place it between the **Webhook Node** and **Evolution API Node**.
   - Connect the **User Message** from the Webhook JSON body.
   - Add a **System Message** defining the bot’s role (e.g.,

     > “You are a friendly assistant. Reply helpfully to every query.”)

2. **Connect a Chat Model**

   - Use **OpenAI**, **Gemini**, or any **LLM node** for natural responses.

3. **Add Simple Memory**

   - Use the **Simple Memory Node** to store conversation history.
   - Set the **Session ID** as the user’s WhatsApp number (`Remote JID`) to maintain context.

4. **Configure Reply in Evolution API Node**

   - Operation → `Send Text (enviarTexto)`
   - Instance → your created instance name (e.g., `whatsapp buddy`)
   - Destination Number → sender’s Remote JID
   - Message → Output from AI Agent node

---

## 🛑 Prevent Infinite Reply Loops (Recommended)

Add an **If Node** after the Webhook:

- Condition → If `fromMe` is **True** → do nothing
- If **False** → pass to the AI Agent node for processing
  This ensures your bot doesn’t reply to its own messages 🔄

---

## 🎉 You’re Done!

Your WhatsApp AI Agent is now ready! 🚀
It can:

- Receive messages on WhatsApp
- Process them with AI
- Send intelligent replies instantly 💬🤖


