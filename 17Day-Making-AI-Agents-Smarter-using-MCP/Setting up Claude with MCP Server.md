# **Setting Up the Claude App for Integrations (MCP)** ⚙️

The Claude Desktop application allows you to connect to external tools and services, such as the N8N workflows we discussed, through a configuration file.

### **Step 1: Access Developer Settings** 👨‍💻

- First, open the Claude Desktop application on your computer.
- **On a Mac**: Click on the "Claude" menu in the top menu bar, then select **Settings**.
- **On a Windows PC**: Click on the "hamburger" menu (≡) in the top-left corner of the app window, go to **File**, and then **Settings**.
- From the left-hand menu in the settings window, select the **Developer** tab.

### **Step 2: Edit the Configuration File** ✍️

- In the Developer settings, you will find an **"Edit Config"** button. Click on it.
- This will open a file named `claude_desktop_config.json` in a text editor (like VS Code or Notepad). This is where you will add your external connections.
- The file's location is typically:
  - **Mac**: `~/Library/Application Support/Claude/claude_desktop_config.json`
  - **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

### **Step 3: Add Your MCP Server Configuration** 🌐

- In the `claude_desktop_config.json` file, you will define the external MCP server you want to connect to. The configuration is a JSON object.
- The `mcpServers` object contains key-value pairs where the key is a name you give to your server, and the value is its configuration.
- Here is a common structure for connecting to a remote server, like the N8N workflow from the videos:

<!-- end list -->

```json
{
  "mcpServers": {
    "my-n8n-server": {
      "command": "npx",
      "args": ["mcp-remote", "https://your-n8n-production-url.com"]
    }
  }
}
```

- **Note:** You can also add headers for API keys, as seen in the video demonstrations for the N8N setup.

### **Step 4: Save and Restart the App** ✅

- After adding your server configuration, **save the `claude_desktop_config.json` file**.
- It is crucial to **completely quit and restart the Claude Desktop application** for the changes to take effect. Simply closing the window is not enough, as the app may continue to run in the background.
  - **Mac**: Right-click the Claude icon in the menu bar and select "Quit."
  - **Windows**: Right-click the Claude icon in the system tray and select "Quit."
- When you reopen Claude, it will connect to the new MCP server.

Once the connection is successful, a new "Search & Tools" button (often a hammer icon) will appear in the chat window, and you will see your N8N tools listed and ready to use. This allows the Claude AI to leverage your external workflows to answer questions and perform actions. 🚀
