# Claude Code Installation and Setup Guide

Welcome! This guide is designed to help you set up **Claude Code** on your computer. We have written this specifically for beginners, so follow the steps carefully.

This guide covers:
1.  Installing necessary prerequisites.
2.  Installing the official Claude Code tool.
3.  Setting up **Claude Code Router** to use free AI models (for users without a paid subscription).

---

## Part 1: Prerequisites

Before we install Claude Code, we need to ensure your system has the necessary tools installed. Please download and install the versions appropriate for your Operating System (Windows, macOS, or Linux). **Always choose the stable/LTS (Long Term Support) versions.**

### 1. Git
Git is a version control system used widely in programming.

1.  **Download:** Go to [https://git-scm.com/downloads](https://git-scm.com/downloads) and download the installer for your OS.
2.  **Install:** Run the installer. During installation, you will be asked many configuration questions. **Do not change anything**; just keep clicking "Next" to accept the defaults.
3.  **Verify:** Open your terminal (Command Prompt or PowerShell on Windows, Terminal on Mac/Linux) and type the following command:
    ```bash
    git --version
    ```
    If you see a version number, Git is installed successfully.

### 2. Python
Python is a programming language required for many tools.

1.  **Download:** Go to [https://www.python.org/downloads/](https://www.python.org/downloads/) and download the latest stable version.
2.  **Install:** Run the installer.
3.  **Verify:** In your terminal, type:
    ```bash
    # On Windows
    py --version
    
    # On macOS/Linux (if 'py' doesn't work)
    python3 --version
    ```

### 3. Node.js
Node.js is a JavaScript runtime needed to run Claude Code.

1.  **Download:** Go to [https://nodejs.org/en/download/current](https://nodejs.org/en/download/current).
2.  **Install:** Download and install the "LTS" (Long Term Support) or Stable version.
3.  **Verify:** In your terminal, type:
    ```bash
    node --version
    ```

---

## Part 2: Installing Claude Code

Now that we have the prerequisites, let's install the official Claude Code CLI.

1.  Open your terminal.
2.  Run the following command:
    ```bash
    npm install -g @anthropic-ai/claude-code
    ```
3.  **Verify:** Type `claude` in your terminal.
    *   If it runs, the installation was successful.
    *   **Note:** To use the official `claude` command directly, you need a paid subscription. You can purchase one at [https://claude.com/pricing](https://claude.com/pricing).

**Don't have a subscription?** Or have you run out of quota? Follow **Part 3** below to use free models.

---

## Part 3: Using Claude Code for Free (Claude Code Router)

If you want to use Claude Code without a paid subscription, we can use a tool called **Claude Code Router (CCR)**. This allows us to connect Claude Code to other AI providers, including free ones.

### Step 1: Install Claude Code Router
Run this command in your terminal:
```bash
npm install -g @musistudio/claude-code-router
```

### Step 2: Get a Free AI Provider (OpenRouter)
We will use **OpenRouter**, which provides access to various AI models, including free ones.

1.  **Create Account:** Go to [https://openrouter.ai/](https://openrouter.ai/) and sign up.
2.  **Get API Key:** Go to [https://openrouter.ai/settings/keys](https://openrouter.ai/settings/keys) to create your API Key. **Copy this key and store it safely; you will need it soon.**
3.  **Find a Free Model:**
    *   Visit the [Models page](https://openrouter.ai/models).
    *   In the search bar, type **"free"**.
    *   In the left sidebar, look for "Supported Parameters" and select **Tools** (this is important because Claude Code needs tool-calling capabilities).
    *   Select a model you like (e.g., `z-ai/glm-4.5-air:free`) and **copy its name**.

### Step 3: Configure Claude Code Router (Easy Method)
We will use the web interface to configure the router.

1.  In your terminal, run:
    ```bash
    ccr ui
    ```
    This will open a configuration page in your web browser.

2.  **Add Provider:**
    *   Click the **"Add Provider"** button.
    *   Click **"Select Template"** and choose **OpenRouter**.
    *   **API Key:** Paste the key you got from OpenRouter.
    *   **Models:** Paste the model name you copied (e.g., `z-ai/glm-4.5-air:free`).
    *   Click **"Add Model"**.
    *   Leave other settings as they are and click **"Save"**.

3.  **Configure Router:**
    *   Look at the **"Router"** box on the right side.
    *   This section tells the system which model to use for specific tasks (Default, Thinking, etc.).
    *   To keep it simple, select your added model (e.g., `openrouter/z-ai/glm-4.5-air:free`) for **all** the available options.
    *   Click **"Save and Restart"**.

4.  **Run It:**
    Back in your terminal, run the following command to start coding:
    ```bash
    ccr code
    ```
    Send a message, and it should work!

---

## Troubleshooting: Manual Configuration
If the `ccr ui` command does not work for any reason, you can configure the router manually.

1.  **Find the Config Directory:**
    *   **Windows:** `C:\Users\YOUR_USERNAME\.claude-code-router\`
    *   **Mac/Linux:** `~/.claude-code-router/`

2.  **Edit Config File:**
    *   Find the `config.json` file in that folder.
    *   Open it with a text editor (like Notepad or VS Code).
    *   Delete everything in the file and paste the code below.
    *   **IMPORTANT:** You must replace `"api_key": ""` with your actual OpenRouter API key (e.g., `"api_key": "sk-or-v1-..."`).

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

3.  **Save and Run:**
    Save the file, then run `ccr code` in your terminal.
