## Setting Up Your Local Environment

Here's a practical, step-by-step guide to setting up a robust local environment. We'll use VS Code as the editor, but the principles are transferable.

1.  **Install Your Core IDE Plugin:**
    *   Go to the Extensions Marketplace in VS Code.
    *   Search for and install **GitHub Copilot**.
    *   Follow the authentication flow to link it to your GitHub account.

2.  **Install Your CLI Agent:**
    *   You'll need `npm` (the Node.js package manager) installed.
    *   Open your terminal and run: `npm install -g @google/generative-ai` (for the Gemini CLI) or the equivalent for the tool of your choice.
    *   Run the setup/authentication command (e.g., `gemini auth login`).

3.  **Configure API Keys Securely:**
    *   Your AI tools need API keys to function. **NEVER commit API keys to your repository.**
    *   The best practice is to store them as environment variables. Add a line like this to your shell profile file (`.zshrc`, `.bash_profile`, or PowerShell profile):
        ```shell
        export GOOGLE_API_KEY="your_api_key_here"
        export GITHUB_TOKEN="your_github_token_here"
        ```
    *   Your tools will automatically detect and use these environment variables.