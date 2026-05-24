# Code Review

Review pull requests with IntelliJ's native diff viewer. Add inline comments, vote, mark files as viewed, and overlay review threads directly on your editor.

## Detail view layout

Opening a PR creates a closable editor tab with three sub-tabs:

| Tab            | Contents                                                                                                              |
|----------------|-----------------------------------------------------------------------------------------------------------------------|
| **Overview**   | Title, description, source/target branches, status checks, branch policies, reviewers, work items, vote summary.      |
| **Files**      | Full diff. Each file is rendered with IntelliJ's diff viewer.                                                         |
| **Discussion** | Chronological timeline of every comment thread, vote, and PR event.                                                   |

## Reading the diff

The **Files** tab shows a two-pane diff per file. The left pane is the target branch (base); the right pane is the source branch (head). Changed ranges are highlighted in green (added) and red (removed) with intra-line highlighting for character-level changes.

### Navigating between files

- Use the file tree on the left of the Files tab.
- Press <shortcut>F7</shortcut> / <shortcut>Shift+F7</shortcut> to step through changed ranges.
- Press <shortcut>⌥↓</shortcut> / <shortcut>⌥↑</shortcut> (macOS) or <shortcut>Alt+↓</shortcut> / <shortcut>Alt+↑</shortcut> (Windows/Linux) to jump between files.

## Inline comments

To leave a comment on a specific line:

<procedure title="Add an inline comment">
    <step>Hover over the gutter of the changed range — a <b>+</b> icon appears.</step>
    <step>Click it to open the comment editor inline beneath that line.</step>
    <step>Type your comment. Markdown is supported (see <a href="Discussions-and-Comments.md">Discussions</a> for the formatting toolbar).</step>
    <step>Click <b>Comment</b> to post.</step>
</procedure>

Existing comment threads appear as inline review-thread inlays anchored to their original line. Click a thread to expand it; click the chevron to collapse.

### Adding a comment at the caret

While the cursor is on a changed line, press <shortcut>⌘⇧M</shortcut> (macOS) / <shortcut>Ctrl+Shift+M</shortcut> (Windows/Linux) to open the comment editor without reaching for the mouse.

## Vote on a PR

From the Overview tab (or the toolbar of any detail tab) you can cast a review vote:

| Vote                          | Effect                                                                                            |
|-------------------------------|---------------------------------------------------------------------------------------------------|
| **Approve**                   | You're satisfied with the PR. Counts toward required reviewer approvals.                          |
| **Approve with suggestions**  | Approves, but flags non-blocking comments the author should consider.                             |
| **Wait for author**           | You've left blocking feedback. Doesn't count as approval until cleared.                           |
| **Reject**                    | The PR should not be merged in its current form.                                                  |
| **Reset vote**                | Removes your previous vote — useful if you voted in error.                                        |

## Complete or abandon

If you have permission to merge, the Overview tab shows:

- **Complete** — opens a dialog where you choose the merge strategy (no fast-forward, squash, rebase, semi-linear), update commit message, and optionally delete the source branch.
- **Abandon** — closes the PR without merging. Reversible from the Azure DevOps web UI.

> **Branch policies are honored**: if the target branch has required reviewers, required status checks, or other policies, you can't complete the PR until they're satisfied — the **Complete** button is disabled with a tooltip explaining why.
> {style="warning"}

## File-viewed tracking

For large PRs, mark each file as **viewed** as you go to keep track of progress:

- Open a file in the diff and press <shortcut>⌘⇧S</shortcut> (macOS) / <shortcut>Ctrl+Shift+S</shortcut> (Windows/Linux).
- Or click the **Viewed** toggle in the diff toolbar.

Viewed files are visually collapsed in the file tree. If the author force-pushes new commits, files you'd marked as viewed are automatically reset to unviewed.

## Review in the editor instead

When the PR's source branch is checked out locally, you can comment on changed lines directly in the regular code editor — no diff tab needed. See [Review in Editor](Review-in-Editor.md).

## Thread visibility

Use the diff toolbar's **Threads** menu to filter inline threads:

- **All threads**
- **Unresolved only** — default after the first read-through
- **Hidden** — collapses every thread

Use **Prev Comment** / **Next Comment** in the toolbar (or via *Find Action*) to skim only unresolved threads.

## Keyboard reference

| Action                       | macOS              | Windows / Linux            |
|------------------------------|--------------------|----------------------------|
| Add comment at caret         | <shortcut>⌘⇧M</shortcut>      | <shortcut>Ctrl+Shift+M</shortcut> |
| Mark file viewed/unviewed    | <shortcut>⌘⇧S</shortcut>      | <shortcut>Ctrl+Shift+S</shortcut> |
| Next changed range           | <shortcut>F7</shortcut>       | <shortcut>F7</shortcut>           |
| Previous changed range       | <shortcut>⇧F7</shortcut>      | <shortcut>Shift+F7</shortcut>     |
| Next file                    | <shortcut>⌥↓</shortcut>       | <shortcut>Alt+↓</shortcut>        |
