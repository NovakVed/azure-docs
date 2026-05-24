# Keyboard Shortcuts

Every action the plugin contributes to the IDE, grouped by surface. To rebind any of them, see [How to rebind](#rebind) at the bottom.

## In the editor (review-in-editor)

| Action                  | macOS                              | Windows / Linux                          | Action ID                                                   |
|-------------------------|------------------------------------|------------------------------------------|-------------------------------------------------------------|
| **Add Review Comment**  | <shortcut>⌘⇧M</shortcut>           | <shortcut>Ctrl+Shift+M</shortcut>        | `AzureDevOps.PullRequest.AddCommentAtCursor`                |

Only fires when the caret is on a changed line of a file that's part of an open PR. See [Review in Editor](Review-in-Editor.md).

## In the diff viewer

| Action                       | macOS                              | Windows / Linux                          | Action ID                                                   |
|------------------------------|------------------------------------|------------------------------------------|-------------------------------------------------------------|
| **Mark File as Viewed**      | <shortcut>⌘⇧S</shortcut>           | <shortcut>Ctrl+Shift+S</shortcut>        | `AzureDevOps.PullRequest.MarkFileAsViewed`                  |
| **Add Review Comment**       | <shortcut>⌘⇧M</shortcut>           | <shortcut>Ctrl+Shift+M</shortcut>        | `AzureDevOps.PullRequest.AddCommentAtCursor`                |
| Next changed range           | <shortcut>F7</shortcut>            | <shortcut>F7</shortcut>                  | *built-in IntelliJ diff*                                    |
| Previous changed range       | <shortcut>⇧F7</shortcut>           | <shortcut>Shift+F7</shortcut>            | *built-in IntelliJ diff*                                    |

## In the PR list / timeline / detail view

| Action                       | Shortcut                  | Action ID                                                   |
|------------------------------|---------------------------|-------------------------------------------------------------|
| **Refresh** (list)           | <shortcut>F5</shortcut>   | `AzureDevOps.PullRequest.List.Reload`                       |
| **Refresh** (timeline)       | <shortcut>F5</shortcut>   | `AzureDevOps.PullRequest.Timeline.Update`                   |
| **Refresh** (detail)         | <shortcut>F5</shortcut>   | `AzureDevOps.PullRequest.Details.Reload`                    |
| Open PR in browser           | *no default*              | `AzureDevOps.PullRequest.Open.Link`                         |
| Copy PR URL                  | *no default*              | `AzureDevOps.PullRequest.Copy.Link`                         |
| Show PR in tool window       | *no default*              | `AzureDevOps.Pull.Request.Show.In.Toolwindow`               |
| Show PR (open detail)        | *no default*              | `AzureDevOps.PullRequest.Show`                              |

## Branch popup / VCS menu

| Action                       | Shortcut                  | Action ID                                                   |
|------------------------------|---------------------------|-------------------------------------------------------------|
| **Open Current Branch PR**   | *no default*              | `AzureDevOps.OpenCurrentBranchPr`                           |
| Update PR Branch             | *no default*              | `AzureDevOps.Pull.Request.Branch.Update`                    |
| Toggle Review in Editor      | *no default*              | `AzureDevOps.Pull.Request.Review.In.Editor.Toggle`          |

## AI actions

| Action                       | Shortcut                  | Action ID                                                   |
|------------------------------|---------------------------|-------------------------------------------------------------|
| Generate PR Summary          | *no default*              | `AzureDevOps.PullRequest.AI.Summarize`                      |
| Run AI Review                | *no default*              | `AzureDevOps.PullRequest.AI.Review`                         |
| Explain Selection / File     | *no default*              | `AzureDevOps.PullRequest.AI.Explain`                        |
| Generate Commit Message      | *no default*              | `AzureDevOps.AI.GenerateCommitMessage`                      |

These all need an AI provider configured — see [AI Features](AI-Features.md).

## How to rebind {id="rebind"}

<procedure title="Bind a shortcut">
    <step>Open <ui-path>Settings | Keymap</ui-path>.</step>
    <step>In the search box, type <code>AzureDevOps</code> to filter down to the plugin's actions.</step>
    <step>Double-click an action and choose <b>Add Keyboard Shortcut</b>.</step>
    <step>Press the key combination you want. If it collides with an existing binding, IntelliJ warns you and offers to remove the conflict.</step>
    <step>Click <b>OK</b>.</step>
</procedure>

You can search by the **action ID** (e.g. `AzureDevOps.PullRequest.AI.Review`) too — IntelliJ matches against IDs as well as display names.

> Use the <b>action ID</b> column above when filing a bug — it identifies the exact action across IDE versions where display names sometimes differ.
> {style="tip"}
