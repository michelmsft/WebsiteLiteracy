---
lab:
    title: 'Buy a Cloudflare domain and connect your website'
    description: 'Purchase an optional domain and ask Codex to connect it to Azure Static Web Apps with Cloudflare DNS and a www redirect.'
    level: 200
    duration: 40
    islab: true
    primarytopics:
        - Cloudflare Registrar
        - DNS
        - Azure Static Web Apps
        - Custom domains
---

# Buy a Cloudflare domain and connect your website

Your website already has an Azure address. In this optional exercise, you buy a memorable domain name through Cloudflare and ask ChatGPT's Codex agent to connect it to your website. Visitors use your root domain, and the `www` version redirects to the same site.

The **Domain Name System (DNS)** connects names to services. A **root domain**, also called an apex domain, is a name such as `example.com`. The name `www.example.com` is a subdomain. A redirect changes the visitor's browser address from one name to another.

| Component | What you're trying to achieve |
| --- | --- |
| Cloudflare account and Registrar | Purchase and manage your own domain |
| Cloudflare DNS records | Send root-domain visitors to Azure |
| Static Web Apps custom domain | Tell Azure to accept your domain and provide its HTTPS certificate |
| Cloudflare Redirect Rule | Send `www` visitors to the root domain |
| Cloudflare Universal SSL | Provide HTTPS for the `www` redirect |

This exercise should take approximately **40** minutes to complete.

> **Important**: This bonus isn't entirely free. Domain registration and renewal cost money, with prices depending on the name and extension. Cloudflare enables auto-renew by default. Review the checkout total, registration term, renewal price, and renewal settings before buying. Azure hosting remains on **Free**.

## Prerequisites

You need the following:

- A working Azure Static Web Apps website and an active subscription.
- The Codex workspace and account connections used to create the site.
- A Cloudflare account with a verified email address, or permission to create one.
- A payment method and accurate registration contact details.
- Permission and budget to register a new domain you don't already use for another service.

If you don't have a site, ask Codex to create and publish one using [the website creation exercise](04-create-publish-with-codex.md). Don't delete the hosting resource before starting this bonus.

Codex needs an approved way to manage Cloudflare: a supported browser-control tool or a securely configured, narrowly scoped API connection. A chat-only interface can't do this work. Ask your instructor to help enable an approved connection if needed. Don't grant unrestricted access to all your Cloudflare domains.

Throughout this exercise, `example.com` means the domain you actually purchase. Don't try to purchase that reserved example name. Codex substitutes your real name in all records and rules.

## Purchase your domain

You choose and buy the name yourself. Codex can explain options, but you enter personal details and authorize payment only in Cloudflare.

1. Open [Cloudflare](https://www.cloudflare.com), create or sign in to your account, and verify your email address.
1. In the dashboard, open **Domain Registration** > **Register domains**, or use [the official registration page](https://dash.cloudflare.com/?to=/:account/registrar/register).
1. Search for an available name you want to own. Choose one you have permission to use, not another organization's brand.
1. Select **Purchase**, choose the registration term, and review the total cost and renewal details.
1. Enter accurate registration contact and payment details privately, review the agreements, and select **Complete purchase** only when you approve the charge.
1. Complete any registrant-email verification Cloudflare requests. Confirm that the domain appears in your account and its DNS zone is active.
1. Tell Codex the purchased domain name, but don't send payment details, passwords, or API tokens.

**What you should see:** Your registered domain in Cloudflare. Cloudflare Registrar domains use Cloudflare's nameservers. You don't move them to Azure DNS or purchase Azure DNS hosting.

## Ask Codex to connect the root domain

You let Codex do the DNS and Azure work after reviewing its proposal. DNS records translate the name into the hosting destination.

1. Return to the same Codex workspace and send this request, replacing `example.com`.

    This request connects only the root domain to Azure and protects existing DNS records.

    ```prompt
    I purchased example.com through Cloudflare. Connect its root domain
    to the Azure Static Web App you created for this project.
    Keep Azure hosting on Free and Cloudflare on its Free website plan.

    Use our approved Cloudflare browser or API connection. Let me complete
    private sign-in screens. Never ask me to paste tokens into chat.
    If the connection is unavailable, stop and explain what access is needed.
    If Azure login is needed, run az login --use-device-code yourself
    and let me complete the official Microsoft browser sign-in.

    Identify the exact Azure resource, subscription, Cloudflare zone,
    and existing DNS records. Show the changes and ask for approval.
    Preserve unrelated DNS, email records, and redirect rules.

    Use az staticwebapp hostname set with dns-txt-token validation and
    --no-wait for the root domain. Retrieve the validationToken using
    az staticwebapp hostname show, then add Azure's required TXT record
    at the root in Cloudflare. Use the returned value, not a made-up token.
    Add a DNS-only CNAME at @ pointing to this site's default
    azurestaticapps.net hostname, without https:// or a path.
    Use Cloudflare's root CNAME flattening. Do not proxy the root record.

    Wait for Azure ownership validation and its managed HTTPS certificate.
    Check the custom-domain status and open https://example.com.
    Report pending validation honestly; don't claim success while it waits.
    ```

1. Complete Cloudflare sign-in privately when requested. If an API connection is used, store its credential through your tool's secure credential mechanism, not in chat or the repository.
1. Review the exact domain, Azure resource, and DNS changes, then approve.
1. Let Codex create the records and wait for validation. Ask it to report the status if the operation takes time.
1. Open your root domain with `https://` and confirm that your website appears without a certificate warning.

**What you should see:** Your site at `https://example.com`. Azure's **Custom domains** list shows the root domain as ready.

The records Codex creates have this shape. Azure supplies the actual validation value and hostname.

| Type | Name | Content | Proxy status |
| --- | --- | --- | --- |
| TXT | `@` | Azure's root-domain validation value | Not applicable |
| CNAME | `@` | Your site's default `azurestaticapps.net` hostname | **DNS only**, gray cloud |

Cloudflare flattens the root CNAME so it works at the apex. Keeping it **DNS only** sends root-domain visitors directly to Azure. Don't replace an existing root record without reviewing what it serves.

## Ask Codex to redirect www

You choose the root domain as the canonical address: the single address visitors should see. Cloudflare handles `www` as a redirect-only hostname, so it doesn't need a second Azure custom-domain binding.

1. Send this request, replacing `example.com` with the same purchased domain.

    This request covers both HTTP and HTTPS and preserves the rest of the address.

    ```prompt
    Configure www.example.com to redirect to https://example.com.
    Show me the proposed DNS record and rule before applying changes.

    Use a Cloudflare proxied A record for www with the documented
    redirect-only placeholder address 192.0.2.0 and TTL Auto.
    This is not an Azure origin IP. Do not use it for the root record.

    Create one Single Redirect rule matching only
    http.host eq "www.example.com", for both HTTP and HTTPS.
    Use the dynamic target
    concat("https://example.com", http.request.uri.path),
    status 301, and preserve_query_string true.
    Do not match or redirect the root hostname back to www.
    Preserve unrelated rules and check rule ordering for conflicts.

    Confirm that Cloudflare Universal SSL is active for www before
    declaring HTTPS ready. Keep the root CNAME DNS-only.
    Test HTTP and HTTPS www requests, including a path and query string.
    Report the response status and Location header without disabling TLS checks.
    ```

1. Approve the proposal only if it targets your exact `www` hostname and doesn't alter unrelated records.
1. Let Codex deploy the rule and check Cloudflare's certificate status.
1. Open `https://www.example.com` and confirm that the browser changes to `https://example.com`.

**What you should see:** The root-domain website, with no `www` in the final address and no redirect loop.

| Setting | Value |
| --- | --- |
| DNS record | `A`, name `www`, content `192.0.2.0` |
| **Proxy status** | **Proxied**, orange cloud |
| Rule match | Exact `www` hostname, regardless of HTTP or HTTPS |
| Redirect destination | HTTPS root domain plus the original path |
| Status | `301`, permanent redirect |
| **Preserve query string** | Enabled |

Single Redirects only run for proxied traffic. The placeholder is appropriate because Cloudflare returns the redirect before contacting an origin. If the rule doesn't match, the placeholder doesn't host a website.

Cloudflare provides the certificate for proxied `www`. Azure provides the certificate for the DNS-only root domain. DNS propagation and certificate issuance can take hours, sometimes longer than the exercise itself. Don't bypass certificate warnings.

## Verify the complete result

You check both names and prove that custom domains don't replace the deployment workflow.

1. Ask Codex to verify the following expected outcomes using your real domain.

    | Request | Expected result |
    | --- | --- |
    | `https://example.com/` | Your website with a valid Azure-managed certificate |
    | `http://www.example.com/` | `301` to `https://example.com/` |
    | `https://www.example.com/` | `301` to `https://example.com/`, with valid Cloudflare HTTPS |
    | `https://www.example.com/activities?source=bonus` | `301` with `Location: https://example.com/activities?source=bonus` |

1. Ask Codex to test the root domain separately and confirm that it doesn't redirect back to `www`. The sample `/activities` request tests redirect preservation; it doesn't require your site to have that route.
1. Request a small website text update and ask Codex to push it to `main`, wait for automatic deployment, and verify the update at your custom domain.
1. Confirm that the hosting plan is still **Free** and that the GitHub Actions workflow still deploys to the same Azure resource.

**Result:** The purchased domain serves your site, `www` redirects correctly, and future updates still publish automatically.

## Summary

You have successfully completed this exercise. You purchased a domain, connected its root to Azure, and configured a secure `www` redirect through Cloudflare while keeping Azure hosting on Free.

## Clean up

If you stop using this domain for the website, ask Codex to list the course's custom-domain binding, DNS record IDs, and redirect rule ID before proposing removal.

1. Approve removal only for the course-created redirect rule, `www` placeholder, root website CNAME, validation TXT record, and Azure custom-domain binding. Ask Codex to remove or restore DNS changes before deleting the hosting resource, so no record points at abandoned Azure hosting.
1. Ask Codex to restore any records replaced during setup and revoke any temporary Cloudflare API credential used for the bonus.
1. Follow [the website cleanup exercise](05-update-with-codex.md) if you also want to remove the Azure resource.
1. Review **Auto-renew** in Cloudflare Registrar yourself. Keep it enabled if you intend to retain the domain, or disable it if you knowingly choose not to renew.

Removing DNS or Azure resources doesn't cancel domain registration, refund the purchase, or disable renewal. Keep registration contact information private and accurate. Don't let a domain expire if you still use it for email or another service.

## Consult the official guidance

- [Register a domain with Cloudflare](https://developers.cloudflare.com/registrar/get-started/register-domain/).
- [Azure root-domain setup](https://learn.microsoft.com/azure/static-web-apps/apex-domain-external).
- [Azure CLI custom-domain commands](https://learn.microsoft.com/cli/azure/staticwebapp/hostname).
- [Cloudflare CNAME flattening](https://developers.cloudflare.com/dns/cname-flattening/).
- [Cloudflare DNS records and redirect-only placeholders](https://developers.cloudflare.com/dns/manage-dns-records/how-to/create-dns-records/).
- [Create a Single Redirect rule](https://developers.cloudflare.com/rules/url-forwarding/single-redirects/create-dashboard/).
- [Cloudflare Universal SSL](https://developers.cloudflare.com/ssl/edge-certificates/universal-ssl/enable-universal-ssl/).
