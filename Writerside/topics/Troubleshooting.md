# Troubleshooting

Quick fixes for the issues users hit most often. For decision-style questions ("should I use OAuth or PAT?", "does it support on-prem?"), see [FAQ](FAQ.md). If your problem isn't covered here, see [Filing a bug](#filing-a-bug) at the bottom.

## The tool window doesn't appear

The Pull Requests tool window is hidden when no Azure DevOps Git remote is detected. Check:

<procedure>
    <step>Run <code>git remote -v</code> in your project root. At least one remote URL must contain <code>dev.azure.com</code> or <code>visualstudio.com</code> (or your configured self-hosted server).</step>
    <step>Verify the bundled <b>Git</b> plugin (<code>Git4Idea</code>) is enabled in <ui-path>Settings | Plugins | Installed</ui-path>.</step>
    <step>Restart the IDE - the remote scan runs on project open.</step>
</procedure>

## "401 Unauthorized" after signing in

- The PAT may lack required scopes - see [Authentication](Authentication.md). Easiest fix: regenerate with **Full access**.
- The PAT may have expired. Tokens expire on the date you set when creating them.
- Your organization may have disabled PATs - in that case use OAuth.

## "403 Forbidden" on specific actions

The PAT is valid but your Azure DevOps account doesn't have permission for the action (e.g. you can read PRs but not vote, or can't merge). Ask your Azure DevOps administrator to grant the required permission on the project or repository.

## OAuth browser doesn't return to the IDE

OAuth completes via a **local loopback redirect** - the browser is sent back to `http://127.0.0.1:<port>/azure-oauth/callback`, served by the IDE's built-in web server, which then shows *"Sign-in complete. You can close this tab."* If that round-trip fails:

- A firewall or security tool may be blocking localhost connections to the IDE's built-in server (port range **63342–63352**).
- A blocked pop-up or a non-default browser can stop the redirect - make sure your intended browser is the default.
- The sign-in window has a **5-minute** limit; if it lapsed, start over.

Workaround: use a Personal Access Token instead of OAuth.

## PRs don't show new comments after sync

<procedure>
    <step>Press <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> / <shortcut>F5</shortcut> (or right-click → <b>Refresh List</b>) to force a sync immediately - there is no Reload toolbar button.</step>
    <step>Check the <b>idea.log</b> for sync errors (<a anchor="enabling-debug-logs">enable debug logs</a> for more detail).</step>
    <step>Sync interval is 60 s by default. If you've increased it in <a href="Settings.md">Settings</a>, expect a longer delay.</step>
</procedure>

## Inline comments don't appear in the diff

- The plugin only renders inline threads on PRs you have **Code (Read)** permission for.
- If you're viewing the diff from your local working tree (not the PR), inline threads won't render - open the PR from the tool window so its changes tree and threads load.
- If your local branch has diverged from the PR head, review-in-editor disables itself. Push your changes or check out the PR head exactly.

## Git push asks for a password

The plugin's HTTPS credential provider only kicks in for Git operations run **inside the IDE** (terminal launched from within the IDE counts as "inside"). For external terminals, configure a system-level Git credential helper:

```bash
# macOS Keychain
git config --global credential.helper osxkeychain

# Windows
git config --global credential.helper manager

# Linux (libsecret)
git config --global credential.helper libsecret
```

## AI features are missing or return errors

- Open <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path> and confirm **Enable AI assistance** is checked and at least one provider is configured and enabled.
- Click **Test connection** on the provider row - if it fails, double-check API key, model name, and endpoint URL.
- For **Ollama**, confirm the daemon is running locally (`ollama serve`) and the model you specified is pulled (`ollama list`).
- For **CLI providers** (Claude Code, Codex, Copilot CLI), make sure the binary is on `PATH` and signed in (`claude /login`, etc.).
- Provider rate-limit or quota errors come straight from the provider - they're not retried.

## Plugin conflicts

The plugin shares the IDE's `collaboration-tools` toolkit with the bundled **GitHub** plugin and the **GitLab** plugin. It coexists with both - independent tool windows, independent state. Two known interaction points:

- If a project has both an Azure DevOps and a GitHub remote, both tool windows appear; right-click context menus may surface actions from each.
- If a third-party plugin overrides the AI extension points (`intellij.vcs.azuredevops.aiSummaryExtension` etc., see [Privacy and Data](Privacy-and-Data.md)), the built-in default is bypassed for that feature. If AI features behave unexpectedly, check <ui-path>Settings | Plugins</ui-path> for other Azure DevOps or AI plugins that may be hooking the EPs.

## Network timeouts or "request failed"

The plugin uses IntelliJ's HTTP proxy configuration - there's no separate proxy setting. If corporate network restrictions block outbound HTTPS:

- Check <ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path>. The plugin honours whatever you set here.
- The HTTP timeout for AI streaming requests is **5 minutes**. Anything longer is surfaced as a hang and reported as a notification.
- The retry behaviour for Azure DevOps API calls is "fail fast" - transient errors aren't retried so the UI doesn't pile up duplicate calls. The 60-second background sync picks up where a failed request left off.

## Plugin update broke something

Roll back to a previous version:

<procedure>
    <step>Open <ui-path>Settings | Plugins | Installed</ui-path>, find <b>Azure DevOps Pull Requests</b>.</step>
    <step>Click the gear icon → <b>Manage Plugin Versions</b>.</step>
    <step>Pick an older version and install it.</step>
    <step>Restart the IDE.</step>
</procedure>

## Enabling debug logs {id="enabling-debug-logs"}

For deeper troubleshooting, enable trace logging:

<procedure>
    <step>Open <ui-path>Help | Diagnostic Tools | Debug Log Settings…</ui-path></step>
    <step>Add lines:
        <code-block lang="text">
#com.vednovak.azure
#com.vednovak.azure.sync
#com.vednovak.azure.api
        </code-block>
    </step>
    <step>Reproduce the issue.</step>
    <step>Open <ui-path>Help | Show Log in Explorer/Finder</ui-path> to find <code>idea.log</code>.</step>
</procedure>

The log lives in your IDE's caches directory:

<tabs>
    <tab title="macOS">
        <code>~/Library/Logs/JetBrains/&lt;IDE&gt;&lt;Version&gt;/idea.log</code>
    </tab>
    <tab title="Windows">
        <code>&#37;LOCALAPPDATA&#37;\JetBrains\&lt;IDE&gt;&lt;Version&gt;\log\idea.log</code>
    </tab>
    <tab title="Linux">
        <code>~/.cache/JetBrains/&lt;IDE&gt;&lt;Version&gt;/log/idea.log</code>
    </tab>
</tabs>

## Filing a bug {id="filing-a-bug"}

If you've found a reproducible issue:

<procedure>
    <step>Run <ui-path>Help | Diagnostic Tools | Collect Logs and Diagnostic Data</ui-path>.</step>
    <step>Open <a href="%repo_url%/issues/new">a new GitHub issue</a> and include:
        <ul>
            <li>Your IDE version (<b>About</b>)</li>
            <li>Plugin version</li>
            <li>OS &amp; architecture</li>
            <li>Steps to reproduce</li>
            <li>Expected vs actual behavior</li>
            <li>A scrubbed <code>idea.log</code> snippet (remove tokens before posting)</li>
        </ul>
    </step>
</procedure>

> **Never paste PATs or OAuth refresh tokens** in a public issue. The log captures redacted tokens by default, but always double-check before submitting.
> {style="warning"}

