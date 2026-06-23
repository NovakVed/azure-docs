# Screenshot capture guide

This is the shot list for the documentation site. Every image referenced from a
topic already has a **labelled placeholder PNG** in [`images/`](images/) so the
site builds green. To add a real screenshot, **capture it and overwrite the
placeholder with the same filename** — no topic edits needed, the image just
appears.

## How to capture (keep them consistent)

- **Theme:** IntelliJ **New UI, Dark** (matches the placeholders and the doc site).
- **Crop tight:** capture just the relevant panel/dialog, not the whole screen.
  On macOS use <kbd>⌘⇧4</kbd> then <kbd>Space</kbd> to grab a single window, or
  drag to select a region.
- **Scale:** capture on a HiDPI/Retina display if you can — the images render up
  to the widths below, so 2× pixels stay crisp.
- **Data hygiene:** use a demo org/repo or scrub anything sensitive. Avoid real
  tokens, private repo names, or personal email addresses in frame.
- **Format:** PNG, same filename as the placeholder.

After dropping files in, run a build (push to `main`, or preview with the
Writerside plugin) to see them live. Delete this file before publishing if you
prefer it not to ship — it lives outside `topics/` so it is **not** part of the
built site either way.

## Must-have first (8)

These carry the most weight — the hero, the two most-misunderstood screens
(single-pane detail, real sign-in), and the headline features.

| File | Used on | Capture |
|------|---------|---------|
| `pr-tool-window.png` | Welcome (hero), Pull Requests, Quick Start | The **Pull Requests** tool window with a populated list: the search field, the full filter-chip row (State, Author, Tags, Assignee, Review, Work Items, Draft, Sort) and the Quick Filters icon on the left, and several PR rows showing status pills, reviewer vote icons, and the amber comment badge. Turn on **Show attention markers** first so a chip is visible. |
| `pr-detail.png` | Quick Start, Pull Requests, Code Review | An open PR in the **single-pane detail view**: title with `!N`, the **View Timeline** link, base→head branches, the status-checks panel with per-reviewer votes, the changes tree, and the action bar with the **Approve** split-button. (No sub-tabs — that's the point.) |
| `pat-login-dialog.png` | Authentication, Quick Start | The **Log In to Azure DevOps** dialog: the single **Server** field (e.g. `https://dev.azure.com/my-org`), the **Token** field, the required-scopes hint line, the **Generate…** button, and the "Learn how to generate…" link. |
| `oauth-scope-dialog.png` | Authentication, Quick Start | The **Sign in with Microsoft** permission picker with both radio options: **Full access (Recommended)** selected and **Standard access** below, and the **Continue** button. |
| `review-in-editor.png` | Review in Editor, Code Review, Git Integration | A source file checked out on a PR branch: the blue gutter line on a changed range, the **Review:** toolbar (Prev/Next Comment) above the editor, an expanded inline thread inlay, and the main-toolbar branch widget showing `!N on <branch>`. |
| `pr-overflow-menu.png` | Pull Requests, Code Review | The PR action bar with the **⋮** (More) menu open, showing Share Pull Request…, Submit Pending Comments, Restart Merge, Change Target Branch…, Cherry-Pick…, Review Changes Since…, Revert…, Open on Web, Copy Link, Summarize Pull Request, Run AI Review. |
| `ai-summary-card.png` | AI Features, Welcome | The collapsible **AI summary card** at the top of the PR timeline showing generated text, with the gear popup (Verbosity / tone) visible if possible. |
| `statistics-dashboard.png` | Statistics, Welcome | The **Pull Request Statistics** tab: the sticky header (Window selector + Author/Reviewer/Target-branch filters), the row of KPI tiles, and at least one chart section (e.g. Process health). |

## Nice-to-have (round out coverage)

| File | Used on | Capture |
|------|---------|---------|
| `quick-filters-menu.png` | Pull Requests | The **Quick Filters** popup: Open pull requests, Awaiting my review, Involving me, and "Clear N filter(s)". |
| `pr-row-anatomy.png` | Pull Requests | A tight crop of one or two PR rows: title with `!N`, status pill, reviewer vote icons, the amber unresolved/total comment badge, and an attention chip. |
| `vote-approve-dropdown.png` | Code Review, Quick Start | The **Approve** split-button dropdown open: Approve, Approve with suggestions, Wait for author, Reject, and Reset feedback. |
| `complete-pr-dialog.png` | Pull Requests | The **Complete Pull Request** dialog: the **Merge type** dropdown, the animated merge-strategy diagram, and the Post-completion options (Complete associated work items, Delete `<branch>`, Customize merge commit message). |
| `compare-updates-banner.png` | Code Review | The iteration-scope banner above the changes tree: "Reviewing only what changed since update N" with the **Show all changes** link. |
| `add-account-menu.png` | Authentication | Settings ▸ Version Control ▸ Azure DevOps with the **+** popup open showing **Log In with Token…** and **Log In via Microsoft…**. |
| `accounts-panel.png` | Authentication, Settings | The Azure DevOps accounts panel: a signed-in row with avatar, display name, organization URL, and the per-row pencil (edit) and ✕ (remove) icons. |
| `diff-comment.png` | Code Review | The diff viewer with the **+** gutter affordance and a new-comment inlay open (formatting toolbar + submit options). |
| `mark-file-viewed.png` | Code Review | The changes-tree right-click menu showing **Mark File as Viewed**, next to the tree with some files dimmed as viewed. |
| `comment-toolbar.png` | Discussions & Comments | A comment editor with the full formatting toolbar, including the **Polish grammar & spelling with AI** button and the suggestion button, with the @mention autocomplete open if possible. |
| `suggestion-block.png` | Discussions & Comments | A **Suggested change** card on a thread with the **Apply Locally** / **Commit…** buttons. |
| `ai-settings.png` | AI Features, Settings | The **AI Settings** page: the **Enable AI assistance** toggle, the **AI Providers** table, and the **Per-Feature Provider** rows. |
| `create-pr-ai.png` | Pull Requests, AI Features | The Create-PR form with source/target pre-filled and the AI **Generate** affordance on the title/description. |
| `attention-row-chips.png` | Notifications & Attention | PR rows showing the coloured attention chips: **Review requested**, **Mentions you**, **Replied**. |
| `attention-balloon.png` | Notifications & Attention | A lower-right notification balloon for a PR that needs you, with **Open pull request** / **Mark as read**. |
| `branch-widget-popup.png` | Git Integration, Review in Editor | The main-toolbar Git branch widget popup with the Azure DevOps section: Show in Tool Window, Update Pull Request Branch, Review in Editor. |
| `marketplace-install.png` | Installation | Settings ▸ Plugins ▸ Marketplace with "Azure DevOps Pull Requests" searched and the **Install** button visible. |
