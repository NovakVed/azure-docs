# Quick Start

From zero to your first PR review in about a minute. This page assumes you've already [installed](Installation.md) the plugin.

## 1. Open a project hosted on Azure DevOps

Clone any Azure DevOps repository the usual way:

```bash
git clone https://dev.azure.com/your-org/your-project/_git/your-repo
cd your-repo
```

Open the folder in your IDE. The plugin scans Git remotes on startup - when it sees a `dev.azure.com` or `*.visualstudio.com` remote it activates and shows the **Pull Requests** tool window.

> **Don't see the tool window?** The plugin hides itself when no Azure DevOps remote is detected. Run `git remote -v` to confirm a remote URL contains `dev.azure.com`.
> {style="note"}

## 2. Sign in

Open the Pull Requests tool window from the left sidebar. On its sign-in screen you have two options:

- **Log In with Token…** - paste a Personal Access Token from your Azure DevOps user settings. The fastest path, and the only option for on-prem Azure DevOps Server.
- **Log In via Microsoft…** - a browser-based OAuth sign-in via Microsoft Entra ID (cloud `dev.azure.com` only). A dialog first asks whether to grant **Full access** or **Standard access**.

![The Sign in with Microsoft permission picker, showing Full access (recommended) and Standard access](oauth-scope-dialog.png){ width="520" border-effect="line" }

If you choose a token, the plugin needs these scopes: **Code (Read &amp; write + Status), User Profile (Read), Identity (Read), Work Items (Read), Security (Manage)**. The login dialog lists them, and its **Generate…** button opens your org's token page in the browser.

> See [Authentication](Authentication.md) for the full sign-in flow, scopes, and the Full vs Standard tier choice.
> {style="note"}

## 3. Browse pull requests

After signing in, the tool window lists the repository's pull requests.

![The Pull Requests tool window with the search field, filter chips, and a populated list](pr-tool-window.png){ width="720" border-effect="line" }

To narrow the list:

- **Quick Filters** - click the filter icon on the left of the chip row for one-click presets: **Open pull requests**, **Awaiting my review**, **Involving me**.
- **Filter chips** - **State** (Active / Completed / Abandoned), **Author**, **Tags**, **Assignee**, **Review** (your vote state), **Work Items**, and **Draft**.
- **Sort** - the last chip: Newest, Oldest, Most/Least commented, or Recently/Least recently updated.
- **Search** - type in the field above the chips to match PR titles and descriptions.

**Click** any PR to open its detail view in an editor tab.

> **No PRs showing up?** Usual causes: (1) your account can't access this repo - open it in the Azure DevOps web UI first; (2) the project points at multiple orgs - switch via the tool-window gear → **Switch Account / Repository…**; (3) there genuinely are no active PRs - set the **State** chip to **Completed** to confirm the connection works.
> {style="note"}

## 4. Review the code

The detail view is a **single pane** - no sub-tabs. From top to bottom: the title with `!`-number and a **View Timeline** link, the source → target branches, the status checks with each reviewer's vote, the changed-files tree, and an action bar.

![A pull request open in the single-pane detail view](pr-detail.png){ width="720" border-effect="line" }

- **Read the diff** - click any file in the changes tree to open the diff. Click a line's gutter to comment.
- **Read discussion** - click **View Timeline** to open the full comment timeline in its own tab.
- **Vote** - the action bar's **Approve** button is a split button. Its dropdown holds **Approve with suggestions**, **Wait for author**, **Reject**, and **Reset feedback**.

![The Approve split-button with its vote options expanded](vote-approve-dropdown.png){ width="380" border-effect="line" }

> **Review without leaving the editor:** check out a PR's branch and the plugin overlays its comments right on your normal editor. See [Review in Editor](Review-in-Editor.md).
> {style="tip"}

## 5. Create a pull request

From the tool-window toolbar, click **+** (Create Pull Request). The form pre-fills the source branch (your current branch) and the default target branch. Add a title, description, and reviewers, then create it.

![Creating a pull request with AI-generated title and description](create-pr-ai.png){ width="640" border-effect="line" }

> **AI-assisted titles &amp; descriptions:** with an [AI provider configured](AI-Features.md), the form's title and description fields gain a **Generate** action that drafts both from your branch's diff.
> {style="tip"}

## Where to go next

- [Pull Requests](Pull-Requests.md) - filtering, search, the action bar, and the overflow menu (Complete, Revert, Compare).
- [Code Review](Code-Review.md) - inline diffs, suggestions, voting, and file-viewed tracking.
- [Notifications &amp; Attention](Notifications-and-Attention.md) - get pinged when a PR needs your review or @mentions you.
- [AI Features](AI-Features.md) - summaries, AI review, and grammar polish.
