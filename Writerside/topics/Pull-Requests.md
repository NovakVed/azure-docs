# Pull Requests

The **Pull Requests** tool window is your command center: browse the queue, filter and search, open a PR, and act on it - complete, revert, compare, and more.

## Open the tool window

The tool window appears in the left sidebar whenever the open project has at least one Azure DevOps Git remote. (No Azure DevOps remote? It stays hidden to reduce clutter.)

- Click the **Pull Requests** stripe icon in the sidebar.
- Or use <ui-path>View | Tool Windows | Pull Requests</ui-path>.
- Or run *Find Action* (<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>) and type **Pull Requests**.

![The Pull Requests tool window with the search field, filter chips, and a populated list](pr-tool-window.png){ width="720" border-effect="line" }

## Find pull requests

### The default view: yours

With no filters active, the list shows exactly what the Azure DevOps web **Mine** tab shows - active PRs you **created**, **assigned to you**, or **assigned to one of your teams**. It's the view you land on, and the view *Clear filters* returns you to.

Pick any chip, preset, or search and the list switches to the full set; clear them and you're back to yours.

> Team-assigned PRs need the right [permissions](Permissions.md). If your credentials can't read team memberships, the plugin tells you once - the rest of the view keeps working.
> {style="note"}

### Quick Filters

Click the **filter icon** on the left of the chip row for one-click presets. A badge on the icon shows how many filters are active.

![The Quick Filters menu with its presets](quick-filters-menu.png){ width="380" border-effect="line" }

| Preset | Shows |
|--------|-------|
| **All pull requests** | Everything - the escape from the default "yours" view |
| **Open pull requests** | All active PRs |
| **Awaiting my review** | PRs where you're a reviewer who hasn't voted |
| **Involving me** | PRs you authored, review, or were mentioned in |
| **Clear N filter(s)** | Resets every active filter - back to the default "yours" view |

### Filter chips

A scrollable row of chips sits below the search field. Click any chip to refine the list:

| Chip | Options |
|------|---------|
| **State** | Active · Completed · Abandoned |
| **Author** | Type-ahead search across users |
| **Tags** | Azure DevOps PR labels (tags) |
| **Assignee** | Type-ahead search across users |
| **Review** | Approved · Approved with suggestions · Waiting for author · Rejected · Awaiting my review |
| **Work Items** | Linked Azure Boards work items |
| **Draft** | Drafts only · Non-drafts only |
| **Sort** | Newest · Oldest · Most/Least commented · Recently/Least recently updated |

Filters persist **per project** across IDE restarts. To clear them, use the Quick Filters menu's **Clear N filter(s)**.

> **Search** - type in the field above the chips to match PR titles, numbers, authors, and branch names. Press <shortcut>⇧ Shift</shortcut> twice to open *Search Everywhere*, where Azure DevOps PRs also appear - selecting one opens it directly.
> {style="tip"}

### Jump to a specific PR

When you already know which PR you want, skip the list. **Go to Pull Requests…** fuzzy-searches every cached PR - by **id, title, author, or repo** - and opens it straight on its timeline. An empty search lists every cached PR (unread first, then newest).

- Press <shortcut>⌘⇧P</shortcut> / <shortcut>Ctrl+Shift+P</shortcut>.
- Or use <ui-path>VCS | Go to Pull Requests…</ui-path>.
- Or run *Find Action* (<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>) and type **Go to Pull Requests**.

By default it opens a **Pull Requests** tab in the IDE's *Search Everywhere* popup, next to Files, Symbols, and Actions; press <shortcut>↵ Enter</shortcut> to open the highlighted PR.

![The Go to Pull Requests results: the Pull Requests tab in Search Everywhere](go-to-pr-popup.png){ width="560" border-effect="line" }

> Prefer a dedicated dialog? Turn **off** **Show in the Search Everywhere window** in [Settings](Settings.md) and the action opens its own quick-pick popup instead - a search field with a status **funnel** beside it, and <shortcut>↵</shortcut> Open / <shortcut>⎋</shortcut> Close keys.
> {style="tip"}

## Read a PR row

Each row packs the status at a glance:

![The anatomy of a pull-request row](pr-row-anatomy.png){ width="640" border-effect="line" }

- **Title and `!`-number**, with a **status pill** when relevant: *Draft*, *Merged*, *Abandoned*, or *Has merge conflicts*.
- **Reviewer vote icons** - approved, approved-with-suggestions, waiting, or rejected.
- **An amber discussion badge** with the thread count (and how many are still unresolved).
- **Attention chips** - *Review requested*, *Mentions you*, or *Replied* - when a PR wants your attention. These are off by default; see [Notifications &amp; Attention](Notifications-and-Attention.md) to turn them on.

Unread PRs can show a blue **unread marker** dot that reacts to new commits *and* new comment activity. Toggle it from the tool-window gear → **Show unread markers**.

## Open and act on a PR

**Click** a PR to open its single-pane detail view in an editor tab. The action bar at the bottom adapts to your role:

| You are… | Primary actions |
|----------|-----------------|
| **Reviewer** | **Approve ▾** (split button: Approve with suggestions, Wait for author, Reject, Reset feedback) |
| **Author, needs review** | **Request review** |
| **Author, reviews in** | **Complete ▾** (Set auto-complete…, Mark as draft, Abandon) |
| **Not involved** | **Set myself as reviewer** |

Every state also shows a **⋮** (More) menu with the full action set:

![The PR action bar overflow menu](pr-overflow-menu.png){ width="440" border-effect="line" }

| Action | What it does |
|--------|--------------|
| **Share Pull Request…** | Email the PR to people (no reviewers added, no comment posted) |
| **Submit Pending Comments (N)** | Post the comments you've queued as a review (only when N > 0) |
| **Restart Merge** | Re-queue a stuck merge (conflicts / failed / policy-rejected) |
| **Change Target Branch…** | Re-point the PR at a different target branch |
| **Cherry-Pick…** | Create a branch with this PR's commits cherry-picked onto another branch |
| **Review Changes Since…** | Re-scope the diff to what changed since a chosen update - see [Code Review](Code-Review.md#compare) |
| **Revert…** | *(merged PRs)* Create a branch that reverts this PR's changes |
| **Open on Web** · **Copy Link** | Jump to / copy the dev.azure.com URL |
| **Summarize Pull Request** · **Run AI Review** | [AI assists](AI-Features.md) |

### Complete a pull request

Click **Complete** to open the **Complete Pull Request** dialog. Pick a **Merge type** - the live diagram shows the resulting history shape:

![The Complete Pull Request dialog with the merge-strategy diagram](complete-pr-dialog.png){ width="560" border-effect="line" }

- **Merge (no fast forward)** · **Squash commit** · **Rebase and fast-forward** · **Semi-linear merge**
- **Post-completion options:** complete associated work items, delete the source branch, and optionally customize the merge commit message.

> **Branch policies are honored.** If required reviewers or status checks aren't satisfied, the dialog lists the blockers. Only if you hold the bypass permission do you get **Override branch policies and enable merge** (with a required reason).
> {style="warning"}

Right-click any row for quick actions too: **View Pull Request**, **View Pull Request in Browser**, **Copy Pull Request URL**, and **Refresh List**.

## Create a pull request

Click **+** (Create Pull Request) in the tool-window toolbar. The form pre-fills the source branch (your current branch) and the default target branch.

![The Create Pull Request form: the Write/Preview description composer and the reviewers, tags, and work-item rows](create-pr-ai.png){ width="640" border-effect="line" }

The **description** uses the same composer as PR comments: a **Write | Preview** tab strip, with the formatting toolbar above the editor. Type `@`, `#`, or `!` for inline autocomplete of people, work items, and PRs. Press <shortcut>⌘↵</shortcut> / <shortcut>Ctrl+Enter</shortcut> to create.

The metadata block below the description is four inline rows - each with a pencil to edit, and where shown an **X** to clear:

| Row | What you set |
|-----|--------------|
| **Required reviewers** | People who must review |
| **Optional reviewers** | People invited to review |
| **Tags** | Azure DevOps PR labels - pick existing ones, or use the **+** to create a brand-new tag |
| **Work items** | Linked Azure Boards work items |

The primary button is a split button: **Create Pull Request**, with **Create Draft Pull Request** on its dropdown.

> With [AI enabled](AI-Features.md), the description composer toolbar gains an AI button (tooltip **Generate title &amp; description with AI**) that drafts the title and description from your branch's commits. If no AI provider is set up yet, clicking it offers to open AI Settings.
> {style="tip"}

## Refresh and background sync

Azure DevOps has no webhooks, so the plugin polls. The list updates on its own, but you can refresh on demand:

- Press <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> or <shortcut>F5</shortcut> while the tool window is focused.
- Or right-click a row → **Refresh List**.

> The polling cadence is the **Sync interval** in [Settings](Settings.md) (default 60 s). On cold start the list shows its **last-known cached state** while the first sync runs, so you can act immediately instead of waiting on a spinner.
> {style="note"}

## Switch account or repository

For projects bound to multiple orgs or repos, use the tool-window gear → **Switch Account / Repository…**. The current branch's PR is also shown in the Git branch widget and the status bar - see [Git Integration](Git-Integration.md).
