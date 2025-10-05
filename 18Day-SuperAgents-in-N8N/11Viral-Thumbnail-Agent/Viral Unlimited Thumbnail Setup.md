# 💡 Viral Thumbnail AI Agent using n8n (in Hindi)

This video explains how to build an automated thumbnail generator using an AI agent on the n8n platform, trained on a personal photo model called Lora.

## 🛠️ The 7-Step Process

### **Step 1: Gather Images for Training** 📸

- **Collect Photos:** Gather a set of images of your face (or the subject's face).
- **Quality Check:** Ensure the images have good lighting.
- **Crop & Rename:** Crop the face and rename the images (e.g., "a photo of Chinmay").
- **Create ZIP File:** Compress all images into a single ZIP file.
- **Size Matters:** Be mindful of the file size; larger files take longer to train the Lora model.

### **Step 2: Train Lora Model** 🧠

- **Use Trainer:** Use a Lora trainer tool (like "Ostis Flux DV Lora Trainer").
- **Create Model:** Create a new model (e.g., "Chinu") and set it to **Private**.
- **Upload ZIP:** Upload the compressed image ZIP file.
- **Set Trigger Word:** Define a trigger word (e.g., "Chinu" or "@Chinmay"). This word will be used in prompts to activate your custom model.
- **Set Steps:** Set the training steps between 500 and 4000 (2000 is used as an example).
- **Hugging Face Integration:**
  - Create a new **private** model repository on Hugging Face (HF).
  - Copy the repository ID (e.g., `Chinmay/Chinu-Thumbnail`) and paste it into the "HF Repo ID" field.
  - Generate an **Access Token** from your HF settings (remember to save it!) and paste it into the "HF Token" field, ensuring all **User Permissions** are on.
- **Start Training:** Start the training process. The estimated cost is low (around $2 to $5).

### **Step 3: Test Lora Model** ✅

- **Access Model:** After training (takes about 15-20 minutes), find your model on the platform's dashboard.
- **Test Prompt:** Use the trigger word in a prompt (e.g., "Portrait of **@Abhijeet** in a Superman outfit") and execute the run.
- **Verify:** Check that the generated image uses your trained face/style correctly.

### **Step 4: Create n8n Workflow (Backend)** ⚙️

1.  **Start Node:** Use a **WebHook** trigger node (instead of Chat Trigger).
    - Set the Method to **POST**.
    - Set the Path.
2.  **AI Agent (Create Prompt):** Add an **AI Agent** node to generate a detailed, viral-optimized image prompt.
    - **System Message:** The prompt must include instructions to **always use the trigger word** (e.g., `@Chinmay`) for the person in the prompt, and to return **just the prompt** (no emojis, commas, or extra text).
    - **Input:** Connect the input to the WebHook's query.
3.  **HTTP Request (Create Thumbnail):** Add an **HTTP Request** node to call the external API (Replicate) for image generation.
    - **Import cURL:** Get the cURL from your trained model's API section on the platform (Replicate) and import it.
    - **API Token:** Replace the placeholder API token in the header with your actual Replicate API token.
    - **Prompt Input:** Replace the static prompt in the JSON body with an **Expression** that pulls the generated prompt from the **AI Agent** node.
4.  **HTTP Request (Get Image):** Add a second **HTTP Request** node to download the image.
    - **URL Input:** Use an **Expression** to get the image URL from the first HTTP Request node's output.
5.  **Respond to Webhook:** Add a **Respond to Webhook** node to send the result back to the frontend.

### **Step 5: Test the Workflow** 🧪

- Run an end-to-end test with a new prompt (e.g., "A man finding treasure in a jungle Mr. Beast style thumbnail").
- Verify that the image is successfully generated and downloaded.

### **Step 6: Develop a Simple Frontend** 💻

- Use a no-code tool (like Bolt or Lovable) to create a simple web interface.
- The frontend should have:
  - A text input bar for the query.
  - A "Send" or "Generate Thumbnail" button.
  - A section to display the generated thumbnail.
  - A **Download Thumbnail** button.
- **Integration:** Connect the frontend's send action to your n8n **WebHook** URL (ensure the WebHook is set to the **Production URL**).

### **Step 7: Test the Final Frontend** 🎉

- **Activate Workflow:** Set your n8n workflow to **Active**.
- **Final Test:** Test the workflow directly through the new website to confirm automatic generation and download functionality.
