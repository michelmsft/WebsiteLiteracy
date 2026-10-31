---
lab:
    title: 'Ask Codex to create and publish your website'
    description: 'Describe a website and let Codex build it in TypeScript, create its repository, and automate deployment to free Azure hosting.'
    level: 200
    duration: 35
    islab: true
    primarytopics:
        - Codex
        - TypeScript
        - Azure Static Web Apps
        - GitHub Actions
---

# Ask Codex to create and publish your website

You describe the website you want, then review what Codex creates. ChatGPT's Codex agent runs the Azure commands and deploys the first version directly from your computer. It also handles the TypeScript files, GitHub repository, and workflow for future updates.

**Continuous integration and continuous deployment (CI/CD)** means automatically checking and publishing saved changes. You don't edit the workflow's YAML instructions yourself.

| Component | What you're trying to achieve |
| --- | --- |
| TypeScript website | Turn your description into a working page |
| Public GitHub repository | Save the project and its history |
| Dedicated Azure resource group | Keep the website resource together for safe cleanup |
| Azure Static Web Apps Free | Publish the site at a free Azure-provided HTTPS address |
| GitHub Actions workflow | Check and deploy every ordinary push to `main` |

This exercise should take approximately **35** minutes to complete.

## Prerequisites

You need Codex working in a dedicated local project, connected to your GitHub account and an approved active Azure subscription. If necessary, use [Download Codex and prepare your workspace](03-install-codex.md) first.

You don't need a repository, hosting resource, website files, or a design specification. Codex creates them.

## Describe the website you want

You start with a simple fictional website so there's no personal or business information to expose.

1. Open the website workspace in Codex and continue the setup conversation.
1. Send this request, or replace the fictional club with your own fictional idea.

    The request describes the visitor experience, not programming decisions.

    ```prompt
    Create a modern website for a fictional Neighborhood Garden Club.
    Include a welcome section, example activities, and a clear way to
    learn more. Make it look good on phones and work with a keyboard.
    Use fictional information only. Do not collect visitor information.
    Choose the layout, colors, and technical details for me.
    Build and test it, then open a local preview for me to review.
    Do not publish until I approve the preview.
    ```

1. Let Codex create the TypeScript project and run its checks.
1. Open the preview link Codex provides and check the page on a wide and narrow browser window.
1. Try the navigation and interactive elements.
1. Request a simple change, such as `Make the welcome section shorter and use blue accents`, then review the updated preview.

**What you should see:** A working website, not just a block of code in chat. Codex reports successful type checking and a successful build.

## Ask Codex to publish it

You approve the design and tell Codex where to publish. You don't create the repository or hosting resource yourself.

1. Send the following request after the preview meets your expectations.

    This request gives Codex the free-hosting and automation boundaries.

    ```prompt
    I approve this website. Publish it for me.

    Create a public repository named neighborhood-website in my GitHub
    account and use main as the publishing branch.
    Run all provisioning and deployment commands yourself.
    If Azure login is needed, run az login --use-device-code, give me
    the official URL and temporary code, and wait for my browser sign-in.
    Confirm the subscription and select it with az account set.
    Use az group create and az staticwebapp create to create a dedicated
    resource group and Static Web App with --sku Free.
    Create it without automatic source integration so there is no
    competing generated workflow. Use the Azure-provided HTTPS address.
    Ask me to confirm the subscription and exact resources before creation.
    Do not upgrade my subscription or create any paid service.

    Type-check and build the website. Install the official
    @azure/static-web-apps-cli if needed, after asking for approval.
    Retrieve this site's deployment token with az staticwebapp secrets list,
    capturing it privately without printing it.
    Use it through the temporary SWA_CLI_DEPLOYMENT_TOKEN environment
    variable to run swa deploy .\dist --env production for this exact site.
    Remove the temporary variable after use, including if deployment fails.
    Verify the live website before configuring future automated updates.

    Create a GitHub Actions YAML workflow that installs from the lockfile,
    type-checks, builds, and deploys the website automatically for every
    push to main, with no file-path filters.
    Use the supplied course workflow as a reference if it is available.
    Store the Azure deployment token directly as a GitHub Actions secret.
    Never display the token or put it in chat or a committed file.
    Create only one deployment workflow for this site.

    After the direct deployment succeeds, commit and push the workflow,
    wait for its first successful run, and verify the live site again.
    Resolve failures yourself. Do not ask me to run commands, provision
    resources in the portal, or copy deployment tokens.
    Give me the repository link, workflow-run link, live website link,
    resource group name, and confirmation that the hosting plan is Free.
    ```

1. Review the proposed subscription, public repository, and Free hosting resource before approving creation.
1. If Codex starts a new device-code login, enter its temporary code at the official Microsoft sign-in page and complete any multifactor authentication. Don't enter passwords or access tokens into chat.
1. Let Codex provision the Free resource, deploy directly, then create the repository workflow and store its secret. Ask it to fix errors instead of presenting you with commands to run.
1. Open the workflow-run link and confirm a successful result.
1. Open the live website link and confirm that it matches the approved preview.
1. Ask Codex to confirm the Free hosting plan and record the resource names and links in the local project notes, without credentials.

**What you should see:** Your website online at an HTTPS address, with a successful GitHub Actions run and a public repository containing the TypeScript project.

The first upload is a **direct deployment by Codex**, using your approved Azure CLI session and the site's deployment token. Subsequent pushes to `main` use **GitHub Actions**, with the token stored as a repository secret. Device-code login belongs to your interactive setup, not the unattended workflow. Codex never commits that login session or its tokens.

The [reference YAML](../../Labfiles/04-create-publish/azure-static-web-apps.yml) uses the project defaults from the setup prompt: an npm project at the repository root, a lockfile, `typecheck` and `build` scripts, and output in `dist`. Codex creates those files and the active `.github/workflows/azure-static-web-apps.yml` file. You don't need to open or edit them.

> **Important**: If Codex proposes paid hosting or asks you to upgrade the subscription, stop. A disabled subscription requires a separate billing decision. It isn't permission to switch to a paid hosting plan.

## Summary

You have successfully completed this exercise. Codex created your TypeScript website and its GitHub-to-Azure publishing connection while you focused on the result.

## Clean up

Keep the website if you plan to practice updates. Otherwise, ask Codex to list the course resources, disable deployment, and propose their removal. Approve deletion only after confirming that the targets belong exclusively to this course.

Continue with [Ask Codex to update and remove your website](05-update-with-codex.md).
