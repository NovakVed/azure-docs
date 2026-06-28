# Review in Editor

Read and comment on a PR's changes inside your regular code editor — no diff viewer required. When the branch you have checked out matches a PR's source branch, the editor itself becomes the review surface.

## When it activates

Review-in-editor turns on automatically when **both** are true:

- Your project has an Azure DevOps remote.
- Your checked-out branch matches the **source branch** of an open PR.

The **Git branch widget in the main toolbar** then shows the PR — e.g. `!1234 on feature/login` — and the editor gains the review affordances below.

![A PR under review directly in the editor](review-in-editor.png){ width="720" border-effect="line" }

## What you see in the editor

Every file with changes in the PR gets:

- **A blue line in the gutter** marking each changed range.
- **A `+` on hover** in the gutter — click to comment on that line, or drag across line numbers for a multi-line range.
- **A subtle highlight** on lines that already have a thread, with the **thread inlays** anchored there. Click a thread header to expand or collapse it.
- **A `Review:` toolbar** above the editor with **Prev Comment** / **Next Comment** to jump between threads in the file.

Threads anchor to the **PR's** line numbers. If you edit the file locally, the plugin tracks the change and keeps each thread on the right line.

## Comment and review

<procedure title="Add a comment from the editor">
    <step>Click the <b>+</b> in the gutter (or press <shortcut>⌃⇧M</shortcut> / <shortcut>Ctrl+Shift+M</shortcut> at the caret).</step>
    <step>Type your comment — full markdown, with the same toolbar, @mentions, suggestions, and image paste as everywhere else.</step>
    <step>Post it immediately, queue it as part of a pending review, or wrap it as a suggested change.</step>
</procedure>

Comments posted from the editor and from the diff viewer are the same comments — both surfaces show the full thread. To finish a review and vote, use the **Submit (N)** button (it carries the count of any queued comments). You can also **Mark File as Viewed** (<shortcut>⌘⇧S</shortcut> / <shortcut>Ctrl+Shift+S</shortcut>) here, and viewed files dim in the changes tree.

## Toggle it on or off

The toggle lives in the **main-toolbar Git branch widget** popup, alongside two related actions:

![The branch widget popup with the Review in Editor toggle](branch-widget-popup.png){ width="440" border-effect="line" }

- **Show in Tool Window** — open the PR's detail view.
- **Update Pull Request Branch** — appears when your local branch has diverged from the PR head.
- **Review in Editor** — turn the editor overlay off or back on without switching branches.

> Don't confuse the two widgets: the **main-toolbar** branch widget shows `!{id} on {branch}` and hosts these actions; a separate **status-bar** widget shows `ADO PR !{id}` and simply opens the PR when clicked. See [Git Integration](Git-Integration.md).
> {style="note"}

## Auto-off on branch divergence

If your local branch drifts from the PR's head — typically because you committed locally and haven't pushed — review-in-editor turns itself off, since it would otherwise anchor threads to stale lines. It re-enables as soon as you push or reset to the PR head.

## Editor vs diff viewer

Review-in-editor is **additive**, not a replacement. Open the PR's full diff anytime from the changes tree in the detail view. Use whichever fits the moment:

- **Editor** — best for reading code in context, with imports, highlighting, and your usual navigation.
- **Diff viewer** — best for side-by-side comparison and seeing every changed file at once.

Comments stay in sync between the two.
