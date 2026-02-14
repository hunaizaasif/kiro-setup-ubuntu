# kiro-setup-ubuntu

📺 Watch the Video: Click here to watch the full step-by-step tutorial


🎁 Phase 1: Get Your Free Kiro Credits
Step 1: Download Kiro IDE
Visit kiro.dev and download the application for your platform.

Step 2: Sign Up & Login
Open Kiro IDE
Create a new account or sign in
✨ You'll automatically receive 500 free credits!
⚠️ Important: Keep Kiro IDE logged in throughout this setup process.

Linux / Ubuntu (Bash)
Before starting the Kiro Gateway server, set the required environment variables in your terminal:

# Set the path to your Kiro credentials JSON file
export KIRO_CREDS_FILE=~/.aws/sso/cache/kiro-auth-token.json

# Set your super-secret proxy API key
export PROXY_API_KEY=my-super-secret-password-123

⚠ Note: These export commands only last for the current terminal session. To make them permanent, you can add them to your ~/.bashrc or ~/.zshrc.

tep 2: Create Configuration File
For Linux(ubuntu) users:
Open the ubuntu terminal.

Create or edit the file at: ~/.claude-code-router/config.json by paste the following configuration:
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
Note: Ensure the api_key matches the PROXY_API_KEY you set in Phase 2. The model name claude-sonnet-4-5 corresponds to the models provided by the Kiro Gateway.

Phase 3: Set Up Claude Code Router
The Claude Code Router wraps the official Claude CLI and redirects requests to your local Kiro gateway.

Step 1: Install Required Packages
npm install -g @anthropic-ai/claude-code
npm install -g @musistudio/claude-code-router

rm -rf kiro-openai-gateway

git clone https://github.com/Jwadow/kiro-openai-gateway.git

cd kiro-openai-gateway

pip3 install -r requirements.txt

ya ye

pip3 install -r requirements.txt --break-system-packages

cp .env.example .env

nano .env


# KIRO_CREDS_FILE="~/.aws/sso/cache/kiro-auth-token.json" uncomment this line in .env file.

Note: Open the terminal on this directory kiro-openai-gateway where we have all the kiro code base and run this command python main.py.If the server is successfully running so it's means that your .env file is loaded successfully and you don't need to implement step Step 5: Setup Variables to set this 2 environment variable manually KIRO_CREDS_FILE and PROXY_API_KEY.
Step 6: Start the Gateway Server
python3 main.py



Success Indicator: You should see:

Server running at http://localhost:8000
📌 Note: To check if the gateway is running, open your browser and go to:

http://localhost:8000

You should not use 0.0.0.0 in the browser, as it is only a server binding address.

This site can’t be reached
The webpage at http://0.0.0.0:8000/ might be temporarily down or it may have moved permanently to a new web address.
ERR_ADDRESS_INVALID
You should convert this http://0.0.0.0:8000 url into your localhost by running python main.py --host 127.0.0.1 command in the terminal and close the old one. Then run this on the browser.

http://127.0.0.1:8000/

It'll show something like this: {"status":"ok","message":"Kiro Gateway is running","version":"2.0-rc.1"} so it means that server is running successfully in the localhost.

You should stopped this server once checked it's working or The server must stay running.



