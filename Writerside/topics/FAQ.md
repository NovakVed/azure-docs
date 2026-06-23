# FAQ

Decision-style questions about whether and how to use %product%. For "it's broken, how do I fix it?" questions, see [Troubleshooting](Troubleshooting.md).

## Does the plugin support Azure DevOps Server (on-prem)?

Yes. Add the server's URL when creating an account. Both Azure DevOps Server 2019+ and Azure DevOps Services (cloud) are supported.

The cloud product uses `dev.azure.com/<org>`. On-prem uses your own server URL (e.g. `https://devops.example.com`). PAT auth works for both. OAuth via Microsoft Entra is **cloud-only**.

## Does it work with classic TFVC (non-Git) repositories?

No. The plugin is for Git-backed Azure Repos only. **TFVC** (Team Foundation Version Control, Microsoft's centralized VCS predecessor to Git in Azure DevOps) is not supported.

## Can I use this without an Azure DevOps account?

No — the plugin is exclusively for Azure DevOps. For GitHub or GitLab, use the bundled GitHub plugin or the JetBrains GitLab plugin respectively.

## Can I have both the GitHub and Azure DevOps PR plugins in the same IDE?

Yes. They register independent tool windows and don't share state. If a single project has remotes pointing at both GitHub and Azure DevOps, both tool windows appear; each one only lists PRs for its own remote.

## OAuth or PAT — which should I pick?

| You should use… | When                                                                                                         |
|-----------------|--------------------------------------------------------------------------------------------------------------|
| **OAuth**       | You're on the cloud product (`dev.azure.com`), your org doesn't ban OAuth, and you want MFA prompts inline.  |
| **PAT**         | You're on Azure DevOps Server (on-prem), your org's policy mandates PATs, or you've hit OAuth handler issues.|

OAuth tokens refresh automatically; PATs expire on the date you set when creating them. PATs bypass MFA by design — generating one requires the user to already be authenticated, but the token itself doesn't re-prompt.

## Is my code sent anywhere other than Azure DevOps?

Not unless you've explicitly enabled AI features and configured a provider. See [Privacy and Data](Privacy-and-Data.md) for the full per-feature data flow.

If AI is disabled (the master switch is off), the plugin makes zero outbound calls beyond your Azure DevOps org.

## How can I use the plugin without any AI calls?

Uncheck **Enable AI assistance** at the top of <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path>. Every AI affordance disappears from menus and toolbars, and no AI calls are made.

You can also leave AI on and route every feature to a local **Ollama** instance for fully on-device inference.

## Where do I see PR metrics?

The [Statistics](Statistics.md) tab shows KPIs and charts — time-to-merge, review velocity, vote distribution, and more — computed locally from cached data. It's a view-only dashboard; for exportable, org-wide reporting use Azure DevOps Analytics.

## What's the memory and CPU footprint?

The plugin is a thin Swing UI over the IDE's bundled `collaboration-tools` toolkit (same toolkit used by the GitHub plugin). On idle it adds ~30-60 MB of heap on top of the IDE's baseline. Active syncing — fetching PR lists, comments, and diffs — adds a few MB more.

For huge orgs (1000+ PRs across many repos), the PR list virtualizes — only visible rows hold UI components.

## Does the plugin upload anything anonymously? Telemetry?

No. The shipping version doesn't collect telemetry, crash reports, or usage analytics. The only outbound calls are to your Azure DevOps org and (if AI is enabled) your configured AI provider. See [Privacy and Data](Privacy-and-Data.md).

## Does it support Azure Repos Wiki?

No. The plugin is scoped to Pull Requests. For wiki editing, use Azure DevOps' web UI.
