# ⚡ **Unlimited Thumbnail Agent — Workflow Setup Guide**

## 🧩 **STEP 1 — Gather Your Images**

- Collect all your reference or sample images for thumbnail design.
- Convert them into a single **ZIP file** for upload.

---

## 🧠 **STEP 2 — Train Your Model**

- Visit: [https://replicate.com/ostris/flux-dev-lora-trainer/train](https://replicate.com/ostris/flux-dev-lora-trainer/train)

---

## 🧠 **STEP 2 — Use Free Gemini Model (Alternative Option)**

- Go to [https://aistudio.google.com/](https://aistudio.google.com/)
- Create a new prompt and paste your thumbnail generation instruction.
- Or, integrate the **Gemini API** into your **n8n workflow** using your free Google API key from [https://makersuite.google.com/app/apikey](https://makersuite.google.com/app/apikey).
- This lets you generate unlimited thumbnail prompts directly inside your workflow — **completely free and faster than Replicate.**

---

## 🔐 **STEP 3 — Create HuggingFace Account**

- Go to [https://huggingface.co/](https://huggingface.co/)
- Sign up and generate your **User ID** and **Access Token**.
- Copy both and use them inside the **Replicate Trainer**.

---

## ⚙️ **STEP 4 — Create Your n8n Workflow**

### 🧱 Node 1: Chat Input (Trigger)

User inputs thumbnail idea → e.g.

> _"make a thumbnail for travel vlog in bali"_

---

### 🧱 Node 2: AI Prompt Generator (OpenAI, Replicate, or Gemini)

**PROMPT:**

```
Use this "{{ $json.chatInput }}" and give me a great viral thumbnail prompt
and for a person in prompt always use @chinmay
give me just the prompt nothing else other than that
don't put any emojis.

make the prompt as detailed as possible

eg : Capture a stunning thumbnail of @chinmay standing on a breathtaking Andaman Nicobar beach during the rainy season. He is enjoying the serene waves crashing gently in the background, with dramatic dark clouds looming in the sky, yet rays of sunlight breaking through, creating a perfect contrast. The beach is adorned with lush green palm trees swaying in the gentle breeze, and the sand is glistening wet from the recent rain. @chinmay has a joyful expression, arms outstretched as if embracing nature, wearing vibrant beach attire that pops against the moody backdrop. Include the text overlay: "Rainy Bliss in Andaman: A First-Time Adventure!" in bold, eye-catching font to convey excitement and attraction to viewers. The overall vibe should evoke a sense of tranquility mixed with adventure, inviting viewers to explore this unique experience.

but if you want to mention text over lay don't put ""

don't put commas , anywhere in the prompt
```

---

### 💡 **Example Output (Generated Prompt):**

```
Create a captivating YouTube thumbnail of @chinmay exploring the busy streets of Bali during sunset 🌅 He is walking with a backpack and camera in hand capturing the golden glow of the sky reflecting on the wet pavement 🏝️ The background shows colorful street lights and local food stalls adding a vibrant and lively atmosphere 🍜 Use dynamic lighting to highlight his silhouette as he walks confidently into the frame 🕶️ Text overlay Explore Bali Like Never Before in bold energetic typography that instantly grabs attention ⚡ The overall feel should inspire wanderlust and excitement for travel lovers 🌍
```
