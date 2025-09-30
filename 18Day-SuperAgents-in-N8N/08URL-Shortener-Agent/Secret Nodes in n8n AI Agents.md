Got it 👍 Here’s your cleaned-up and polished version without timestamps and YouTube links:

---

## 💡 Key Takeaway: The 4 Powerhouse Nodes in n8n

The focus is on combining four essential n8n nodes to build a **URL shortener**, highlighting that **learning individual nodes is more valuable than just copying a workflow**.

| Node                   | Purpose                                                                                                                 | Action in Workflow                                                                                              |
| :--------------------- | :---------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| **1. Webhook** 🌐      | Acts as a **trigger** for the workflow, receiving data from an external source (like a form submission from a website). | Receives the **long URL** from the custom-built website.                                                        |
| **2. HTTP Request** ⚙️ | Makes calls to **external APIs** (Application Programming Interfaces).                                                  | Connects to the **tinyurl.com API** to create the shortened URL.                                                |
| **3. Set** 🛠️         | Used to **modify, manipulate, add, or subtract data** within the workflow.                                              | **Filters and extracts** only the newly created **tiny URL** from the bulky API response.                       |
| **4. Code** 💻         | Allows you to execute custom **JavaScript code** for complex logic, data manipulation, or formatting.                   | **Formats the final output** (the tiny URL) with a custom message (e.g., "Congratulations, this is your URL!"). |

---

## 🛠️ The URL Shortener Project Walkthrough

The project demonstrates building a **functional URL shortener** in n8n and connecting it to a simple website created using **Bolt**.

### 1. External API Integration (tinyurl.com)

* Sign up for a **tinyurl.com account** and **generate an API token** to use their service.
* The API call details (like the **POST** method and endpoint URL) are obtained from the tinyURL **Open API documentation** and imported into the HTTP Request node using the **Import cURL** feature.
* Authentication is configured using a **Generic Credential** with **Bearer Auth** type and the API token.
* In the HTTP Request node, the URL to be shortened is dynamically mapped from the **Webhook's incoming data**.

### 2. Data Refinement and Custom Output

* The **Set node** is crucial for cleaning up the data, as the HTTP Request returns a lot of unnecessary information. You simply drag and drop the desired `tiny_url` field into the Set node's value to isolate it.
* The **Code node** is used to create a user-friendly output, which is especially helpful if you need to present the final result in a specific way.

### 3. Front-end Connection (Website)

* The **Webhook URL** (specifically the **Production URL** when ready) is given to the Bolt website builder as the destination for the user's input.
* The final **Response to Webhook** node sends the structured result (created by the Code node) back to the website to display to the user, completing the full process.

---

## 🚀 Final Structure & Next Steps

* **Workflow Order:** The complete, production-ready workflow is: **Webhook** (trigger) → **HTTP Request** (API call) → **Set** (filter data) → **Code** (format message) → **Respond to Webhook** (send result back).
* **Result:** The final result is a custom website that shortens a long URL and displays a confetti-accompanied "Congratulations" message with the new tiny URL.
* **Monetization Idea:** Once hosted, the URL shortener can potentially be monetized through advertising.

---

Do you want me to also **make a simplified diagram/flowchart** of this workflow (Webhook → HTTP Request → Set → Code → Respond) for quick visualization?
