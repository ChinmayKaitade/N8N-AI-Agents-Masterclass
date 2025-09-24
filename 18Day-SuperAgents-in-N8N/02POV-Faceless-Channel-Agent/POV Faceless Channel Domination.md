# 🚀 Automated Viral POV Video Generator AI Agent (n8n Workflow)

This README outlines an n8n workflow for creating an automated AI agent capable of generating viral Point-of-View (POV) style videos. Learn how to leverage AI tools to automate content creation for platforms like Instagram and YouTube.

---

## ✨ Introduction

This project demonstrates building an AI-powered automation workflow using n8n to generate unique POV videos. The goal is to create a "content machine" that can produce engaging videos, potentially leading to significant audience growth and monetization.

---

## 🎯 Features

* **Automated Content Generation:** From idea to final video, the entire process is automated.
* **Dynamic Prompt Creation:** Generates detailed video prompts based on a simple user idea.
* **AI-Powered Image Generation:** Creates high-quality visual content.
* **AI-Powered Video Animation:** Animates static images into dynamic video clips.
* **Integrated Workflow:** Connects various AI services and tools seamlessly using n8n.
* **Automated Publishing/Distribution:** Automatically uploads generated videos to Google Drive and sends notification emails.

---

## 🛠️ Technologies & Tools Used

* **n8n:** Workflow automation platform.
* **OpenAI (GPT-4.1):** For intelligent prompt generation.
* **Replicate:**
    * **Flux 1.1 Pro Ultra (Image Generation):** Creates images from text prompts.
    * **Kling 1.6 Standard (Video Generation):** Animates images into videos.
* **Google Drive:** For storing generated videos.
* **Gmail:** For sending automated notifications.

---

## ⚙️ Workflow Overview (Step-by-Step)

The n8n workflow is structured as follows:

1.  **💡 Idea Submission (n8n Form Trigger)**
    * A simple form collects the initial video idea (e.g., "Waking up during World War 3 in 2050").

2.  **📝 Prompt Generation (OpenAI Node)**
    * The submitted idea is fed to an OpenAI model (e.g., GPT-4.1).
    * This model generates a detailed, descriptive prompt suitable for image and video creation, often in JSON format.

3.  **🖼️ Image Generation (Replicate API via HTTP Request Node)**
    * The detailed prompt is sent to a Replicate image generation model (e.g., Flux 1.1 Pro Ultra).
    * The model generates a high-quality image URL based on the prompt.
    * *(Note: This step involves API integration and handling Replicate API tokens.)*

4.  **⏳ Wait Node**
    * A wait node (e.g., 2.5 minutes) is crucial here to ensure the subsequent video generation process has enough time to complete, preventing "null" outputs.

5.  **🎥 Video Generation (Replicate API via HTTP Request Node)**
    * The generated image URL and the detailed prompt are passed to a Replicate video generation model (e.g., Kling 1.6 Standard).
    * This model animates the image into a short video clip.
    * *(Note: This also involves API integration and Replicate API tokens.)*

6.  **📊 Retrieve Data (HTTP Request + Set Node)**
    * After the video is generated, an HTTP GET request is made to Replicate's prediction endpoint using the generated prediction ID to retrieve the final video URL.
    * A `Set` node is used to extract and simplify the video URL for further use.

7.  **🚀 Final Video (HTTP Request Node)**
    * Another HTTP request node is used to fetch the final video file content from the retrieved URL.

8.  **☁️ Upload to Google Drive (Google Drive Node)**
    * The final video file is automatically uploaded to a specified folder in Google Drive.

9.  **📧 Send Notification (Gmail Node)**
    * An email is sent to a designated recipient (e.g., the team or creator) containing the link to the newly generated video.

---

## 💰 Cost Analysis (Estimates)

Based on the tutorial's examples (as of the video's creation date):

* **Image Generation (Replicate):** ~ $0.07 per image (approx. 14 images for $1).
* **Video Generation (Replicate - Kling 1.6 Standard):** ~ $1 for a 20-second video (approx. 4 x 5-second videos for $1).

**Estimated Daily Cost:**
If generating one 5-second video daily (1 image + 1 video):
* Image: ₹6 (approx.)
* Video: ₹21 (approx.)
* **Total daily:** ~ ₹27-30
* **Total monthly:** ~ ₹900
* **Total yearly:** ~ ₹10,800

The creator emphasizes that this is an "approachable" investment, especially if the content performs well.

---

## ⚠️ Important Considerations & Tips

* **Initial Investment:** Be prepared for a small monetary investment for API credits on platforms like Replicate. Free tools may not offer the same quality or flexibility.
* **Realistic Expectations:** Viral success is not guaranteed. Focus on consistent, quality content and unique ideas.
* **Market Saturation:** The "POV" video niche can be saturated. Innovate with fresh concepts.
* **API Token Management:** Securely manage your API tokens for Replicate and other services.
* **Model Selection:** Explore various image and video generation models on Replicate (or Hugging Face) to find the best balance of cost and quality for your needs. Check pricing carefully.
* **Workflow Renaming:** Always rename your n8n nodes for clarity and to avoid confusion in complex workflows.
* **Error Handling (Wait Nodes):** Use `Wait` nodes, especially after video generation, to ensure the process completes before attempting to retrieve results, preventing "null" outputs.

