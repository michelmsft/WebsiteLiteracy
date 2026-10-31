---
lab:
    title: 'Download Codex and prepare your workspace'
    description: 'Install the official Codex-capable desktop app and ask its coding agent to prepare the tools and account connections.'
    level: 200
    duration: 15
    islab: true
    primarytopics:
        - Codex
        - AI-assisted development
---

# Download Codex and prepare your workspace

Codex is an AI coding agent. Unlike a conversation that only gives you code to copy, it can create project files, run tools, and help publish your website. You install the desktop app and give it a dedicated place to work.

| Component | What you're trying to achieve |
| --- | --- |
| Official desktop app with Codex | Give the agent access to a local project |
| Project workspace | Keep this website separate from other files |
| Account connections and development tools | Let Codex prepare what it needs, with your approval |

This exercise should take approximately **15** minutes to complete.

> **Note**: OpenAI's current documentation labels the Codex-capable Windows app **ChatGPT desktop app**. Features, account access, and usage limits change. Check [Codex availability and pricing](https://developers.openai.com/codex/pricing/) first. Free desktop access is subject to rollout.

## Prerequisites

You need a Windows computer that supports the official desktop app, permission to install approved software, and your Azure and GitHub accounts. You also need a ChatGPT account with access to the app's coding-agent features.

Create missing accounts through the linked [Azure](01-create-azure-account.md) and [GitHub](02-create-github-account.md) exercises. Don't use a chat-only interface that cannot create files and run tools.

## Download and sign in

You install from the official source, not an advertisement or an unrelated download site.

1. Open the [official Windows app download instructions](https://developers.openai.com/codex/windows/windows-app/).
1. Select the official download link and complete installation.
1. Open the app and sign in with your ChatGPT account, or create one when prompted.
1. Choose local project work and use **Add new project**, or the equivalent folder picker, to open a new empty folder named `neighborhood-website`.
1. Keep **Ask for approval** enabled. Don't choose unrestricted full access.
1. Confirm that the selected workspace is your new website folder.

If your account doesn't have coding-agent access, pause and ask your instructor about an approved equivalent with local file and tool access. Don't purchase API credits just to continue.

## Ask Codex to prepare everything

You describe the outcome. Codex checks and installs the needed tools, rather than asking you to learn installation commands.

1. Start a conversation in the website workspace.
1. Send the following setup request.

    This request sets the course defaults once. You don't choose a framework or write configuration files.

    ```prompt
    I am a complete beginner. Prepare this workspace so you can create
    and publish my website for me.

    Use TypeScript and choose the framework, design, and project setup.
    Keep it a static website with no database, paid services, or secrets
    in the website files. Use an npm lockfile, typecheck and build scripts,
    and browser-ready build output in dist.

    Check for Git, Node.js LTS, GitHub CLI, and Azure CLI. Install missing
    tools from official sources after asking for my approval.
    Run all commands yourself. Start Azure authentication by running
    az login --use-device-code. Give me the official sign-in URL and
    temporary device code from that command, then wait while I sign in
    and complete any multifactor authentication in my browser.
    Guide me through GitHub's browser sign-in and installer approvals.
    After Azure login succeeds, list my subscriptions and ask me to
    confirm the active subscription before selecting it with az account set.
    Do not create cloud resources or publish anything yet.
    Keep credentials out of chat, source files, and command output.
    Tell me when the workspace and account connections are ready.
    ```

1. Review installation requests and approve only the tools listed in the request.
1. Open `https://aka.ms/devicelogin` when Codex starts Azure sign-in, enter the temporary code from its current login request, and complete sign-in and any multifactor authentication. Complete GitHub's browser sign-in when requested.
1. Reopen the app and workspace if Codex explains that installed tools require a restart.
1. Ask Codex to confirm that the tools are available, both account connections work, and it hasn't created Azure resources.

**What you should see:** Codex reports a ready workspace and connected accounts. You don't type commands or configure the tools yourself.

Only use a device code from the login request you just asked Codex to start. Don't approve unsolicited codes. Your password stays in Microsoft's sign-in page, not in chat. The temporary device code isn't an Azure deployment token.

If the code expires, ask Codex to restart the login. If your organization's policy blocks device-code authentication, ask Codex to use the approved interactive `az login` browser flow instead. Don't bypass the policy.

## Summary

You have successfully completed this exercise. Codex is ready to create and publish your website.

## Clean up

No cloud resources are needed yet. If you stop, ask Codex to sign out of the course's tool connections and list any local files it created. Delete only the dedicated workspace if you don't need it. Installed tools don't need to be removed to finish the course.

Continue with [Ask Codex to create and publish your website](04-create-publish-with-codex.md).
