# 🧠 **STEP 2 — Use Free Google Gemini Model Instead of Replicate**

### ✅ Option 1: Use Gemini via **Google AI Studio (No Code)**

1. Go to [https://aistudio.google.com/](https://aistudio.google.com/).

2. Sign in using your **Google Account**.

3. Click on **“New Prompt”**.

4. Paste this instruction:

   ```
   You are a Thumbnail AI Prompt Generator.
   Use this input: {{ $json.chatInput }}
   and give me a viral YouTube thumbnail prompt for AI image generation.
   Always use @chinmay as the main person in the scene.
   The prompt should be extremely detailed and cinematic.
   No emojis, no commas.
   If you want to add text overlay mention it directly without quotes.
   ```

5. Click **Run** to test your prompt.

6. You can copy the output and use it in your thumbnail image generator (like Leonardo.ai, Flux, or Ideogram).

---

### ✅ Option 2: Connect Gemini API to n8n (Automation Way)

If you want this integrated directly inside your **n8n workflow** instead of Replicate:

#### 🪜 Steps to Set It Up:

1. Go to [https://makersuite.google.com/app/apikey](https://makersuite.google.com/app/apikey)

2. Click **Create API Key** → copy it.

3. In **n8n**:

   - Go to **Settings → Credentials → Add Credential → HTTP Request**.
   - Name it **Gemini_API_Key** and paste your key.

4. Create a new **HTTP Request Node** after your Chat Input node.

5. Configure it like this:

   **Method:** `POST`
   **URL:**

   ```
   https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-lite:generateContent?key={{your_api_key}}
   ```

   **Headers:**

   ```
   Content-Type: application/json
   ```

   **Body:**

   ```json
   {
     "contents": [
       {
         "parts": [
           {
             "text": "Use this {{ $json.chatInput }} and give me a great viral thumbnail prompt with @chinmay as main character. Make it cinematic, no emojis, no commas. If you mention text overlay don't put quotes."
           }
         ]
       }
     ]
   }
   ```

6. Add a **Set Node** or **Markdown Node** after this to extract and display the output in your workflow.

---

### ✅ Option 3: Use Gemini inside **n8n’s AI Node (if available)**

If your n8n instance already includes the **Google Gemini node**, simply:

1. Add the **Gemini node** after your Chat Input.
2. Connect your API key.
3. Paste the same prompt template as above.

---

### 💡 Updated Section for Your Document

Replace this part 👇

```markdown
## 🧠 **STEP 2 — Train Your Model**

- Visit: [https://replicate.com/ostris/flux-dev-lora-trainer/train](https://replicate.com/ostris/flux-dev-lora-trainer/train)
```

with this 👇

---

## 🧠 **STEP 2 — Use Free Gemini Model**

- Go to [https://aistudio.google.com/](https://aistudio.google.com/)
- Create a new prompt and paste your thumbnail generation instruction.
- Or, integrate the **Gemini API** into your **n8n workflow** using your free Google API key from [https://makersuite.google.com/app/apikey](https://makersuite.google.com/app/apikey).
- This lets you generate unlimited thumbnail prompts directly inside your workflow — **completely free and faster than Replicate.**

---

# ⚙️ **If the Above Doesn’t Work — Try This Simpler n8n Setup**

Perfect Chinmay 👌
Here’s a **super simple step-by-step guide** to configure the **Gemini API HTTP Node** in **n8n** — using only the built-in fields you see inside the HTTP Request node.

---

## ⚙️ **How to Configure Gemini API in n8n (Step-by-Step)**

### 🪜 1. Add HTTP Request Node

- Click ➕ and add a **“HTTP Request”** node.
- Name it → **Gemini AI Prompt Generator**

---

### 🪜 2. Fill Out These Fields One by One

#### **🔹 HTTP Method**

```
POST
```

#### **🔹 URL**

```
https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=YOUR_API_KEY
```

👉 Replace `YOUR_API_KEY` with the key from [https://makersuite.google.com/app/apikey](https://makersuite.google.com/app/apikey)

---

### 🪜 3. **Authentication**

Leave it as → `None`
(You’re already adding the key in the URL.)

---

### 🪜 4. **Headers**

Click **“Add Header”** → fill as follows:

| Key          | Value            |
| ------------ | ---------------- |
| Content-Type | application/json |

---

### 🪜 5. **Body Content**

Select:

```
Send Body as → JSON
```

Then click **Add Field → Add Parameter → Body Parameters → JSON**

Paste this JSON:

```json
{
  "contents": [
    {
      "parts": [
        {
          "text": "Use this {{$json.chatInput}} and give me a great viral thumbnail prompt with @chinmay as main character. Make it cinematic no emojis no commas If you mention text overlay don't put quotes"
        }
      ]
    }
  ]
}
```

✅ Tip:

- `{{$json.chatInput}}` automatically pulls the text from your Chat Input node.
- No need to edit anything else.

---

### 🪜 6. **Response Format**

```
Response → JSON
```

---

### 🪜 7. **Connect Nodes**

- Connect your **Chat Input Node → Gemini HTTP Node**
- (Optional) Add a **Set Node** after Gemini to clean and display the response text.

Example:
In the **Set Node**, add:

| Name   | Value                                                       |
| ------ | ----------------------------------------------------------- |
| output | `{{$json["candidates"][0]["content"]["parts"][0]["text"]}}` |

This extracts the generated prompt cleanly.

---

### 🧠 That’s it!

Now your n8n flow will:
**User input → Gemini → Generate Thumbnail Prompt → Output Result** 🎯
