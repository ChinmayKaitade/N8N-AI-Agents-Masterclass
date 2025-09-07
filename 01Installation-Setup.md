# 🚀 Step-by-Step Guide to Install & Run n8n Locally

n8n is a powerful workflow automation tool 🔄. Follow this guide to set it up and run it **locally** on your system.

---

## 🛠 1. Install NVM (Node Version Manager)

🔗 [Download NVM for Windows](https://github.com/coreybutler/nvm-windows/releases?utm_source=chatgpt.com)

- Download the latest **`nvm-setup.exe`**
- Install with default settings
- Verify installation in CMD:

```bash
nvm version
```

---

## 📦 2. Install Node.js (Latest LTS via NVM)

- Install the latest LTS Node.js:

```bash
nvm install 18.20.4
```

(or replace with the latest LTS from [Node.js Downloads](https://nodejs.org/en/download/))

- Switch to it:

```bash
nvm use 18.20.4
```

- Verify installation:

```bash
node -v
npm -v
```

---

## 🔑 3. Run Command Prompt as Administrator

- Search for `cmd` → Right-click → **Run as administrator**

---

## ⚡ 4. Install n8n Globally

```bash
npm install -g n8n
```

---

## ▶️ 5. Start n8n

```bash
n8n
```

- Opens at 👉 [http://localhost:5678](http://localhost:5678/)
- Or press **O** in CMD to auto-open in browser

---

## 👤 6. Sign Up / Sign In

- Create an account or log in
- Enter your **email** → receive a **license key**

---

## 🔐 7. Activate License

- Paste the license key when prompted

---

## 🛠 8. Fix License Activation Error (if any)

```bash
n8n license:clear
n8n start
```

---

## 🎉 9. Done!

Now n8n is ready to use for **free** at 👉 [http://localhost:5678](http://localhost:5678/) 🚀

---

## 📌 Summary

✅ Install **NVM**
✅ Install **Node.js LTS**
✅ Install **n8n**
✅ Run & Activate License
✅ Fix errors if needed
