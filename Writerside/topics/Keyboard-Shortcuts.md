# Keyboard Shortcuts

Every action the plugin contributes, grouped by surface. To rebind any of them, see [How to rebind](#rebind).

## In the editor (review-in-editor)

| Action | macOS | Windows / Linux | Action ID |
|--------|-------|------------------|-----------|
| **Add Review Comment** | <shortcut>⌘⇧M</shortcut> | <shortcut>Ctrl+Shift+M</shortcut> | `AzureDevOps.PullRequest.AddCommentAtCursor` |
| **Copy Link to Code** | <shortcut>⌘⇧L</shortcut> | <shortcut>Ctrl+Shift+L</shortcut> | `AzureDevOps.PullRequest.CopyCodeLink` |

Only fires when the caret is on a changed line of a file in an open PR. See [Review in Editor](Review-in-Editor.md).

## In the diff viewer

| Action | macOS | Windows / Linux | Action ID |
|--------|-------|------------------|-----------|
| **Mark File as Viewed** | <shortcut>⌘⇧S</shortcut> | <shortcut>Ctrl+Shift+S</shortcut> | `AzureDevOps.PullRequest.MarkFileAsViewed` |
| **Add Review Comment** | <shortcut>⌘⇧M</shortcut> | <shortcut>Ctrl+Shift+M</shortcut> | `AzureDevOps.PullRequest.AddCommentAtCursor` |
| **Copy Link to Code** | <shortcut>⌘⇧L</shortcut> | <shortcut>Ctrl+Shift+L</shortcut> | `AzureDevOps.PullRequest.CopyCodeLink` |
| Next / previous changed range | <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> | <shortcut>F7</shortcut> / <shortcut>Shift+F7</shortcut> | *built-in IntelliJ diff* |

## In the PR list, timeline, and detail view

| Action | Shortcut | Action ID |
|--------|----------|-----------|
| **Refresh List** | <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> / <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.List.Reload` |
| **Refresh Timeline** | <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.Timeline.Update` |
| **Refresh Pull Request** | <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.Details.Reload` |
| **View Pull Request** | *no default* | `AzureDevOps.PullRequest.Show` |
| **View Pull Request in Browser** | *no default* | `AzureDevOps.PullRequest.Open.Link` |
| **Copy Pull Request URL** | *no default* | `AzureDevOps.PullRequest.Copy.Link` |
| **Show in Tool Window** | *no default* | `AzureDevOps.Pull.Request.Show.In.Toolwindow` |

> The Pull Requests tool window has no Reload button — refresh is keyboard-only (or right-click → **Refresh List**).
> {style="note"}

## Branch widget / VCS menu

| Action | Shortcut | Action ID |
|--------|----------|-----------|
| **Open Current Branch PR** | *no default* | `AzureDevOps.OpenCurrentBranchPr` |
| **Update Pull Request Branch** | *no default* | `AzureDevOps.Pull.Request.Branch.Update` |
| **Review in Editor** | *no default* | `AzureDevOps.Pull.Request.Review.In.Editor.Toggle` |
| **Go to Pull Requests…** | <shortcut>⌘⇧P</shortcut> / <shortcut>Ctrl+Shift+P</shortcut> | `AzureDevOps.PullRequest.GoTo` |

## AI actions

| Action | Shortcut | Action ID |
|--------|----------|-----------|
| **Summarize Pull Request** | *no default* | `AzureDevOps.PullRequest.AI.Summarize` |
| **Run AI Review** | *no default* | `AzureDevOps.PullRequest.AI.Review` |
| **Explain This File** | *no default* | `AzureDevOps.PullRequest.AI.Explain` |
| **Generate Commit Message with AI** | *no default* | `AzureDevOps.AI.GenerateCommitMessage` |

These need an AI provider configured — see [AI Features](AI-Features.md).

## How to rebind {id="rebind"}

<procedure title="Bind a shortcut">
    <step>Open <ui-path>Settings | Keymap</ui-path>.</step>
    <step>Type <code>AzureDevOps</code> in the search box to filter to the plugin's actions (it matches action IDs as well as display names).</step>
    <step>Double-click an action → <b>Add Keyboard Shortcut</b>.</step>
    <step>Press the combination. If it collides, IntelliJ warns you and offers to remove the conflict.</step>
    <step>Click <b>OK</b>.</step>
</procedure>

> Use the **action ID** column when filing a bug — it identifies the exact action across IDE versions where display names sometimes differ.
> {style="tip"}
