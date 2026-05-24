# Git Integration

The plugin integrates with the IDE's bundled Git plugin to detect Azure DevOps remotes, match your current branch to its PR, and hand off HTTPS credentials so `git fetch` and `git push` just work.

## Repository detection

When you open a project, the plugin scans every Git remote and looks for these patterns:

- `https://dev.azure.com/<org>/<project>/_git/<repo>`
- `https://<org>.visualstudio.com/<project>/_git/<repo>` (legacy)
- `git@ssh.dev.azure.com:v3/<org>/<project>/<repo>` (SSH)
- Self-hosted Azure DevOps Server URLs configured in settings

If any remote matches, the **Pull Requests** tool window appears and the plugin starts background sync. Otherwise the plugin stays out of your way.

## Current branch → PR matching

The plugin watches your current Git branch and resolves it to the corresponding open PR (matching by source branch name). When a match is found:

- The Git status bar widget shows the PR number — e.g. `!1234 on feature/login`.
- [Review in Editor](Review-in-Editor.md) turns on so you can comment on changed lines directly in the editor.
- The action **Open Current Branch PR** becomes available.

### What happens when you switch branches

- If the new branch has a PR, the widget updates and Review in Editor stays on.
- If the new branch has no PR, the widget hides and Review in Editor turns off.

## Status bar widget

The Git branch widget in the bottom status bar gets an Azure DevOps badge when applicable:

```text
master  |  feature/login  |  !1234 Update login redirect
```

Click the badge for a popup with quick actions:

- **Open PR** — switch to the detail view.
- **Open in browser**
- **Copy PR link**
- **Update PR description**
- **Mark as draft / ready**

## HTTPS authentication

When Git needs HTTPS credentials to fetch or push from an Azure DevOps remote, the plugin offers the stored PAT to Git automatically:

<procedure title="How HTTPS auth handoff works">
    <step>You run <code>git fetch</code> or <code>git push</code> (from the IDE's <i>Update Project</i>, the Git tool window, or the embedded terminal).</step>
    <step>Git asks the IDE for credentials.</step>
    <step>The plugin matches the remote URL to a signed-in account and supplies the PAT.</step>
    <step>Git proceeds — no password prompt.</step>
</procedure>

If you're signed into multiple accounts that all match the same URL, the plugin uses the project's default account (set in [Settings](Settings.md)).

> Git operations run from your **system shell** (outside the IDE) won't see this credential provider. Configure a Git credential helper system-wide if you do most of your work in the terminal.
> {style="note"}

## Branch popup actions

Click the branch name in the status bar (or use <ui-path>VCS | Branches</ui-path>) and the dropdown gains an **Azure DevOps** section when the current branch has a PR. Actions:

- **Open PR**
- **Update PR description from latest commit**
- **Mark PR as draft / ready for review**
- **Vote** (Approve / Reject / Wait for author)

## Notifications driven by Git events

The plugin listens for VCS events and surfaces relevant Azure DevOps activity:

| Event                                          | Notification                                                   |
|------------------------------------------------|----------------------------------------------------------------|
| You push commits to a branch with an open PR   | Toast confirming the push showed up in the PR.                 |
| You're added as a reviewer to a new PR         | Sticky balloon — click to open the PR.                         |
| Status check on your PR completes              | Toast with pass/fail state.                                    |
| Branch policy fails                            | Toast pointing to the policy that blocked completion.          |

Notification categories: `AzureDevOps.PullRequests` (toast) and `AzureDevOps.PullRequests.Sticky` (balloon). Disable individual categories in <ui-path>Settings | Appearance &amp; Behavior | Notifications</ui-path>.

## Multi-repo projects

If your IntelliJ project contains multiple Git repositories (a monorepo with submodules, or a multi-module setup), each Azure DevOps repo is detected independently. The tool window's **Repository** filter lets you focus on one at a time.

## Self-hosted Azure DevOps Server

The plugin works with Azure DevOps Server (formerly TFS) as well as the cloud product. Configure the server URL in <ui-path>Settings | Version Control | Azure DevOps | Add Account</ui-path> and use a PAT generated from the server.
