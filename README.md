# 🚀 Kiro Setup on Ubuntu (Step-by-Step Copyable Guide)

---

## 📺 Video Tutorial

Watch the full step-by-step tutorial (add your video link here).

---

# 🎁 Phase 1: Get Your Free Kiro Credits

## Step 1: Download Kiro IDE

* Visit: [https://kiro.dev](https://kiro.dev)
* Download for your platform

## Step 2: Sign Up & Login

1. Open Kiro IDE
2. Create a new account or sign in

✨ You’ll automatically receive **500 free credits**

⚠️ Important: Keep Kiro IDE logged in during the entire setup.

---

# 🐧 Linux / Ubuntu Setup

Before starting the Kiro Gateway server, set environment variables.

## Step 1: Set Environment Variables (Temporary)

```bash
# Path to Kiro credentials
export KIRO_CREDS_FILE=~/.aws/sso/cache/kiro-auth-token.json

# Your proxy API key
export PROXY_API_KEY=my-super-secret-password-123
```

⚠️ These only work for the current terminal session.
To make permanent, add them to:

* ~/.bashrc
* ~/.zshrc

---

# ⚙️ Step 2: Create Claude Router Config

## Create config file:

```bash
cat > ~/.claude-code-router/config.json << 'EOF'
{
  "LOG": true,
  "LOG_LEVEL": "debug",
  "Providers": [
    {
      "name": "kiro",
      "api_base_url": "http://localhost:8000/v1/chat/completions",
      "api_key": "my-super-secret-password-123",
      "models": [
        "claude-sonnet-4-5",
        "claude-haiku-4-5",
        "claude-opus-4-5"
      ],
      "transformer": {
        "use": ["openrouter"]
      }
    }
  ],
  "Router": {
    "default": "kiro,claude-sonnet-4-5",
    "think": "kiro,claude-sonnet-4-5",
    "background": "kiro,claude-sonnet-4-5",
    "longContext": "kiro,claude-sonnet-4-5",
    "webSearch": "kiro,claude-sonnet-4-5"
  }
}
EOF
```

📌 Make sure:

* api_key matches PROXY_API_KEY
* Model names are correct

---

# 🔁 Phase 3: Install Claude Code Router

## Step 1: Install Required Packages

```bash
npm install -g @anthropic-ai/claude-code
npm install -g @musistudio/claude-code-router
```

---

# 📦 Clone Kiro Gateway

```bash
rm -rf kiro-openai-gateway

git clone https://github.com/Jwadow/kiro-openai-gateway.git

cd kiro-openai-gateway
```

---

# 🐍 Install Python Requirements

```bash
pip3 install -r requirements.txt
```

If error occurs:

```bash
pip3 install -r requirements.txt --break-system-packages
```

---

# 🔐 Setup .env File

```bash
cp .env.example .env
nano .env
```

Uncomment this line inside `.env`:

```
KIRO_CREDS_FILE="~/.aws/sso/cache/kiro-auth-token.json"
```

---

# ▶️ Run Gateway Server

Run inside the project directory:

```bash
python3 main.py
```

If successful, you should see:

```
Server running at http://localhost:8000
```

---

# 🌐 Verify Server in Browser

Open:

```
http://localhost:8000
```

---

# ❌ If You See 0.0.0.0 Error

Browser error example:

```
http://0.0.0.0:8000
ERR_ADDRESS_INVALID
```

## Fix:

Stop server and run:

```bash
python3 main.py --host 127.0.0.1
```

Then open:

```
http://127.0.0.1:8000
```

Expected response:

```json
{"status":"ok","message":"Kiro Gateway is running","version":"2.0-rc.1"}
```

✅ This means the server is working.

---

# 🛑 Should You Stop the Server?

* ✅ For testing → You can stop it
* 🚀 For real usage → Server must stay running

---

# ✅ Done!

You now have:

* Kiro Gateway running locally
* Claude Router configured
* Local AI routing ready 🎉

---

If you want, I can also generate:

* YouTube version
* Urdu version
* PDF version
* Troubleshooting guide
