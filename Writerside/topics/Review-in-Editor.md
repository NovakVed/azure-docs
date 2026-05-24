# Review in Editor

Read and comment on a PR's changes inside the regular code editor — no diff viewer required. When the branch you have checked out matches a PR's source branch, the editor itself becomes the review surface.

## When it activates

Review-in-editor turns on automatically when **both** of these are true:

- Your project has an Azure DevOps remote.
- Your checked-out Git branch matches the **source branch** of an open PR.

The Git branch widget in the status bar shows the PR — e.g. `!1234 on feature/login` — and the editor gains the review affordances described below.

## What you see in the editor

While review-in-editor is on, every file that has changes in the PR gets:

- **A blue line in the gutter** marking each changed range — the same kind of marker IntelliJ uses for VCS changes, recolored to signal "this is part of a PR".
- **A `+` icon on hover** in the gutter — click it to add an inline comment at that line. The comment editor opens directly in the editor, with the same markdown toolbar used in the diff viewer.
- **Existing comment threads** anchored to their original line as inlay panels. Click a thread header to expand or collapse it.

Threads anchor to the **PR's** line numbers, not the file's current state. If you edit the file locally, the plugin tracks the change and keeps each thread on the right line.

## Adding a comment

<procedure title="Add a comment from the editor">
    <step>Place your cursor on a changed line.</step>
    <step>Click the <b>+</b> icon in the gutter, or press the <b>Add Review Comment</b> shortcut (defaults: <shortcut>⌘⇧M</shortcut> on macOS, <shortcut>Ctrl+Shift+M</shortcut> on Windows/Linux — see <a href="Keyboard-Shortcuts.md">Keyboard Shortcuts</a>).</step>
    <step>Type your comment. Markdown is supported.</step>
    <step>Click <b>Comment</b> to post.</step>
</procedure>

Comments posted from the editor and comments posted from the diff viewer are the same comments — both surfaces show the full thread.

## Auto-off on branch divergence

If your local branch drifts from the PR's head — typically because you committed locally and haven't pushed — review-in-editor turns itself off. It would otherwise anchor threads to stale line numbers.

You'll see review-in-editor re-enable as soon as the divergence is resolved (you push, or you reset to the PR head).

## Toggling manually

To turn review-in-editor off (or back on) without changing branches:

- Click the Git branch widget in the status bar.
- In the popup, toggle **Review in Editor**.

The toggle is also available as the `AzureDevOps.Pull.Request.Review.In.Editor.Toggle` action — find it in <ui-path>Help | Find Action</ui-path> or bind it to a shortcut in <ui-path>Settings | Keymap</ui-path>.

## Relationship to the diff viewer

Review-in-editor is **additive**, not a replacement. You can still open the PR's full diff at any time (<ui-path>tool window | PR detail | Files</ui-path>). Use whichever surface fits the moment:

- **Editor**: best for reading code in context, with imports, syntax highlighting, and your usual navigation shortcuts.
- **Diff viewer**: best for side-by-side comparisons, "viewed" tracking, and seeing the full set of changed files at once.

Comments stay in sync between the two views.

## Limitations

- Only works while the PR's source branch is checked out locally.
- Auto-disables on branch divergence to avoid stale anchors.
- Doesn't apply to files outside the PR — uninvolved files behave as normal IntelliJ editors.
