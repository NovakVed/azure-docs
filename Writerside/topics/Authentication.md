# Authentication

The plugin supports two authentication methods: Personal Access Token (PAT) and OAuth2 via Microsoft Entra ID. Both store credentials in the IDE's system-backed keychain.

## Personal Access Token (PAT)

A PAT is the simplest way to authenticate. It's a long-lived secret you generate from Azure DevOps that the plugin sends with every API request.

### Create a PAT

<procedure title="Generate a Personal Access Token">
    <step>Open Azure DevOps in a browser and click your avatar (top right).</step>
    <step>Choose <b>Personal access tokens</b>.</step>
    <step>Click <b>+ New Token</b>.</step>
    <step>Set a name, organization, and expiration date.</step>
    <step>Select the scopes (see table below).</step>
    <step>Click <b>Create</b> and copy the token — Azure DevOps shows it only once.</step>
</procedure>

### Required scopes

| Scope                          | Required for                                                                            |
|--------------------------------|-----------------------------------------------------------------------------------------|
| **Code (Read)**                | Browsing PRs, reading diffs, viewing comments. Minimum.                                 |
| **Code (Read & Write)**        | Voting, commenting, creating PRs, replying to threads, marking files viewed.            |
| **Profile (Read)**             | Displaying user avatars and names.                                                      |
| **Identity (Read)**            | @-mention autocomplete in the comment editor.                                           |
| **Work Items (Read)**          | Showing linked work items in the PR overview.                                           |
| **Build (Read)**               | Status checks from Azure Pipelines on the overview tab.                                 |

> **Quick recipe**: if you just want everything to work, pick **Full access** and you're done. The granular scopes above are for users with stricter security requirements.
> {style="tip"}

### Rotate or revoke a PAT

Tokens are long-lived secrets — rotate them on the cadence your security policy requires (90 days is a common default).

<procedure title="Rotate a PAT">
    <step>In Azure DevOps, open your avatar (top right) → <b>Personal access tokens</b>.</step>
    <step>Click <b>+ New Token</b> with the same scopes as the old one. Copy the new token.</step>
    <step>In the IDE, open <ui-path>Settings | Version Control | Azure DevOps</ui-path>, select the account, and click <b>Edit credentials</b>. Paste the new token.</step>
    <step>Back in Azure DevOps, find the old PAT in the same list and click <b>Revoke</b>.</step>
</procedure>

A PAT can be revoked at any time from the same Azure DevOps page. Once revoked, the IDE shows a 401 on its next API call — re-edit credentials with a fresh token.

### Add the PAT to the plugin

<procedure title="Sign in with PAT">
    <step>Open the <b>Pull Requests</b> tool window.</step>
    <step>Click <b>Sign in</b> (or open <ui-path>Settings | Version Control | Azure DevOps | +</ui-path> to add another account).</step>
    <step>Choose <b>Personal Access Token</b>.</step>
    <step>Fill in:
        <ul>
            <li><b>Server URL</b> — usually <code>https://dev.azure.com</code> (default). For self-hosted Azure DevOps Server, enter the full URL.</li>
            <li><b>Organization</b> — your Azure DevOps organization slug (e.g. <code>my-company</code>).</li>
            <li><b>Token</b> — paste the PAT.</li>
        </ul>
    </step>
    <step>Click <b>Sign in</b>. The plugin validates the token and your tool window populates.</step>
</procedure>

## OAuth2 (Microsoft Entra ID)

For organizations that disable PATs or prefer SSO, the plugin supports OAuth2 via Microsoft Entra ID (formerly Azure AD). OAuth is only available against `dev.azure.com` (Azure DevOps Services) — on-prem Azure DevOps Server installations must use a PAT because the Microsoft login service can't reach them.

<procedure title="Sign in with Microsoft Entra ID">
    <step>Open the <b>Pull Requests</b> tool window and click <b>Log In via Microsoft…</b>, or open <ui-path>Settings | Version Control | Azure DevOps | +</ui-path> and choose <b>Log In via Microsoft…</b>.</step>
    <step>A small dialog asks which permissions to request — pick <b>Full access</b> (default) or <b>Standard access</b>. See <a href="#oauth-permission-tiers">Permission tiers</a> below to decide.</step>
    <step>Click <b>Continue</b>. A browser tab opens with the Microsoft login page.</step>
    <step>Authenticate (including MFA if your org enforces it) and approve the requested scopes.</step>
    <step>The browser redirects back to the IDE via a loopback handler on <code>127.0.0.1</code>. The plugin stores the resulting refresh token.</step>
</procedure>

Refresh tokens are renewed automatically. If your organization requires re-authentication periodically you'll be prompted in the IDE.

### Permission tiers {id="oauth-permission-tiers"}

Before opening the browser the plugin asks which scope set to request. Both tiers cover the core PR review workflow; the difference is what extra org-directory data the plugin can fetch.

| Tier                       | What you get                                                                                                                                            | What you don't get                                                                                       |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Full access** *(default)* | Pull requests, comments, votes, status checks, **plus** user avatars, @-mention search in the comment editor, and linked work items on the overview tab. | —                                                                                                        |
| **Standard access**        | Pull requests, comments, votes, status checks.                                                                                                          | User avatars appear as initials, @-mention autocomplete returns no suggestions, and linked work items don't render in PR details. |

> **Picking a tier**: choose Full unless your org has a stated policy against the org-directory scopes (`vso.profile`, `vso.identity`, `vso.work`). To change tiers later, sign out of the account in <ui-path>Settings | Version Control | Azure DevOps</ui-path> and sign back in — the scope picker shows again on every fresh sign-in.
> {style="tip"}

> **Mark files as viewed** is local to your machine (state lives in the IDE workspace, not in Azure DevOps), so it works on both tiers regardless of which scopes you grant.
> {style="note"}

> **MFA & OAuth**: if your org enforces multi-factor auth, the browser OAuth flow handles it inline — the MFA prompt happens before the IDE callback. PATs, by contrast, bypass MFA by design (you authenticated with MFA to generate the PAT; the token itself doesn't re-prompt). Pick OAuth if you want every IDE session to honor your MFA policy.
> {style="note"}

> **OAuth callback handler**: the plugin registers a custom URL handler the first time you launch it. If you've disabled custom URL handlers at the OS level, OAuth won't be able to complete the round-trip — fall back to PAT in that case. See [Troubleshooting](Troubleshooting.md) for OS-specific recovery steps.
> {style="warning"}

## Multiple accounts

You can sign into multiple Azure DevOps organizations at once. Each project can have its own **default account**, which controls which credentials are used for that project's API calls.

To manage accounts:

<procedure>
    <step>Open <ui-path>Settings | Version Control | Azure DevOps</ui-path>.</step>
    <step>The Accounts panel lists every signed-in identity.</step>
    <step>Click <b>+</b> to add another, or select an account and click the gear to set it as the default for the current project.</step>
</procedure>

## Credential storage

PATs and OAuth refresh tokens are stored in the IDE's password-safe, which is backed by the OS keychain:

<tabs>
    <tab title="macOS">
        Keychain Access — the IDE creates an entry per signed-in account.
    </tab>
    <tab title="Windows">
        Credential Manager (DPAPI-encrypted).
    </tab>
    <tab title="Linux">
        KWallet or Secret Service (if available), otherwise an encrypted file in the IDE config directory.
    </tab>
</tabs>

You can switch storage modes in <ui-path>Settings | Appearance &amp; Behavior | System Settings | Passwords</ui-path>.

## Sign out

Open <ui-path>Settings | Version Control | Azure DevOps</ui-path>, select an account, and click **Remove**. The token is deleted from the keychain immediately.

## Troubleshooting auth

Common issues:

| Symptom                                   | Likely cause                                                                                          |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **401 Unauthorized** after sign-in        | Token lacks required scope, or has expired. Regenerate with at least *Code (Read & Write)*.           |
| **403 Forbidden** on specific actions     | Project-level permissions in Azure DevOps deny the action — ask your org admin.                       |
| **Browser doesn't return to IDE** during OAuth | Custom URL handler is blocked. Use PAT instead, or check your default browser settings.          |
| **"No accounts" after restart**           | Password safe is locked. Open <ui-path>Settings &#124; Passwords</ui-path> and re-enter the master password. |

For anything else, see [Troubleshooting](Troubleshooting.md).
