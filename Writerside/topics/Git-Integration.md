# Git Integration

The plugin works with the IDE's bundled Git plugin to detect Azure DevOps remotes, match your current branch to its PR, and hand off HTTPS credentials so `git fetch` and `git push` just work.

## Repository detection

When you open a project, the plugin scans every Git remote for these patterns:

- `https://dev.azure.com/<org>/<project>/_git/<repo>`
- `https://<org>.visualstudio.com/<project>/_git/<repo>` (legacy)
- `git@ssh.dev.azure.com:v3/<org>/<project>/<repo>` (SSH)
- Self-hosted Azure DevOps Server URLs from your accounts

If any remote matches, the **Pull Requests** tool window appears and background sync starts. Otherwise the plugin stays out of your way.

## Current branch → PR

The plugin watches your checked-out branch and resolves it to the matching open PR (by source-branch name). When it finds one, two widgets light up.

### Main-toolbar branch widget

The Git branch widget in the **main toolbar** gains an Azure DevOps badge - `!1234 on feature/login`. Click it for the PR's actions:

![The main-toolbar branch widget popup](branch-widget-popup.png){ width="440" border-effect="line" }

- **Show in Tool Window** - open the PR's detail view.
- **Update Pull Request Branch** - appears when your local branch has diverged from the PR head (runs *Update Project*).
- **Review in Editor** - toggle the in-editor review overlay. See [Review in Editor](Review-in-Editor.md).

### Status-bar widget

A separate widget in the **status bar** shows `ADO PR !1234`. Click it to open that PR in the tool window. (Hide or show it via the status-bar widget chooser - its name is *Azure DevOps PR (current branch)*.)

When you switch branches, both widgets update - and disappear when the new branch has no PR.

## HTTPS authentication

When Git needs HTTPS credentials for an Azure DevOps remote, the plugin supplies the stored token automatically:

<procedure title="How HTTPS auth handoff works">
    <step>You run <code>git fetch</code> or <code>git push</code> from inside the IDE (Update Project, the Git tool window, or the embedded terminal).</step>
    <step>Git asks the IDE for credentials.</step>
    <step>The plugin matches the remote to a signed-in account and supplies its token.</step>
    <step>Git proceeds - no password prompt.</step>
</procedure>

If several signed-in accounts match the same URL, the project's **default account** is used (see [Settings](Settings.md)).

> Git commands run from a **system shell** outside the IDE won't see this provider. Configure a system-wide Git credential helper if you mostly work in an external terminal - see [Troubleshooting](Troubleshooting.md#git-push-asks-for-a-password).
> {style="note"}

## Push → Create PR

After you push a branch with no PR yet, the plugin can offer to **Create a pull request** in a balloon - a faster path than the toolbar. Toggle it with **Offer Create PR after I push to an Azure DevOps remote** in [Settings](Settings.md). Other Git-driven notifications (review requests, vote changes, replies) are covered in [Notifications &amp; Attention](Notifications-and-Attention.md).

## Multi-repo and self-hosted

- **Multiple repositories** in one project are each detected independently; use the tool-window **Switch Account / Repository…** to focus on one.
- **Azure DevOps Server (on-prem)** works just like the cloud product - add the server URL when signing in, with a token generated from that server.
