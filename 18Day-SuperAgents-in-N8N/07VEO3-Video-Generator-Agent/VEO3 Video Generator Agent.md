# 🎬 Project: The Cheapest VEO Killer AI Agent (N8N Workflow) 🤖

This powerful N8N workflow uses AI to generate high-quality, unique stock videos with automatically generated **sound effects (SFX) and audio**. The goal is to create a low-cost service for creators (around $1.5 per video).

---

### 💡 Phase 1: Form Input and Video Prompt Generation

This initial phase captures user preferences and creates a dynamic, detailed text prompt for the video generation model.

1.  **Form Trigger (Input):** 📥 A simple form collects all video specifics: **Who** (Man/Woman), **What** (Action like Running/Singing), **Location**, **Nationality**, and **Extra Details**.
2.  **AI Agent (Generate Prompt):** 📝 All form data is passed to an AI model (like OpenAI 4.1 Mini).
    - **Key Instruction:** The AI is instructed to create a **"Stock Video Style"** prompt that **excludes** any reference to voice or people talking to ensure a clean video canvas.

---

### ⚙️ Phase 2: Video Creation & Retrieval

This phase handles the technical creation of the video file itself.

1.  **Video Creation (HTTP Request to Replicate):** 🎥 The prompt is sent to an external service, **Replicate.com** (using the affordable _ByteDance DanceOne Light_ model), configured via a cURL import and Replicate API Token.
2.  **Wait Node:** ⏳ A **40-second Wait Node** is essential to ensure the external service finishes processing the video before the next steps try to retrieve it.
3.  **Retrieve & Convert to Binary (HTTP Requests):** The video output is retrieved and immediately converted into a **binary file format**, a necessary step for the upcoming AI analysis.

---

### 🧠 Phase 3: Video Analysis (The Crucial Step)

This is the most unique step, where the video's content is deeply analyzed to determine the correct sounds and ambiance.

1.  **API Setup (Gemini 2.5):** 🚀 The video is analyzed by the **Gemini 2.5** model because of its high capability to understand video content.
    - **Goal:** Determine what **SFX** (sound effects) are needed based on the visuals (e.g., footsteps in a gym, beeping in a hospital).
2.  **Create File & Analyze (HTTP Requests):** The binary video is uploaded to the Gemini API. A POST request then sends the prompt: **"Describe what's going on in the video in extreme detail,"** receiving a detailed description of the scene and action.
3.  **Error Handling:** A path is added to allow the workflow to **retry the analysis** if the initial attempt fails.

---

### 🎵 Phase 4: Audio Prompt Generation

This phase uses the detailed video description to create a specific, structured prompt for the final sound generation.

1.  **AI Agent (SFX & Audio Prompt Generator):** The detailed description from Phase 3 is input into a new AI Agent.
    - **System Prompt:** Instructs the AI to act as an "SFX and Audio Prompt Generator" that studies the ambiance and subject's actions.
    - **Goal:** Generate two distinct outputs required for the final audio model: **Caption** (general sound description) and **COT (Chain of Thought)** (a detailed, step-by-step sound plan).
2.  **Code Node (Separation):** 💻 A `Code Node` is used to separate the AI's combined text output into the two distinct **Caption** and **COT** fields, ensuring they map correctly.

---

### 🎤 Phase 5: Final Video Generation with Audio

The final phase combines the original video with the custom-generated audio to produce the finished asset.

1.  **Create Audio Video (HTTP Request to Replicate - Think Sound):** This is the final POST request to a third-party audio generation model on Replicate, specifically the **Think Sound** model.
    - **Mapped Inputs:** The original video (binary), the **COT**, and the **Caption** are all sent to the Think Sound model.
2.  **Retrieve Final Video (HTTP Request):** A final GET request retrieves the URL for the completed video, which now includes the high-quality, generated SFX and audio.
3.  **Storage Tip:** The video files on Replicate are only temporary. You must link a **Google Drive** or other storage node at the end of the workflow to save the videos permanently. 💾
