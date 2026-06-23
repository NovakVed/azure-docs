# Code Review

Review pull requests with IntelliJ's native diff viewer: read the changes, leave inline comments and suggestions, vote, and track which files you've seen.

## The detail view

Opening a PR creates a closable editor tab — a **single pane**, no sub-tabs. From top to bottom: the title and `!`-number with a **View Timeline** link, the source → target branches, the status checks (CI, conflicts, required reviewers and their votes), the **changed-files tree**, and the action bar.

![A pull request open in the single-pane detail view](pr-detail.png){ width="720" border-effect="line" }

- **Changed files** live in the tree — click one to open the diff.
- **Discussion** opens in its own tab via the **View Timeline** link — see [Discussions &amp; Comments](Discussions-and-Comments.md).
- **Votes and actions** live in the action bar and its overflow menu — see [Pull Requests](Pull-Requests.md#open-and-act-on-a-pr).

## Read the diff

Clicking a file opens the diff in a single tab per PR — clicking another file swaps it in place, so <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> step through every changed range across the whole PR. The diff tab carries a **Review:** toolbar with **Refresh**, **Submit review**, and **Previous / Next Comment**.

| Navigate | macOS | Windows / Linux |
|----------|-------|------------------|
| Next / previous changed range | <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> | <shortcut>F7</shortcut> / <shortcut>Shift+F7</shortcut> |
| Next / previous comment | *Review: toolbar* | *Review: toolbar* |

### Show or hide threads

In the diff's gutter settings, the **Review Discussions** menu controls which inline threads render: **Show all discussions**, **Show only unresolved**, or **Don't show**.

## Comment on a line

<procedure title="Add an inline comment">
    <step>Hover the gutter of a changed line — a <b>+</b> appears. Click it (or drag across line numbers to span a range). You can also press <shortcut>⌘⇧M</shortcut> / <shortcut>Ctrl+Shift+M</shortcut> at the caret.</step>
    <step>Type your comment. The editor is full markdown with a formatting toolbar, @mentions, and image paste — see <a href="Discussions-and-Comments.md">Discussions &amp; Comments</a>.</step>
    <step>Post it one of three ways: <b>immediately</b> as a comment, <b>queued</b> as part of a pending review to submit together, or wrapped as a <b>suggested change</b> the author can apply in one click.</step>
</procedure>

![An inline comment open in the diff viewer](diff-comment.png){ width="720" border-effect="line" }

> **Pending review.** Comments you queue stay as drafts (counted on the **Submit (N)** button) until you submit them together with your vote — the same review flow GitHub users expect. Submit from the **Review:** toolbar or the overflow menu's **Submit Pending Comments**.
> {style="note"}

## Vote

The action bar's **Approve** button is a split button: its dropdown holds **Approve with suggestions**, **Wait for author**, **Reject**, and **Reset feedback**.

![The Approve split-button vote options](vote-approve-dropdown.png){ width="380" border-effect="line" }

Completing or abandoning a PR, including merge strategies, is covered in [Pull Requests](Pull-Requests.md#complete-a-pull-request).

## Track files as viewed

For large PRs, mark each file **viewed** as you go — viewed files dim in the changes tree.

- Press <shortcut>⌘⇧S</shortcut> / <shortcut>Ctrl+Shift+S</shortcut>, or right-click → **Mark File as Viewed**.
- Right-click with several files selected to **Mark All as Viewed**.

![Mark File as Viewed in the changes tree](mark-file-viewed.png){ width="560" border-effect="line" }

> Want files to mark themselves viewed as you open them? Turn on **Mark files as viewed when their diff is opened** in [Settings](Settings.md) (off by default, matching GitHub).
> {style="tip"}

## Review only what changed since an update {id="compare"}

When an author pushes new commits, you don't have to re-read the whole PR. From the overflow **⋮** menu, choose **Review Changes Since…**, pick an update, and the changes tree re-scopes to just that diff — target-branch commits merged in between are filtered out.

![The iteration-scope banner above the changes tree](compare-updates-banner.png){ width="700" border-effect="line" }

A banner — *"Reviewing only what changed since update N"* — sits above the tree; click **Show all changes** to return to the full PR. (The action appears once a PR has at least two updates.)

## Review in the editor instead

When the PR's source branch is checked out, you can comment on changed lines right in your normal editor — no diff tab needed. See [Review in Editor](Review-in-Editor.md).
