# Create and publish your first website with Codex

Create your Azure and GitHub accounts, download Codex, and describe the website you want. ChatGPT's Codex agent creates the TypeScript website, signs in to Azure through device-code authentication, provisions Free hosting, and deploys the first version directly. It also sets up GitHub Actions for automatic publishing of later changes.

**Audience:** Complete beginners and business users.  
**Level:** 200.  
**Time:** Approximately 90 minutes, plus installation and deployment waiting time.  
**Optional bonus:** 40 minutes, plus DNS and certificate waiting time, with a paid domain purchase.  
**Environment:** A Windows computer, a browser, and the official Codex-capable desktop app.

You don't write code, select a framework, edit YAML, or type terminal commands. You describe the result, complete sign-in screens, approve specific actions, and review the website. Codex handles the technical work.

> **Note**: OpenAI's current Windows documentation calls the Codex-capable application the **ChatGPT desktop app**. This course calls its coding agent **Codex**. Use the official download instructions linked in exercise three, not an unrelated app with a similar name.

## Follow the course

Each exercise begins with what you're trying to achieve and which components are involved.

| Exercise | What you achieve | Time |
| --- | --- | --- |
| [Create your Azure account](Instructions/Exercises/01-create-azure-account.md) | An account and active subscription for website hosting | 15 minutes |
| [Create your GitHub account](Instructions/Exercises/02-create-github-account.md) | An account where Codex can save your website | 10 minutes |
| [Download Codex and prepare your workspace](Instructions/Exercises/03-install-codex.md) | An installed coding agent that prepares the tools for you | 15 minutes |
| [Ask Codex to create and publish your website](Instructions/Exercises/04-create-publish-with-codex.md) | A TypeScript website, GitHub repository, and live Azure website | 35 minutes |
| [Ask Codex to update and remove your website](Instructions/Exercises/05-update-with-codex.md) | A verified automatic update and safe cleanup | 15 minutes |
| [Bonus: Buy a Cloudflare domain and connect your website](Instructions/Exercises/06-bonus-cloudflare-domain.md) | A custom root domain with `www` redirected to it | 40 minutes |

Use an existing account if you already have one. After account registration, all setup, coding, repository creation, deployment, troubleshooting, and cleanup requests go through Codex. You still complete private browser sign-ins and installer approvals yourself. For the optional bonus, you also complete the paid domain checkout yourself. Keep the website resource instead of cleaning it up in exercise five if you plan to do the bonus.

## Understand the components

| Component | Plain-language explanation |
| --- | --- |
| Azure account | Your sign-in identity for Azure |
| Azure subscription | Where Azure records your resource access, usage, and billing |
| GitHub account and repository | Your account and the project folder where Codex saves the website |
| Codex | An AI coding agent that creates files and runs tools on your behalf |
| TypeScript website | The website code Codex creates and turns into browser-ready files |
| Azure Static Web Apps Free plan | The service that hosts your website at an HTTPS address |
| GitHub Actions CI/CD | Automation that checks and publishes saved changes to `main` |

**Your role:** Describe, approve, and check.  
**Codex's role:** Choose the design and tools, create the files, run checks, and publish.

Codex runs `az login --use-device-code` itself. You enter the temporary code at the official Microsoft sign-in page and complete any multifactor authentication. Codex then uses Azure CLI to create the hosting resource and Static Web Apps CLI to upload the built website directly to production. You don't run commands, create resources in the portal, or copy deployment tokens. GitHub Actions handles later pushes to `main` without another device-code sign-in.

## Keep the free-service boundaries clear

> **Important**: Azure's new-customer free account offer and the Static Web Apps Free hosting plan are different. Introductory credit expires or runs out. Azure disables the subscription and services unless you explicitly upgrade to pay-as-you-go. Free hosting still needs an active subscription. After an upgrade, unrelated paid services can incur charges.

- Use only **Azure Static Web Apps Free**, with the Azure-provided address.
- Use a **public GitHub repository** with fictional content and standard hosted Actions runners, which are free for public repositories.
- Don't create a database or enable a paid Azure service. The main course doesn't require a domain purchase. The optional bonus purchases a domain through Cloudflare, with annual renewal costs, while Azure hosting stays on Free.
- Review [Codex availability and pricing](https://developers.openai.com/codex/pricing/) before starting. Free desktop access is subject to rollout and usage limits. This course doesn't guarantee unlimited free AI use.
- Never put passwords, payment information, or deployment tokens into chat or source files.
- Leave approval safeguards enabled. Don't grant unrestricted access to your whole computer.

The hosting Free plan is suitable for this learning project, not a promise of production business hosting with a service-level agreement.

## Find the workflow reference

The [supplied GitHub Actions YAML](Labfiles/04-create-publish/azure-static-web-apps.yml) is a reference for Codex or an instructor. Learners don't copy it into GitHub themselves.

The reference assumes Codex creates an npm-based TypeScript project at the repository root, with a lockfile, `typecheck` and `build` scripts, and build output in `dist`. Codex selects the framework and creates this setup. Every ordinary push to `main` runs the checks and deploys the built website. There are no file-path filters.

The reference file isn't installed as an active workflow in this course repository. Codex creates the active workflow in the learner's repository.

## Consult the official guidance

- [Azure free account offer](https://azure.microsoft.com/free/).
- [Avoid charges with an Azure free account](https://learn.microsoft.com/azure/cost-management-billing/manage/avoid-charges-free-account).
- [GitHub account signup](https://github.com/signup).
- [Official Codex-capable Windows app download and setup](https://developers.openai.com/codex/windows/windows-app/).
- [Azure Static Web Apps Free hosting plan](https://learn.microsoft.com/azure/static-web-apps/plans).
- [Azure CLI device-code sign-in](https://learn.microsoft.com/cli/azure/authenticate-azure-cli-interactively).
- [Direct deployment with Static Web Apps CLI](https://azure.github.io/static-web-apps-cli/docs/cli/swa-deploy/).
- [GitHub Actions deployment to Azure Static Web Apps](https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/azure-static-web-app).

Codex can make mistakes. A task is complete only when the checks pass and you can open the expected website.
