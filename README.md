# Claude Code Installation and Setup Guide

Welcome! This guide is designed to help you set up **Claude Code** on your computer. We have written this specifically for beginners, so follow the steps carefully.

This guide covers:
1. Installing necessary prerequisites (Git, Python, Node.js)
2. Installing the official Claude Code tool
3. Setting up **Claude Code Router** to use free AI models (for users without a paid subscription)

---

## Part 1: Prerequisites

Before we install Claude Code, we need to ensure your system has the necessary tools installed. Please download and install the versions appropriate for your Operating System (Windows, macOS, or Linux). **Always choose the stable/LTS (Long Term Support) versions.**

### 1. Git
Git is a version control system used widely in programming and is required for Claude Code to function properly.

**Download:** [https://git-scm.com/downloads](https://git-scm.com/downloads)

**Installation Steps:**
1. Download Git for your operating system
2. Run the installer
3. During installation, you will be asked many configuration questions. **Do not change anything** - just keep clicking "Next" to accept the defaults
4. Complete the installation

**Verify Installation:**

Open your terminal (Command Prompt or PowerShell on Windows, Terminal on Mac/Linux) and run:

```bash
git --version
```

If you see a version number (e.g., `git version 2.43.0`), Git is installed successfully.

---

### 2. Python
Python is a programming language that Claude Code depends on for certain functionalities.

**Download:** [https://www.python.org/downloads/](https://www.python.org/downloads/)

**Installation Steps:**
1. Download the latest stable version for your operating system
2. Run the installer
3. **Important:** Make sure to check "Add Python to PATH" during installation
4. Complete the installation

**Verify Installation:**

In your terminal, type:

```bash
# On Windows
py --version

# On macOS/Linux (if 'py' doesn't work)
python3 --version
```

You should see output showing the Python version number (e.g., `Python 3.12.0`).

---

### 3. Node.js
Node.js is a JavaScript runtime that allows you to run Claude Code on your system.

**Download:** [https://nodejs.org/en/download/current](https://nodejs.org/en/download/current)

**Installation Steps:**
1. Download the "LTS" (Long Term Support) or stable version for your operating system
2. Run the installer
3. Follow the installation wizard with default settings
4. Complete the installation

**Verify Installation:**

In your terminal, type:

```bash
node --version
```

You should see output showing the Node.js version number (e.g., `v20.10.0`).

---

## Part 2: Installing Claude Code

Once all prerequisites are installed, you can install Claude Code globally using npm (Node Package Manager).

**Run the following command:**

```bash
npm install -g @anthropic-ai/claude-code
```

**Verify Installation:**

After installation completes, type:

```bash
claude
```

If Claude Code is installed correctly, it will attempt to run. However, **it will not work without a subscription** to Anthropic's Claude service.

**Getting a Subscription:**

To use Claude Code with the official Anthropic service, purchase a subscription at [https://claude.com/pricing](https://claude.com/pricing).

**Don't have a subscription?** Or have you run out of quota? Follow **Part 3** below to use free models.

---

## Part 3: Using Claude Code for Free (Claude Code Router)

**What if you want to use Claude Code without a paid subscription, or you've run out of your quota?**

The solution is **Claude Code Router (CCR)**, which allows you to use alternative AI providers, including free models.

### Step 1: Install Claude Code Router

Run this command in your terminal:

```bash
npm install -g @musistudio/claude-code-router
```

---

### Step 2: Get a Free AI Provider (OpenRouter)

We will use **OpenRouter**, which provides access to various AI models, including free ones.

**Create an OpenRouter Account:**

1. Go to [https://openrouter.ai/](https://openrouter.ai/) and sign up for a free account

**Get Your API Key:**

1. Navigate to [https://openrouter.ai/settings/keys](https://openrouter.ai/settings/keys)
2. Generate a new API key
3. **Copy and save this API key in a safe place** - you'll need it later

**Find a Free Model:**

1. Visit the [Models page](https://openrouter.ai/models)
2. In the search bar, type **"free"** to filter free models
3. In the left sidebar, look for **"Supported Parameters"** and select **Tools**
   - This is important because Claude Code needs tool-calling capabilities
4. Select a model you like (e.g., `z-ai/glm-4.5-air:free`) and **copy its name**

**Summary:** You now have:
- **Provider:** OpenRouter
- **Model name:** (e.g., `z-ai/glm-4.5-air:free`)
- **API key:** (saved from earlier)

---

### Step 3: Configure Claude Code Router (Easy Method)

We will use the web interface to configure the router.

**Launch CCR UI:**

In your terminal, run:

```bash
ccr ui
```

This will open a configuration page in your web browser.

**Add Provider:**

1. Click the **"Add Provider"** button
2. Click **"Select Template"** and choose **OpenRouter**
   - The name and API base URL fields will auto-fill
   - **Do NOT change these values**
3. In the **"API Key"** input field, paste your OpenRouter API key
4. In the **"Models"** input field, paste the model name you copied (e.g., `z-ai/glm-4.5-air:free`)
5. Click **"Add Model"**
   - Note: You can add multiple models from the same provider if desired
6. Leave other settings as they are and click **"Save"**

**Configure Router:**

1. Look at the **"Router"** box on the right side
2. This section tells the system which model to use for specific tasks (Default, Thinking, etc.)
3. To keep it simple, select your added model (e.g., `openrouter/z-ai/glm-4.5-air:free`) for **all** the available options
4. Click **"Save and Restart"**

**What you've accomplished:** You've added OpenRouter as a provider, specified which models to use, and configured CCR to route requests to your chosen model.

**Run It:**

Back in your terminal, run the following command to start coding:

```bash
ccr code
```

Send a message, and it should work!

---

## Troubleshooting: Manual Configuration

**If the `ccr ui` command does not work for any reason, you can configure the router manually.**

### Step 1: Locate the Configuration Directory

Find the Claude Code Router installation directory:

- **Windows:** `C:\Users\YOUR_USERNAME\.claude-code-router\`
- **Mac/Linux:** `~/.claude-code-router/`

Replace `YOUR_USERNAME` with your actual Windows username.

### Step 2: Edit config.json

1. Navigate to the directory above
2. Find and open the `config.json` file in a text editor (like Notepad or VS Code)
3. Delete everything in the file and paste the code below
4. **IMPORTANT:** Replace `"YOUR_OPENROUTER_API_KEY_HERE"` with your actual OpenRouter API key (e.g., `"sk-or-v1-..."`)

```json
{
  "LOG": false,
  "LOG_LEVEL": "debug",
  "CLAUDE_PATH": "",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "APIKEY": "",
  "API_TIMEOUT_MS": "1200000",
  "PROXY_URL": "",
  "transformers": [],
  "Providers": [
    {
      "name": "openrouter",
      "api_base_url": "https://openrouter.ai/api/v1/chat/completions",
      "api_key": "YOUR_OPENROUTER_API_KEY_HERE",
      "models": [
        "z-ai/glm-4.5-air:free"
      ],
      "transformer": {
        "use": [
          "openrouter"
        ]
      }
    }
  ],
  "StatusLine": {
    "enabled": false,
    "currentStyle": "default",
    "default": {
      "modules": []
    },
    "powerline": {
      "modules": []
    }
  },
  "Router": {
    "default": "openrouter,z-ai/glm-4.5-air:free",
    "background": "openrouter,z-ai/glm-4.5-air:free",
    "think": "openrouter,z-ai/glm-4.5-air:free",
    "longContext": "openrouter,z-ai/glm-4.5-air:free",
    "longContextThreshold": 120000,
    "webSearch": "openrouter,z-ai/glm-4.5-air:free",
    "image": ""
  },
  "CUSTOM_ROUTER_PATH": ""
}
```

### Step 3: Customize Your Configuration

In the configuration above:
- Replace `YOUR_OPENROUTER_API_KEY_HERE` with your actual OpenRouter API key (keep the quotes)
- You can change the model name `z-ai/glm-4.5-air:free` to any other free model you selected from OpenRouter

### Step 4: Save and Test

1. Save the `config.json` file
2. Close your text editor
3. Run the following command in your terminal:

```bash
ccr code
```

Claude Code should now launch with your configured provider and model!

---

## Common Issues and Solutions

**1. "command not found" errors**
- Ensure all prerequisites (Git, Python, Node.js) are properly installed
- Restart your terminal after installation
- On Windows, you may need to restart your computer

**2. Claude Code Router doesn't start**
- Verify that the `config.json` file is properly formatted (valid JSON)
- Check that your API key is correct and active
- Ensure the model name is spelled exactly as shown on OpenRouter

**3. API key issues**
- Make sure you copied the entire API key
- Check that there are no extra spaces before or after the key
- Verify your OpenRouter account is active

**4. Model not responding**
- Try a different free model from OpenRouter
- Check your internet connection
- Ensure the model supports tool calling (has "Tools" in supported parameters)

---

## Summary

Congratulations! You've successfully set up Claude Code. Here's what you accomplished:

✅ Installed prerequisites (Git, Python, Node.js)  
✅ Installed Claude Code CLI  
✅ Installed Claude Code Router for free model access  
✅ Configured OpenRouter as your AI provider  
✅ Selected and configured a free model  
✅ Launched Claude Code with your custom configuration

You can now use Claude Code with free AI models through OpenRouter!

**Need help?** Review each section carefully and ensure all steps are completed. Most issues arise from skipped steps or incorrect API key configuration.

Happy coding with Claude! 🚀
