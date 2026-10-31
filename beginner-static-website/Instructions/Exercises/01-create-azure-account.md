---
lab:
    title: 'Create your Azure account'
    description: 'Create an eligible Azure free account and identify the subscription that Codex uses for website hosting.'
    level: 200
    duration: 15
    islab: true
    primarytopics:
        - Azure accounts
        - Azure subscriptions
---

# Create your Azure account

Your website needs an online home. You first create an Azure account so Codex can later set up free website hosting with your permission.

An **account** identifies you when you sign in. A **subscription** records the cloud resources, permissions, and billing associated with your account. You need an active subscription, not just an account.

| Component | What you're trying to achieve |
| --- | --- |
| Azure account | Sign in to Azure |
| Azure subscription | Give Codex an approved place to create your website hosting |

This exercise should take approximately **15** minutes to complete.

## Prerequisites

You need a browser, an email address, and any phone number or accepted payment card requested for Azure verification. The free-account offer is subject to eligibility and regional availability.

If you already have an approved active subscription, skip registration. Don't use an employer subscription without permission.

## Register for the free account

You use the official signup page and review the offer before entering personal details.

1. Open the [Azure free account page](https://azure.microsoft.com/free/).
1. Review the offer terms, then select the free-account signup option.
1. Sign in with a Microsoft account, or create one when prompted.
1. Complete the requested profile, phone, and payment-card verification.
1. Review the agreement and finish signup without selecting a paid support plan.
1. Open the [Azure portal](https://portal.azure.com) and sign in.

> **Important**: Eligible new customers receive introductory credit for up to 30 days. Azure doesn't automatically upgrade you to pay-as-you-go. When credit expires or runs out, services stop unless you explicitly upgrade. An upgrade permits charges for paid services. A temporary card-verification hold can appear during signup.

If the offer isn't available to you, ask your instructor about an approved subscription rather than selecting a paid option.

## Confirm your subscription

You check that Codex has an active subscription to use later.

1. Search for `Subscriptions` in the Azure portal.
1. Open **Subscriptions** and select your subscription.
1. Confirm that its status is active, usually shown as **Enabled**.
1. Note its name privately so you recognize it during sign-in.
1. Set a reminder before your introductory credit expires to review whether to keep or remove the website.

**What you should see:** An active subscription. You haven't created any hosting resource yet.

The **Static Web Apps Free** plan has no hosting charge within its limits, but it still needs an active subscription. Free-account credit and a service's Free plan aren't the same thing.

## Summary

You have successfully completed this exercise. You have Azure access and understand which subscription Codex uses.

## Clean up

No cloud resource is created in this exercise. Keep the account if you plan to continue. If you stop, review [Azure subscription cancellation](https://learn.microsoft.com/azure/cost-management-billing/manage/cancel-azure-subscription) before canceling a subscription. Don't cancel one that contains other people's resources.

Continue with [Create your GitHub account](02-create-github-account.md).
