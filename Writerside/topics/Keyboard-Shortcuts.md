# Keyboard Shortcuts

Every shortcut the plugin uses, in one place. There are two kinds:

- **IDE actions** - registered with the IDE, shown in their menus, and **rebindable** in <ui-path>Settings | Keymap</ui-path>. Each has an **Action ID** (most match `AzureDevOps`; the tool-window ones match their window name).
- **In-view keys** - built into a specific view (the comment composer, the PR timeline, the Pipelines run editor) and active only while that view is focused. They aren't in Keymap and can't be rebound.

> On macOS, <shortcut>⌘</shortcut> is Command and <shortcut>⌃</shortcut> is **Control** - most actions use ⌘, but a few use ⌃. Windows / Linux use <shortcut>Ctrl</shortcut>.
> {style="note"}

## Tool windows

Open (or focus) a plugin tool window from anywhere. These are the IDE's standard **Activate tool window** actions, so they're rebindable in <ui-path>Settings | Keymap</ui-path> (search the window name).

| Action | macOS | Windows / Linux | Action ID |
|--------|-------|------------------|-----------|
| **Pull Requests** tool window | <shortcut>⌘⇧Y</shortcut> | <shortcut>Ctrl+Shift+Y</shortcut> | `ActivatePullRequestsWindowToolWindow` |
| **Pipelines** tool window | <shortcut>⌘⇧W</shortcut> | *first free - see tooltip* | `ActivatePipelinesWindowToolWindow` |

> The **Pipelines** shortcut only does anything when the Pipelines integration is on (<ui-path>Settings | Version Control | Azure DevOps</ui-path> → **Enable Pipelines integration**) - without it there's no tool window to open.
> {style="note"}

> On **macOS** the default is <shortcut>⌘⇧W</shortcut> - one of the few ⌘⇧ combos free on both 2025.2 and 2026.1 (modern IntelliJ claims most of them: ⌘⇧J is the Database console, ⌘⇧O is Go to File, ⌘⇧K is Push, …). On **Windows / Linux** the plugin picks the first free combo instead, so it can differ - **hover the Pipelines stripe icon to see the actual key**. Already use the default for something else? Rebind Pipelines in <ui-path>Settings | Keymap</ui-path> (search **Pipelines**). The shortcut is seeded at IDE startup, so after installing/updating the plugin you must **fully restart the IDE** (a plugin reload-in-place won't seed it) - and a rebind likewise shows on the icon only after a restart.
> {style="tip"}

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

> The Pull Requests tool window has no Reload button - refresh is keyboard-only (or right-click → **Refresh List**).
> {style="note"}

## In the PR timeline

These keys drive the **View Timeline** editor and fire while it's focused. Like the composer keys they're built in (not in Keymap). Press <shortcut>?</shortcut> any time for the same list.

| Action | Shortcut |
|--------|----------|
| **Next unresolved thread** | <shortcut>F8</shortcut> / <shortcut>J</shortcut> |
| **Previous unresolved thread** | <shortcut>⇧F8</shortcut> / <shortcut>K</shortcut> |
| **Resolve / reopen** the focused thread | <shortcut>R</shortcut> |
| **Reply** to the focused thread | <shortcut>A</shortcut> |
| **Start a new comment** | <shortcut>C</shortcut> |
| **Collapse / show resolved** threads | <shortcut>H</shortcut> |
| **View AI review comments** | <shortcut>I</shortcut> |
| **Find in timeline** | <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> |
| **Show this list** | <shortcut>?</shortcut> |

> **View AI review comments** (<shortcut>I</shortcut>) jumps into the diff at the first AI suggestion - AI review comments render as diff inlays, and the inlay's own arrows step through the rest. It needs an AI review to have run first. See [AI Features](AI-Features.md).
> {style="tip"}

## In the Pipelines run editor

The run overview (opened from the **Pipelines** tool window) has its own keys, shown any time with <shortcut>?</shortcut> or the **?** button on the stage-graph toolbar. Built in, not in Keymap. Needs the Pipelines integration enabled.

| Action | Shortcut |
|--------|----------|
| **View logs / back** to the stage graph | <shortcut>L</shortcut> |
| **Previous / next tab** | <shortcut>[</shortcut> / <shortcut>]</shortcut> |
| **Zoom in / out / fit** the stage graph | <shortcut>=</shortcut> / <shortcut>-</shortcut> / <shortcut>0</shortcut> |
| **Open this run in the browser** | <shortcut>B</shortcut> |
| **Filter tests** (Tests tab) | <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> |
| **Show this list** | <shortcut>?</shortcut> |

> Inside a job's **logs**, <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> opens the log search bar instead (find across all steps).
> {style="note"}

## Branch widget / VCS menu

| Action | Shortcut | Action ID |
|--------|----------|-----------|
| **Open Current Branch PR** | *no default* | `AzureDevOps.OpenCurrentBranchPr` |
| **Update Pull Request Branch** | *no default* | `AzureDevOps.Pull.Request.Branch.Update` |
| **Review in Editor** | *no default* | `AzureDevOps.Pull.Request.Review.In.Editor.Toggle` |
| **Go to Pull Requests…** | <shortcut>⌘⇧P</shortcut> / <shortcut>Ctrl+Shift+P</shortcut> | `AzureDevOps.PullRequest.GoTo` |

> Double **Shift** (<shortcut>⇧⇧</shortcut>) opens the IDE's *Search Everywhere*, where Azure DevOps PRs appear in their own **Pull Requests** tab - the same tab **Go to Pull Requests…** opens by default. See [Pull Requests](Pull-Requests.md#jump-to-a-specific-pr).
> {style="tip"}

## AI actions

| Action | Shortcut | Action ID |
|--------|----------|-----------|
| **Summarize Pull Request** | *no default* | `AzureDevOps.PullRequest.AI.Summarize` |
| **Run AI Review** | *no default* | `AzureDevOps.PullRequest.AI.Review` |
| **Explain This File** | *no default* | `AzureDevOps.PullRequest.AI.Explain` |
| **Generate Commit Message with AI** | *no default* | `AzureDevOps.AI.GenerateCommitMessage` |

These need an AI provider configured - see [AI Features](AI-Features.md).

## How to rebind {id="rebind"}

Only the **IDE actions** above (the ones with an Action ID) can be rebound - the **in-view keys** (the comment composer, the PR timeline, and the Pipelines run editor) are fixed.

<procedure title="Bind a shortcut">
    <step>Open <ui-path>Settings | Keymap</ui-path>.</step>
    <step>Type <code>AzureDevOps</code> in the search box to filter to the plugin's actions (it matches action IDs as well as display names).</step>
    <step>Double-click an action → <b>Add Keyboard Shortcut</b>.</step>
    <step>Press the combination. If it collides, IntelliJ warns you and offers to remove the conflict.</step>
    <step>Click <b>OK</b>.</step>
</procedure>

> The two **tool-window** shortcuts are IDE actions too, but their IDs (`ActivatePullRequestsWindowToolWindow` / `ActivatePipelinesWindowToolWindow`) don't contain `AzureDevOps` - search **Pull Requests** or **Pipelines** to find and rebind them.
> {style="note"}

> Use the **action ID** column when filing a bug - it identifies the exact action across IDE versions where display names sometimes differ.
> {style="tip"}
