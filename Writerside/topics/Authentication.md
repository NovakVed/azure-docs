# Authentication

The plugin signs in two ways — a **Personal Access Token (PAT)** or **Microsoft Entra ID (OAuth)**. Both store credentials in the IDE's system-backed keychain.

## Which method should I use?

| Use… | When |
|------|------|
| **Personal Access Token** | Works everywhere, including on-prem Azure DevOps Server. The token itself doesn't re-prompt for MFA. |
| **Microsoft (OAuth)** | Cloud `dev.azure.com` only. Honors your org's SSO/MFA on every sign-in; tokens refresh automatically. |

Both reach every sign-in through the **`+`** button in the accounts panel, which opens a small popup:

![The add-account popup: Log In with Token and Log In via Microsoft](add-account-menu.png){ width="420" border-effect="line" }

> On on-prem Azure DevOps Server, **Log In via Microsoft…** is disabled with the tooltip *"Microsoft sign-in is only available for Azure DevOps Services (dev.azure.com). Use a Personal Access Token for on-prem Azure DevOps Server."*
> {style="note"}

## Sign in with a Personal Access Token

### 1. Generate a token

You can let the plugin take you there: the login dialog's **Generate…** button opens your organization's Personal Access Tokens page in the browser. Or do it by hand:

<procedure title="Generate a token in Azure DevOps">
    <step>Open Azure DevOps, click your avatar (top right) → <b>Personal access tokens</b>.</step>
    <step>Click <b>+ New Token</b>, set a name, organization, and expiry.</step>
    <step>Grant the scopes below (or just pick <b>Full access</b>).</step>
    <step>Click <b>Create</b> and copy the token — Azure DevOps shows it only once.</step>
</procedure>

The plugin uses these scopes (the login dialog lists them):

| Scope (in the PAT UI) | Powers |
|-----------------------|--------|
| **Code** → *Read &amp; write + Status* | Reading PRs and diffs, commenting, voting, completing/abandoning, and branch-policy/status checks. **Required.** |
| **User Profile** → *Read* | Your profile and reviewer avatars. |
| **Identity** → *Read* | @-mention autocomplete. |
| **Work Items** → *Read* | Linked work items on a PR and the Work Items filter. |
| **Security** → *Manage* | The permission check that enables the **Override branch policies** option in the Complete dialog. |

> **Quick recipe:** if you just want everything to work, pick **Full access**. The granular scopes above are for stricter security policies.
> {style="tip"}

### 2. Add it to the plugin

<procedure title="Sign in with a token">
    <step>In the Pull Requests tool window (or <ui-path>Settings | Version Control | Azure DevOps</ui-path>), click <b>+</b> → <b>Log In with Token…</b>.</step>
    <step>Fill in the two fields:
        <ul>
            <li><b>Server</b> — a full URL (<code>https://dev.azure.com/your-org</code>), a bare org slug (<code>your-org</code>), a legacy <code>visualstudio.com</code> URL, or an on-prem URL (<code>https://tfs.example.com/tfs/your-collection</code>). There is no separate organization field — the org is read from this one.</li>
            <li><b>Token</b> — paste the PAT.</li>
        </ul>
    </step>
    <step>Click <b>Log In</b>. The plugin validates the token ("Validating credentials…") and your tool window populates.</step>
</procedure>

![The Log In to Azure DevOps dialog with the Server and Token fields](pat-login-dialog.png){ width="520" border-effect="line" }

### Rotate or revoke a token

<procedure title="Rotate a token">
    <step>In Azure DevOps, create a new token with the same scopes and copy it.</step>
    <step>In <ui-path>Settings | Version Control | Azure DevOps</ui-path>, click the <b>pencil</b> icon on the account row and paste the new token. (The Server field is locked while editing — only the token changes.)</step>
    <step>Back in Azure DevOps, revoke the old token.</step>
</procedure>

If a token is revoked or expires, the plugin shows **Log In Again** in the tool window — click it to paste a fresh token.

## Sign in with Microsoft (OAuth)

For cloud organizations that prefer SSO, sign in via Microsoft Entra ID.

<procedure title="Sign in with Microsoft">
    <step>Click <b>+</b> → <b>Log In via Microsoft…</b>.</step>
    <step>In <b>Sign in with Microsoft</b>, choose a permission tier (below) and click <b>Continue</b>.</step>
    <step>Authenticate in the browser (MFA included). The page redirects back to the IDE over a local loopback and shows <b>"Sign-in complete. You can close this tab."</b></step>
</procedure>

![The Sign in with Microsoft permission picker](oauth-scope-dialog.png){ width="480" border-effect="line" }

Refresh tokens renew automatically (with a 60-second leeway before expiry), so you stay signed in across sessions.

### Permission tiers {id="oauth-permission-tiers"}

| Tier | What you get | What you don't |
|------|--------------|----------------|
| **Full access** *(recommended)* | Pull requests, comments, votes, status checks, **plus** avatars, @-mention search, and linked work items. | — |
| **Standard access** | Pull requests and comments only. | Avatars show as initials; @-mention autocomplete returns nothing; work-item links don't render. |

> To change tiers later, remove the account and sign in again — the picker reappears on every fresh sign-in.
> {style="tip"}

## Multiple accounts

Sign into several Azure DevOps organizations at once. Each row in <ui-path>Settings | Version Control | Azure DevOps</ui-path> shows the avatar, display name, organization URL, and auth type, with a **pencil** (edit) and **✕** (remove) per row.

![The Azure DevOps accounts panel in Settings](accounts-panel.png){ width="700" border-effect="line" }

Each project remembers its own **default account** (stored in the project's workspace) — the one used for that project's API calls and Git HTTPS handoff.

## Credential storage

PATs and OAuth refresh tokens live in the IDE's PasswordSafe, backed by the OS keychain:

<tabs>
    <tab title="macOS">Keychain — one entry per signed-in account.</tab>
    <tab title="Windows">Credential Manager (DPAPI-encrypted).</tab>
    <tab title="Linux">KWallet / Secret Service if available, otherwise an encrypted file in the IDE config directory.</tab>
</tabs>

Switch storage modes in <ui-path>Settings | Appearance &amp; Behavior | System Settings | Passwords</ui-path>.

## Sign out

In <ui-path>Settings | Version Control | Azure DevOps</ui-path>, click the **✕** on an account row and **Apply**. The token is deleted from the keychain and any cached data for that account is cleared.

## Common sign-in errors

| Message | Likely cause |
|---------|--------------|
| **Token invalid or expired** | Wrong/expired PAT, or missing scopes. Create a new one with at least *Code (Read &amp; write)*. |
| **Organisation not found** | The Server field's org doesn't exist or you can't access it. |
| **Couldn't reach Azure DevOps** | Network/proxy issue — check <ui-path>Settings &#124; System Settings &#124; HTTP Proxy</ui-path>. |
| **403 Forbidden** on an action | Your account lacks the project/repo permission — ask your org admin. |

For more, see [Troubleshooting](Troubleshooting.md).
