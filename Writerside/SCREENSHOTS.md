# Screenshot capture guide

This is the shot list for the documentation site. Every image referenced from a
topic already has a **labelled placeholder PNG** in [`images/`](images/) so the
site builds green. To add a real screenshot, **capture it and overwrite the
placeholder with the same filename** - no topic edits needed, the image just
appears.

## How to capture (keep them consistent)

- **Theme:** IntelliJ **New UI, Dark** (matches the placeholders and the doc site).
- **Crop tight:** capture just the relevant panel/dialog, not the whole screen.
  On macOS use <kbd>⌘⇧4</kbd> then <kbd>Space</kbd> to grab a single window, or
  drag to select a region.
- **Scale:** capture on a HiDPI/Retina display if you can - the images render up
  to the widths below, so 2× pixels stay crisp.
- **Data hygiene:** use a demo org/repo or scrub anything sensitive. Avoid real
  tokens, private repo names, or personal email addresses in frame.
- **Format:** PNG, same filename as the placeholder.

After dropping files in, run a build (push to `main`, or preview with the
Writerside plugin) to see them live. Delete this file before publishing if you
prefer it not to ship - it lives outside `topics/` so it is **not** part of the
built site either way.

## Must-have first (8)

These carry the most weight - the hero, the two most-misunderstood screens
(single-pane detail, real sign-in), and the headline features.

| File | Used on | Capture |
|------|---------|---------|
| `pr-tool-window.png` | Welcome (hero), Pull Requests, Quick Start | The **Pull Requests** tool window with a populated list: the search field, the full filter-chip row (State, Author, Tags, Assignee, Review, Work Items, Draft, Sort) and the Quick Filters icon on the left, and several PR rows showing status pills, reviewer vote icons, and the amber comment badge. Turn on **Show attention markers** first so a chip is visible. |
| `pr-detail.png` | Quick Start, Pull Requests, Code Review | An open PR in the **single-pane detail view**: title with `!N`, the **View Timeline** link, base→head branches, the status-checks panel with per-reviewer votes, the changes tree, and the action bar with the **Approve** split-button. (No sub-tabs - that's the point.) |
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
| `diff-comment.png` | Code Review | The diff viewer with the **+** gutter affordance and a new-comment inlay open: the **Write / Preview** tabs + top toolbar, and the **Start Review** split submit button (dropdown: Add Single Comment, Suggest change). |
| `mark-file-viewed.png` | Code Review | The changes-tree right-click menu showing **Mark File as Viewed**, next to the tree with some files dimmed as viewed. |
| `comment-toolbar.png` | Discussions & Comments | A comment composer showing the **Write / Preview** tab strip at top-left, the formatting toolbar along the same top strip (with **Polish grammar & spelling with AI** pinned far-right), and the muted **Add files** link on the bottom row beside the submit buttons. |
| `suggestion-block.png` | Discussions & Comments | A **Suggested change** card on a thread with the **Apply Locally** / **Commit…** buttons. |
| `ai-settings.png` | AI Features, Settings | The **AI Settings** page: the **Enable AI assistance** toggle, the **AI Providers** table, and the **Per-Feature Provider** rows. |
| `create-pr-ai.png` | Pull Requests, AI Features | The Create-PR form: source/target pre-filled, the **Write / Preview** description composer with the AI bulb button in its toolbar, and the Required/Optional reviewers, Tags, and Work items metadata rows. |
| `attention-row-chips.png` | Notifications & Attention | PR rows showing the coloured attention chips: **Review requested**, **Mentions you**, **Replied**. |
| `attention-balloon.png` | Notifications & Attention | A lower-right notification balloon for a PR that needs you, with **Open pull request** / **Mark as read**. |
| `branch-widget-popup.png` | Git Integration, Review in Editor | The main-toolbar Git branch widget popup with the Azure DevOps section: Show in Tool Window, Update Pull Request Branch, Review in Editor. |
| `marketplace-install.png` | Installation | Settings ▸ Plugins ▸ Marketplace with "Azure DevOps Pull Requests" searched and the **Install** button visible. |
| `go-to-pr-popup.png` | Pull Requests | **Go to Pull Requests…** (⌘⇧P): the **Pull Requests** tab in *Search Everywhere* with a few results - or, with **Show in the Search Everywhere window** turned off, the standalone quick-pick popup (search field, status funnel, ↵ Open / ⎋ Close footer). |
| `ai-summary-settings-popup.png` | AI Features | The **Summary settings** popup off the AI summary card's gear: the *Generate automatically on open* checkbox, the **Verbosity** and **Formality tone** sliders, and the **Personality** / **Customization prompt** fields. |

## Pipelines - must-have (4)

The headline surfaces of the Pipelines integration: the tool window, the run
overview with its interactive stage graph, the streaming job logs, and the
Tests donut. Capture these against the seeded on-prem mock (the disconnected
"Monorepo CI" run 4993 is the only surface that shows a real DAG - real Azure
runs omit `dependsOn`).

| File | Used on | Capture |
|------|---------|---------|
| `pipelines-tool-window.png` | Welcome, Pipelines (hero) | The **Pipelines** tool window docked on the left, on the **Pipelines** list tab with the **Recent** scope selected. Show the PR-style search bar - the search field, the **View** chip (reading "Recent"), the **Status** chip, and the **Quick filters** funnel icon - above a populated list of pipeline **definitions**: each row a status icon + bold pipeline name + muted `folder · last run <relative>` subtitle, with a mix of Succeeded, Failed, and Partially-succeeded icons. Include the top-right **Run Pipeline…** and **Refresh** title actions. Have at least one open `#<n>` run-detail tab visible in the tab strip to show the tabbed UI. |
| `pipeline-run-overview.png` | Pipelines, Welcome | The **Pipeline Run** editor (main tab, title e.g. `#20260101.1`) on the **Summary** tab. Frame the header: run status icon + `<pipeline name>  <run#>` (H2) and the muted `status • branch • requestedFor • duration` meta line, with the **Re-run** button and **Open in Browser** link at right. Below, the **Stages** heading with its zoom toolbar (**Zoom out / Zoom in / Fit to view / Keyboard shortcuts**) and the interactive **stage graph** showing several connected Stage cards with status icons and `N jobs · duration` subtitles. Use the mock **Monorepo CI** run so multiple stages and edges are visible. Make sure the adaptive **Tests** tab appears in the tab strip (Summary \| Tests \| Extensions \| Environments \| Code coverage). |
| `pipeline-job-logs.png` | Pipelines | The **Pipeline Run** editor showing a job's **step logs** (`PipelineJobStepsView`). Frame the slim job-header bar - the **← Summary** back-link, then the job status icon + name + muted `Succeeded · 56s`-style meta - above the GitHub-Actions-style collapsible step sections: chevron + status icon + step name + duration per header, with one step (ideally the **failed** step, auto-expanded) opened to reveal the numbered, colour-coded log. Pick a run/job where a `##[error]` line is red and a `##[section]` header is bold so the syntax colouring is visible. |
| `pipeline-tests-tab.png` | Pipelines | The **Pipeline Run** editor on the **Tests** tab (only present when the run reported tests - use a mock run with `totalTests > 0`). Frame the **donut** (green Passed / red Failed / grey Others) with its **Passed / Failed / Others** legend, flanked by the **Total tests**, **Pass percentage**, **Run duration**, and **Tests not reported** stat blocks. Below, the **Test results** card with the **Filter by test or run name** search box, the facet chips (**Test file**, **Owner**, and the **Outcome: All** chip), and the results table (**Test**, **Owner**, **Duration**, **Outcome** columns) with a few Failed rows visible (default filter = Failed + Aborted). |

## Pipelines - nice-to-have (round out coverage)

| File | Used on | Capture |
|------|---------|---------|
| `pipeline-stage-graph.png` | Pipelines | A tight crop of just the interactive **stage graph** on the Summary tab, with one stage **focused** (hovered or clicked) so its flow lights up: upstream **Depends on** edges in blue, downstream **Runs after** edges in green, others dimmed, connection bullets at the edge ends. Include the two screen-space overlays - the bottom-right **legend** ("Depends on / Runs after · hover a stage to trace its flow · others dimmed") and the top-right **focused-stage caption card** (stage title, status·duration, "Depends on: …", "Followed by: …"). Use the **Monorepo CI** mock run (the only DAG surface). Expand one card via its chevron so the per-job list and **Rerun stage** button show. |
| `pipeline-approval-gate.png` | Pipelines | The **Pipeline Run** editor header with an **approval gate** callout band directly beneath it (red Validator-error tint chrome). Show the header row **Approval needed — <Stage>** with the waiting-for-author vote icon and the **N of M approved · in sequence · waiting since <time>** meta, the check's instructions, one or two per-approver rows (avatar + name + Pending/Approved state), and the action row: the **Add an optional comment…** field with the right-aligned **Reject** and **Approve** buttons. Requires a mock run with a pending `Checkpoint.Approval` gate. |
| `pipeline-run-dialog.png` | Pipelines | The **Run Pipeline** dialog. Frame the **Pipeline** and **Branch** native combo pickers (Pipeline showing name + muted folder subtitle), the **Parameters** section rendered as a typed form (a `values:` dropdown chip, a boolean checkbox, and a text field, with required params marked `*`), the **Variables** section, the two checkboxes (**Enable system diagnostics**, **Preview only (render final YAML, don't queue)**), and the **Run** button. Use a mock YAML pipeline that declares runtime parameters so the form is populated rather than a fallback message. |
| `pipeline-notification.png` | Pipelines, Notifications & Attention | A lower-right IDE notification balloon from the **Azure DevOps Pipelines** group for a run of yours reaching a terminal state: title `<pipeline> <run#> failed` (use a failed run for the red ERROR styling), body `on <branch>`, and the **Open run** action link. Trigger it with a mock run whose `requestedFor` matches the signed-in user. Optionally show the **Pipelines** stripe icon carrying its severity dot (red) in the same frame. |
