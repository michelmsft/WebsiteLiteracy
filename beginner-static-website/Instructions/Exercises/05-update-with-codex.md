---
lab:
    title: 'Ask Codex to update and remove your website'
    description: 'Request a website change, verify automatic main-branch deployment, and ask Codex to remove the course resources safely.'
    level: 200
    duration: 15
    islab: true
    primarytopics:
        - Codex
        - GitHub Actions
        - Azure resource cleanup
---

# Ask Codex to update and remove your website

You maintain the website the same way you created it: describe what you want and let Codex handle the files and publishing tools. You verify that saving a change to `main` starts deployment automatically.

| Component | What you're trying to achieve |
| --- | --- |
| Website project | Apply a small content change through Codex |
| GitHub Actions workflow | Prove that a saved change starts publishing automatically |
| Azure hosting resource | Check the live result, then remove it if you're finished |

This exercise should take approximately **15** minutes to complete.

## Prerequisites

You need the published website, its GitHub repository, and the Codex workspace that created them. If you don't have these, ask Codex to build and publish the site using [the creation exercise](04-create-publish-with-codex.md).

## Ask for an update

You make one visible change so it's easy to recognize the new version.

1. Open your live website and note its current heading.
1. Return to the same Codex project conversation.
1. Send this request.

    The request asks for an ordinary saved change, not a manual deployment.

    ```prompt
    Change the welcome heading to "Neighborhood Garden Club - Autumn update".
    Run the project checks, commit the change, and push it to main.
    Do not manually start deployment. Let the existing GitHub Actions
    workflow start automatically from the push.
    Wait for success and give me the commit link, automatic workflow-run
    link, and live website link. Don't make another change while it runs.
    ```

1. Open the workflow-run link and confirm that it succeeds for the heading-change commit.
1. Refresh the live website and confirm that the new heading appears.
1. Check the navigation and phone-sized layout again.

**What you should see:** The requested heading online, published by a workflow that starts from Codex's push to `main`. No manual publishing step is needed.

If it fails, tell Codex: `Diagnose the failed run, fix the cause, and verify the next automatic deployment. Don't switch to paid services.`

## Ask for recovery if needed

You practice describing a recovery request without editing project history yourself.

1. Ask Codex to restore the previous welcome heading using a new commit.
1. Ask it to run checks, push to `main`, and wait for the automatic deployment.
1. Refresh the website and confirm the original heading returns.

Restoring with a new commit keeps the recorded history. Codex shouldn't erase commits or remove the deployment workflow.

## Summary

You have successfully completed this exercise. You requested an update and recovery in plain language and verified automatic publishing.

## Clean up

If you want to complete [the optional Cloudflare domain exercise](06-bonus-cloudflare-domain.md), keep the website and its connections for now. Complete that exercise before removing the Azure resources.

If you're finished, ask Codex to prepare removal. You approve the exact targets before it deletes anything.

1. Send the following request.

    This request makes cleanup a reviewed action, not an unrestricted deletion instruction.

    ```prompt
    I am finished with this course. Identify the exact GitHub repository,
    workflow, deployment secret, Azure Static Web App, and resource group
    created for this website. Show me a cleanup proposal before deleting.
    Do not cancel my subscription, delete accounts, remove shared resources,
    or delete my local project. Wait for my approval.
    ```

1. Review the names and confirm that the proposed Azure resources belong only to this course.
1. Approve the proposal and ask Codex to disable the workflow, wait for active runs, delete only the dedicated course Azure resources, and remove the deployment secret.
1. Ask Codex to verify deletion. Keep the repository unless you separately approve deleting it.
1. Open the old live website link after deletion settles and confirm that it's no longer available.

If you keep the website, retain your Azure billing reminder. Free hosting requires an active subscription, and a pay-as-you-go upgrade is a separate decision.
