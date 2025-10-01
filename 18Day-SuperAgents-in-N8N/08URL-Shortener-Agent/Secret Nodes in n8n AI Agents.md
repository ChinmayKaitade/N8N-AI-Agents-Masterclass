# 💡 Key Takeaway: The 4 Powerhouse Nodes in n8n

The focus is on combining four essential n8n nodes to build a **URL shortener**, highlighting that **learning individual nodes is more valuable than just copying a workflow**.

| Node                   | Purpose                                                                                                                 | Action in Workflow                                                                                              |
| :--------------------- | :---------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| **1. Webhook** 🌐      | Acts as a **trigger** for the workflow, receiving data from an external source (like a form submission from a website). | Receives the **long URL** from the custom-built website.                                                        |
| **2. HTTP Request** ⚙️ | Makes calls to **external APIs** (Application Programming Interfaces).                                                  | Connects to the **tinyurl.com API** to create the shortened URL.                                                |
| **3. Set** 🛠️          | Used to **modify, manipulate, add, or subtract data** within the workflow.                                              | **Filters and extracts** only the newly created **tiny URL** from the bulky API response.                       |
| **4. Code** 💻         | Allows you to execute custom **JavaScript code** for complex logic, data manipulation, or formatting.                   | **Formats the final output** (the tiny URL) with a custom message (e.g., "Congratulations, this is your URL!"). |

---

## 🛠️ The URL Shortener Project Walkthrough

The project demonstrates building a **functional URL shortener** in n8n and connecting it to a simple website created using **Bolt**.

### 1. External API Integration (tinyurl.com)

- Sign up for a **tinyurl.com account** and **generate an API token** to use their service.
- The API call details (like the **POST** method and endpoint URL) are obtained from the tinyURL **Open API documentation** and imported into the HTTP Request node using the **Import cURL** feature.
- Authentication is configured using a **Generic Credential** with **Bearer Auth** type and the API token.
- In the HTTP Request node, the URL to be shortened is dynamically mapped from the **Webhook's incoming data**.

### 2. Data Refinement and Custom Output

- The **Set node** is crucial for cleaning up the data, as the HTTP Request returns a lot of unnecessary information. You simply drag and drop the desired `tiny_url` field into the Set node's value to isolate it.
- The **Code node** is used to create a user-friendly output, which is especially helpful if you need to present the final result in a specific way.

### 3. Front-end Connection (Website)

- The **Webhook URL** (specifically the **Production URL** when ready) is given to the Bolt website builder as the destination for the user's input.
- The final **Response to Webhook** node sends the structured result (created by the Code node) back to the website to display to the user, completing the full process.

---

## 🌐 Live URL Shortener Application

👉 [Dark Theme URL Shortener](https://dark-theme-url-short-vs86.bolt.host/)

### 🎨 Interface Overview

- The app uses a **modern dark-theme UI** with a clean and minimal design.
- There is a **single input field** where users can paste any long URL.
- A **shorten button** is placed next to or below the input field for triggering the process.
- Once processed, the shortened URL is displayed clearly in a result box or section.
- To enhance user experience, the final message appears with a **celebratory “Congratulations”** note along with the shortened link.

### ⚙️ Working Process

1. **User Input:** The user pastes a long URL into the input field.
2. **Webhook Trigger:** On clicking the shorten button, the URL is sent to the **n8n Webhook node**.
3. **API Call:** The **HTTP Request node** sends this URL to the **tinyurl.com API**.
4. **Data Refinement:** The **Set node** isolates the shortened link from the API response.
5. **Formatting Output:** The **Code node** wraps the shortened link inside a friendly message.
6. **Response:** The shortened link is displayed on the website, ready to copy and share.

---

## 🚀 Final Structure & Next Steps

- **Workflow Order:** **Webhook** → **HTTP Request** → **Set** → **Code** → **Respond to Webhook**.
- **Result:** The live application allows users to paste any long URL and instantly receive a shortened version with a polished output message.
- **Monetization Idea:** This can be scaled by adding features like user accounts, click analytics, or advertisements around the app.
