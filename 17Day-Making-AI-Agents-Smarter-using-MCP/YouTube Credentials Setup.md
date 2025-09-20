# **Part 1: Google Cloud Setup** ⚙️

This is where you'll get the **Client ID** and **Client Secret** needed for N8N.

1.  **Create a Project**: Go to the **Google Cloud Console**. In the top menu, click the project dropdown and select **New Project**. Give it a name like "N8N YouTube."

2.  **Enable the YouTube API**:

    - In the Google Cloud Console, navigate to the **APIs & Services Dashboard**.
    - Click **"+ Enable APIs and Services"**.
    - Search for **"YouTube Data API v3"** and select it.
    - Click the **Enable** button.

3.  **Configure OAuth Consent Screen**:

    - From the APIs & Services sidebar, go to **OAuth consent screen**.
    - Select **"External"** as the User Type and click **Create**.
    - Fill in the required app information, including the **App name** and a **User support email**.
    - On the **"Scopes"** screen, you can click **"Add or remove scopes"** and search for `YouTube`. Select the scopes that match your needs. For general access, `.../auth/youtube.readonly` is a good starting point.
    - On the **"Test users"** screen, add your Google account as a test user.

4.  **Create Credentials**:
    - From the APIs & Services sidebar, go to **Credentials**.
    - Click **"+ Create Credentials"** and select **"OAuth client ID"**.
    - Choose **"Web application"** as the Application type.
    - In the **"Authorized redirect URIs"** field, you need to get the URL from your N8N instance. Go to your N8N, create a new workflow, add a YouTube node, and click "New Credential." A URL will be provided. Copy this URL and paste it here.
    - Click **Create**. You will be given your **Client ID** and **Client Secret**. **Copy both.**

---

### **Part 2: N8N Setup** 🔗

Now, use the credentials you just obtained to set up the connection in N8N.

1.  **Add YouTube Node**: In your N8N workflow, add a YouTube node from the list of integrations.
2.  **Create New Credential**: Click on the credential field in the node and select **"New Credential."**
3.  **Enter Credentials**: A new window will appear.
    - In the **OAuth2 Grant Type** dropdown, select **"Authorization Code."**
    - Paste your **Client ID** and **Client Secret** into the corresponding fields.
    - Click **"Connect"**.
4.  **Authorize Access**: A Google sign-in window will pop up. Log in with the Google account you added as a test user in Part 1. Grant N8N the necessary permissions.

Your YouTube credentials are now successfully configured in N8N.

This is a common security message from Google that means the app you're trying to connect isn't publicly verified by them. Don't worry, you don't need to publish your app to fix it. You just need to tell Google that you trust this specific app by adding your email to a list of "test users."

-----

### **How to Fix the "Access Blocked" Error** 🔒

You must configure your app's OAuth Consent screen in the Google Cloud Console to allow your account to connect.

1.  **Go to Your Google Cloud Project**: In the Google Cloud Console, navigate to the project you created for your N8N credentials.
2.  **Open OAuth Consent Screen**: In the sidebar, go to **APIs & Services** and then select **OAuth consent screen**.
3.  **Add Your Account as a Test User**:
      * Scroll down to the section titled **"Test users"**.
      * Click **"Add users."**
      * Enter the **exact email address** of the Google account you are trying to use with N8N.
      * Click **"Save."**
4.  **Re-attempt Connection**: Go back to N8N and try to connect your Google account again. The error should no longer appear, and you will be able to grant the necessary permissions.

\<br\>
This video explains why the "Access Blocked" error occurs and provides a step-by-step solution using the Google Cloud Console.
[Fixing Google API Access Blocked Error: n8n](https://www.youtube.com/watch?v=Ysmt_qsZiXk)
http://googleusercontent.com/youtube_content/6