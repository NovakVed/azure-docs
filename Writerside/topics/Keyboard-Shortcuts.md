# Keyboard Shortcuts

Every shortcut the plugin uses, in one place. There are two kinds:

- **IDE actions** — registered with the IDE, shown in their menus, and **rebindable** in <ui-path>Settings | Keymap</ui-path> (search `AzureDevOps`). Each has an **Action ID**.
- **Composer keys** — built into the comment / description editor and active only while it's focused. They aren't in Keymap and can't be rebound.

> On macOS, <shortcut>⌘</shortcut> is Command and <shortcut>⌃</shortcut> is **Control** — most actions use ⌘, but a few use ⌃. Windows / Linux use <shortcut>Ctrl</shortcut>.
> {style="note"}

## In the editor (review-in-editor)

| Action | macOS | Windows / Linux | Action ID |
|--------|-------|------------------|-----------|
| **Add Review Comment** | <shortcut>⌃⇧M</shortcut> | <shortcut>Ctrl+Shift+M</shortcut> | `AzureDevOps.PullRequest.AddCommentAtCursor` |
| **Copy Link to Code** | <shortcut>⌘⇧L</shortcut> | <shortcut>Ctrl+Shift+L</shortcut> | `AzureDevOps.PullRequest.CopyCodeLink` |

Only fires when the caret is on a changed line of a file in an open PR. See [Review in Editor](Review-in-Editor.md).

## In the diff viewer

| Action | macOS | Windows / Linux | Action ID |
|--------|-------|------------------|-----------|
| **Mark File as Viewed** | <shortcut>⌘⇧S</shortcut> | <shortcut>Ctrl+Shift+S</shortcut> | `AzureDevOps.PullRequest.MarkFileAsViewed` |
| **Add Review Comment** | <shortcut>⌃⇧M</shortcut> | <shortcut>Ctrl+Shift+M</shortcut> | `AzureDevOps.PullRequest.AddCommentAtCursor` |
| **Copy Link to Code** | <shortcut>⌘⇧L</shortcut> | <shortcut>Ctrl+Shift+L</shortcut> | `AzureDevOps.PullRequest.CopyCodeLink` |
| Next / previous changed range | <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> | <shortcut>F7</shortcut> / <shortcut>Shift+F7</shortcut> | *built-in IntelliJ diff* |

## In the comment composer

These work while a comment, reply, or PR-description editor is focused. They're built into the composer (not in Keymap), so they're identical on every platform apart from the modifier key.

| Action | macOS | Windows / Linux |
|--------|-------|------------------|
| **Bold** | <shortcut>⌘B</shortcut> | <shortcut>Ctrl+B</shortcut> |
| **Italic** | <shortcut>⌘I</shortcut> | <shortcut>Ctrl+I</shortcut> |
| **Inline code** | <shortcut>⌘E</shortcut> | <shortcut>Ctrl+E</shortcut> |
| **Insert link** | <shortcut>⌘K</shortcut> | <shortcut>Ctrl+K</shortcut> |
| **Mention user** (`@`) | <shortcut>⇧⌘M</shortcut> | <shortcut>Ctrl+Shift+M</shortcut> |
| **Bulleted list** | <shortcut>⇧⌘8</shortcut> | <shortcut>Ctrl+Shift+8</shortcut> |
| **Numbered list** | <shortcut>⇧⌘7</shortcut> | <shortcut>Ctrl+Shift+7</shortcut> |
| **Task list** | <shortcut>⇧⌘9</shortcut> | <shortcut>Ctrl+Shift+9</shortcut> |
| **Paste image** | <shortcut>⌘V</shortcut> | <shortcut>Ctrl+V</shortcut> |
| **Submit** (Comment / Reply / Save) | <shortcut>⌘↵</shortcut> | <shortcut>Ctrl+Enter</shortcut> |
| **Cancel / close editor** | <shortcut>⎋</shortcut> | <shortcut>Esc</shortcut> |

> Two similar shortcuts, different jobs: **Mention user** (<shortcut>⇧⌘M</shortcut>) inserts an `@mention` *inside* a composer, while **Add Review Comment** (<shortcut>⌃⇧M</shortcut>) *starts* a new comment at the caret in the editor or diff.
> {style="note"}

## In the PR list, timeline, and detail view

| Action | Shortcut | Action ID |
|--------|----------|-----------|
| **Refresh List** | <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> / <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.List.Reload` |
| **Refresh Timeline** | <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.Timeline.Update` |
| **Refresh Pull Request** | <shortcut>F5</shortcut> | `AzureDevOps.PullRequest.Details.Reload` |
| **View Pull Request** | <shortcut>↵ Enter</shortcut> / double-click *(in the list)* | `AzureDevOps.PullRequest.Show` |
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

> Double **Shift** (<shortcut>⇧⇧</shortcut>) opens the IDE's *Search Everywhere*, where Azure DevOps PRs appear in their own **Pull Requests** tab — the same tab **Go to Pull Requests…** opens by default. See [Pull Requests](Pull-Requests.md#jump-to-a-specific-pr).
> {style="tip"}

## AI actions

| Action | Shortcut | Action ID |
|--------|----------|-----------|
| **Summarize Pull Request** | *no default* | `AzureDevOps.PullRequest.AI.Summarize` |
| **Run AI Review** | *no default* | `AzureDevOps.PullRequest.AI.Review` |
| **Explain This File** | *no default* | `AzureDevOps.PullRequest.AI.Explain` |
| **Generate Commit Message with AI** | *no default* | `AzureDevOps.AI.GenerateCommitMessage` |

These need an AI provider configured — see [AI Features](AI-Features.md).

## How to rebind {id="rebind"}

Only the **IDE actions** above (the ones with an Action ID) can be rebound — the composer keys are fixed.

<procedure title="Bind a shortcut">
    <step>Open <ui-path>Settings | Keymap</ui-path>.</step>
    <step>Type <code>AzureDevOps</code> in the search box to filter to the plugin's actions (it matches action IDs as well as display names).</step>
    <step>Double-click an action → <b>Add Keyboard Shortcut</b>.</step>
    <step>Press the combination. If it collides, IntelliJ warns you and offers to remove the conflict.</step>
    <step>Click <b>OK</b>.</step>
</procedure>

> Use the **action ID** column when filing a bug — it identifies the exact action across IDE versions where display names sometimes differ.
> {style="tip"}
