### **Airtable Credentials in n8n: A Setup Guide** 🔑

This guide will walk you through the steps to connect your **Airtable** account to **n8n** using an access token. Follow these steps to get your automation journey started! 🚀

---

### **Step-by-Step Setup Guide**

1.  **Add New Credential in n8n**

    - In your n8n workspace, navigate to the **Credentials** section.
    - Click on **"New Credential"** and search for **Airtable**.
    - Give your credential a clear name, like "My Airtable Connection," for easy identification.

2.  **Generate Your Airtable Access Token**

    - Go to Airtable's developer hub to create a new personal access token.
    - Give the token a unique name so you know what it's for.

3.  **Define Scopes for Your Token**

    - In Airtable, you need to grant your token specific permissions, or "scopes." These tell the token what it's allowed to do.
    - The video shows which scopes are necessary to connect with n8n. Make sure to add the correct ones to your token.

4.  **Grant Access to Your Bases**

    - Choose which bases this token will have access to. You can either grant it access to **all** bases in your workspace or select a **specific base** for added security.

5.  **Connect to n8n**
    - Once you've created the token in Airtable, copy it.
    - Go back to the n8n credential setup page and paste the token into the designated field.
    - Save the credential. Your Airtable account is now securely connected to n8n! 🎉

---

### **`README.md` for Airtable Credential Setup**

### **Airtable Credentials in n8n 🔑**

This guide provides a quick setup reference for connecting Airtable to n8n.

### **✨ What This Setup Does**

This setup allows you to build powerful automation workflows that can:

- Read and write data from your Airtable bases. 📝
- Create new records, update existing ones, and delete records. 🗑️
- Trigger workflows based on changes in your Airtable data. 🔔

### **🛠️ Requirements**

- An n8n account or self-hosted instance.
- An Airtable account.

### **✅ Final Steps**

Once you have followed the steps above and saved your credentials, you can begin using the **Airtable node** in your workflows. It's time to automate all the things! 🚀
