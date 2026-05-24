# Quick Start

From zero to your first PR review in under a minute. This page assumes you've already [installed](Installation.md) the plugin.

## 1. Open a project hosted on Azure DevOps

Clone any Azure DevOps repository the usual way:

```bash
git clone https://dev.azure.com/your-org/your-project/_git/your-repo
cd your-repo
```

Open the folder in your IDE. The plugin scans Git remotes on startup — when it sees a `dev.azure.com` or `*.visualstudio.com` remote it activates and shows the **Pull Requests** tool window.

> **Don't see the tool window?** The plugin hides itself when no Azure DevOps remote is detected. Run `git remote -v` to confirm the URL contains `dev.azure.com`.
> {style="note"}

## 2. Sign in

Open the Pull Requests tool window (left sidebar) and click **Sign in**. You'll see two options:

- **Log In with Token…** — paste a PAT from your Azure DevOps user settings. Fastest path.
- **Log In via Microsoft…** — opens a browser-based OAuth flow via Microsoft Entra ID. A small dialog asks whether to grant **Full access** (everything the plugin can do) or **Standard access** (PR review essentials only; no avatars, @-mention search, or work-item links) before the browser opens.

If you choose PAT, the minimum required scope is **Code (Read)**. For voting, commenting, and creating PRs, use **Code (Read & Write)**.

See [Authentication](Authentication.md) for full details on scopes, OAuth setup, and the Full vs Standard tier choice.

## 3. Browse pull requests

After signing in, the tool window populates with all PRs in the current repository.

> **No PRs showing up?** Three usual causes: (1) your account doesn't have access to this repo — try opening it in the Azure DevOps web UI first; (2) the project has multiple Azure DevOps remotes pointing at different orgs — set the default account at <ui-path>Settings | Version Control | Azure DevOps</ui-path>; (3) the repository genuinely has no open PRs — flip the State filter to **Completed** to confirm the connection is working.
> {style="note"}

You can:

- **Filter** by state (Open / Draft / Completed / Abandoned), repository, author, label, or reviewer using the chip bar at the top.
- **Sort** by creation date, update date, or number.
- **Search** within the list — or use *Search Everywhere* (<shortcut>⇧ Shift</shortcut> twice) to find PRs from anywhere.

Double-click any PR to open its detail view in an editor tab.

## 4. Review code

The detail view has three tabs:

- **Overview** — title, description, status checks, branch policies, reviewers, work items.
- **Files** — the full diff. Click any line gutter to add an inline comment.
- **Discussion** — every comment thread in a chronological timeline.

When you've finished reviewing, hit the vote button: **Approve**, **Approve with suggestions**, **Wait for author**, or **Reject**.

> **Review without leaving the editor**: when you check out a branch that has an open PR, the plugin overlays the diff comments directly on your editor. See [Code Review](Code-Review.md) for details.
> {style="tip"}

## 5. Create a pull request

From the tool window toolbar, click the **+** button to launch the Create PR wizard. The plugin pre-fills the source branch (your current branch) and the default target branch.

Add a title, description, and reviewers, then click **Create**. Optionally, mark the PR as a **Draft** if it isn't ready for review yet.

## Where to go next

- [Authentication](Authentication.md) — set up PAT scopes, OAuth, and multi-account.
- [Pull Requests](Pull-Requests.md) — filtering, sorting, search, and the create wizard.
- [Code Review](Code-Review.md) — inline diffs, file-viewed tracking, review-in-editor.
- [AI Features](AI-Features.md) — summaries, AI reviews, and commit message drafts.
