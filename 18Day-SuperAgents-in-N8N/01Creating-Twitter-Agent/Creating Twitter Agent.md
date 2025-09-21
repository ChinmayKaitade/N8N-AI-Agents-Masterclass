## 🐦 Building a Twitter Trend Tracking AI Agent with n8n! 🚀

This Project demonstrates how to create a simple yet powerful AI agent using n8n to track trending posts on Twitter (now X). This agent can be built with just four nodes and is incredibly useful for content creation, market research, and staying updated on real-time trends.

---

### 🌟 Agent Capabilities:

* **Searches Trending Posts:** Given a search term, the agent fetches top-trending posts on X.
* **Data Organization:** Organizes key metrics like likes, retweets, views, and bookmark counts.
* **URL Retrieval:** Provides direct URLs to the trending posts for quick access.
* **Filtering & Sorting:** Allows you to filter and sort results based on various metrics like views and bookmark counts, making it easy to find the most engaging content.
* **Simple & Efficient:** Built with only four nodes, making it easy to set up and understand, even for beginners.

---

### 🛠️ Key Components & How it Works:

1.  **Chat Message Trigger:**
    * Initiates the workflow when a user inputs a search term (e.g., "n8n AI agents"). 

2.  **HTTP Request Node (Twitter API Integration):**
    * Connects to a third-party Twitter API (like `twitterapi.io`) to fetch data.
    * **Caution:** The presenter highlights potential security concerns with `twitterapi.io` (BitDefender blocking it) and advises caution, especially when dealing with payment information. 
    * **Free Credits:** The recommended API provides 100,000 free credits, which is ample for testing and initial usage. 
    * **Configuration:**
        * **Method:** `GET` request. 
        * **URL:** A specific API endpoint for searching Twitter posts. 
        * **Query Parameters:**
            * `query_type`: Set to `top` to retrieve top-trending results.
            * `query`: Dynamically takes the search term from the Chat Message trigger. 
        * **Headers:** Includes an `X-API-Key` for authentication using the API key obtained from `twitterapi.io`. 
        * **Pagination:** Configured to fetch a limited number of pages (e.g., 1-5 pages) to manage API credit consumption. The `response contains next URL` and `respond to next cursor` settings help navigate through search results. =

3.  **Code Node (Data Transformation):**
    * Takes the raw data from the HTTP Request node and transforms it into a structured, organized format. =
    * This ensures that metrics like `like_count`, `retweet_count`, `views`, and `bookmark_count` are clearly identifiable. The video suggests using GPT to quickly generate the code for this transformation. =

4.  **Airtable Node (Data Storage & Visualization):**
    * Connects to an Airtable base to store the processed Twitter data. =
    * **Table Setup:** Requires specific columns in Airtable: `Tweet ID`, `URL`, `Content`, `Likes`, `Retweets`, `Quotes`, `Views`, `Bookmark Count`, `Date`, and `Rating` (optional). =
    * **Mapping:** Maps the structured data from the Code node to the corresponding Airtable columns. =
    * **Dynamic Sorting:** Airtable's filtering and sorting capabilities are used to arrange the data (e.g., by `Views` or `Bookmark Count` in descending order) to easily identify the most popular content. =
    * **Why Airtable?** The presenter emphasizes Airtable's dynamic capabilities over Google Sheets for building AI agents. =
---

### 💡 Additional Insights & Tips:

* **API Security:** Always be cautious when using third-party APIs, especially if you're inputting sensitive information or payment details.
* **Credit Management:** Limit the number of pages fetched in the HTTP Request node to conserve API credits.
* **Content Strategy:** This agent is highly valuable for content creators and marketers to understand what's trending and adapt their content strategy accordingly.
* **Learning Airtable:** The presenter recommends learning Airtable thoroughly if you plan to build AI agents, suggesting their member-exclusive content for a deep dive.

---

### 🔗 Workflow in Action:

Imagine typing "AI trends 2025" into your n8n chat trigger. The agent will then:
1.  Query the Twitter API for top posts related to "AI trends 2025".
2.  Process the raw Twitter data, extracting key information.
3.  Store this organized data in your Airtable base.
4.  You can then go to your Airtable base, sort by "Views" or "Bookmark Count," and instantly see the most popular tweets, along with their links, to understand the current discourse and gather insights.
