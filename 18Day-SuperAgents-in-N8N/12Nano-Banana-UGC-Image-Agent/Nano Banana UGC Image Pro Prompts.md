# 🍌 Nano Banana UGC AI Agent

> 🧠 An intelligent automation workflow that **analyzes images, generates UGC-style prompts**, and seamlessly integrates with **FAL AI’s Nano Banana model** to create authentic, influencer-style visuals.

---

## 🚀 Overview

**Nano Banana UGC AI Agent** is designed to automate the **User-Generated Content (UGC)** creation process using AI.
It analyzes product or character images, extracts key details, and then generates **realistic, casual UGC-style image prompts** ready for AI-based content generation via **[FAL AI Nano Banana Model](https://fal.ai/)**.

This agent is perfect for:

- 📸 Product marketing teams
- 🎬 Content creators and UGC designers
- 🧩 AI-based visual automation workflows

![Nano Banana UGC AI Agent](./UGC%20Image%20PRO.png)

---

## ⚙️ Workflow Overview

The workflow consists of **three main stages**:

### **1️⃣ Upload Image**

Upload your product or character image to **[IMGBB](https://imgbb.com/)** to get a public image URL.

**IMGBB API:**
`https://api.imgbb.com/`

You’ll receive a JSON response with a hosted image link like:

```json
{
  "data": {
    "image": {
      "url": "https://i.ibb.co/example/image.png"
    }
  }
}
```

---

### **2️⃣ Image Analysis**

Analyzes the uploaded image to identify:

- Whether it shows a **product**, **character**, or **both**
- Extracts **brand**, **color scheme**, **font styles**, and **visual descriptions**

**🧩 Image Analysis Prompt:**

```JavaScript
Image Analysis Instructions

Primary Task: Analyze the given image to determine if it shows a product, character, or both
Output Format: Return analysis in YAML format only (no explanations or additional comments)
For Product Images:

brand_name: Brand name shown or inferable from image
color_scheme: List each prominent color with:

hex: Hex code value
name: Descriptive color name


font_style: Font characteristics (serif/sans-serif, bold/thin, etc.)
visual_description: 1-2 sentences describing what's visible (exclude background)


For Character Images:

character_name: Character name if visible or inferable
color_scheme: List each prominent color with:

hex: Hex code value
name: Descriptive color name


outfit_style: Description of clothing, accessories, or notable features
visual_description: 1-2 sentences describing character appearance (exclude background)


For Images Containing Both: Provide both product and character descriptions using the respective fields above
Important: Return only the YAML output with no additional text
```

**✅ Output:**
Returns structured YAML describing the image with accurate visual metadata.

---

### **3️⃣ Prompt Generator**

The AI creates a **UGC-style image prompt** that visually replicates the product or character in **casual, authentic environments**.

It ensures:

- Accurate text and brand representation
- Natural, unpolished iPhone photo aesthetics
- Candid, influencer-style realism

---

## 🧠 Prompt Generation Flow

### **User Message Template**

```JavaScript
Primary Objective: Create 1 image prompt following system guidelines
Accuracy Requirements:

Depict reference image as accurately as possible
Ensure all text elements are reproduced precisely
Maintain visual fidelity to original


Input Sources:

User Instructions:{{ $('On form submission').item.json.Prompt }}
Reference Image Description: {{ $json.content }}
Aspect Ratio: User's preferred ratio (infer from message; default to vertical if unspecified)


Process Steps:

Analyze user's prompt requirements
Review reference image description thoroughly
Determine appropriate aspect ratio
Use Think tool to verify output before finalizing


Output: Single, comprehensive image generation prompt that accurately captures all specified elements
```

---

### **System Message Template**

```JavaScript
System Prompt: Image Prompt Generator

Default Behavior:

If user instructions lack detail: Generate "put this (product) into the scene with the (character)"


UGC Authentic Content Requirements:

When Requested: Use casual UGC-style scenes unless user specifies otherwise
Override: Follow explicit user style/setting requests when provided


Core Task:

Take reference image/product and place into realistic, casual scenes
Simulate everyday content creator/influencer captures


Mandatory UGC Style Elements:

Natural, candid, unpolished appearance
Everyday realism with authentic, relatable settings
Amateur-quality iPhone photo aesthetic
Slightly imperfect framing and lighting
Candid poses with genuine expressions
Visible imperfections (blemishes, messy hair, uneven skin, texture flaws)
Real-world environments as-is (clutter, busy backgrounds)
Text Preservation: All visible product text must be accurate (logos, slogans, packaging claims)
No Fabrication: Never invent extra claims or numbers


Camera Parameters Must Include:

Casual realism descriptors: unremarkable amateur iPhone photos, reddit image, snapchat photo, casual iPhone selfie, slightly uneven framing, authentic share, slightly blurry, amateur quality phone photo


Content Restrictions:

Generate image prompts only (no dialogue/video)
Avoid copyrighted character names in prompts


Output Requirements:

Generate image generation instructions in exact YAML format
Default to vertical aspect ratio if unspecified
Always include both:

image_prompt (stringified YAML with scene details)
aspect_ratio_image ("3:2" or "2:3")




Guidance Standards:

Follow UGC-style casual realism principles
Ensure diversity (gender, ethnicity, hair color) when applicable
Default age range: 21-38 years unless specified
Default to casual real-world environments unless setting specified
Avoid double quotes in image prompts


Good Example Format:
{
  "scenes": [
    {
      "image_prompt": "REPLACE YOUR PROMPT",
      "aspect_ratio_image": "2:3"
    }
  ]
}

Bad Examples to Avoid:

Altering or fabricating product packaging text


Final Output Structure:

Object containing only:

image_prompt → stringified YAML
aspect_ratio_image → "3:2" or "2:3" (default vertical → 2:3)


Quality Control:

Use Think Tool to verify: completeness, text accuracy, UGC realism adherence, image-only outputs
```

---

## 🧩 Integration with FAL AI

Use **[Nano Banana Model](https://fal.ai/models/fal-ai/nano-banana)** or
**[Nano Banana Edit Model](https://fal.ai/models/fal-ai/nano-banana/edit)** for image generation and editing.

### **JSON Payload Example:**

```JavaScript
{
     "prompt": "{{ $json.output.replace(/\"/g, '\\\"').replace(/\n/g, '\\n') }} }}",
     "image_urls": [
       "{{ $('Upload Image').item.json.data.image.url }}"
     ]
}
```

📤 Replace the `prompt` and `image_urls` fields with:

- ✅ Your generated YAML UGC prompt
- ✅ Uploaded IMGBB image URL

---

## 🧩 Example Flow Summary

| Step | Task                | Tool Used    | Output                |
| ---- | ------------------- | ------------ | --------------------- |
| 1️⃣   | Upload Image        | IMGBB        | Hosted image URL      |
| 2️⃣   | Analyze Image       | AI Prompt    | YAML analysis         |
| 3️⃣   | Generate UGC Prompt | Nano Banana  | Realistic prompt      |
| 4️⃣   | Generate Image      | FAL AI Model | Final UGC-style image |

---

## 💡 Example Output (Simplified)

```yaml
image_prompt: >
  candid iPhone photo of a young woman holding a bright yellow "Nano Banana" energy drink can.
  Shot in natural lighting, with authentic messy kitchen background, slightly uneven framing,
  showing real skin texture and casual pose.
aspect_ratio_image: "2:3"
```

---

## 🧩 Tools & Dependencies

| Tool                               | Purpose                    |
| ---------------------------------- | -------------------------- |
| 🧠 **n8n**                         | Workflow automation engine |
| 🖼 **IMGBB API**                    | Image hosting              |
| 🤖 **FAL AI (Nano Banana)**        | AI-based image generation  |
| ⚙️ **JavaScript / JSON Templates** | Dynamic data handling      |

---

## 🎯 Use Cases

- UGC Ad Generation
- Product Lifestyle Visuals
- AI-Driven Brand Marketing
- Influencer Content Mockups

---

## 📚 References

- [FAL AI – Nano Banana Model](https://fal.ai/models/fal-ai/nano-banana)
- [IMGBB API Documentation](https://api.imgbb.com/)
- [n8n Workflow Automation](https://n8n.io/)

---

## 🧾 License

This project is open-source and available for educational or personal use under the **MIT License**.

---

## 🧑‍💻 Author

**Chinmay Kaitade**
💼 MERN Stack & AI Developer
🔗 [Portfolio](https://chinmaykaitadeportfolio.vercel.app/)
🌐 [GitHub](https://github.com/ChinmayKaitade) | [LinkedIn](https://linkedin.com/in/chinmaykaitade)
