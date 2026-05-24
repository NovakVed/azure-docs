# Pull Requests

The Pull Requests tool window is the entry point for everything: browse open PRs, search and filter, jump to a PR's detail view, or create a new one.

## Tool window

The tool window appears in the left sidebar of the IDE whenever the open project has at least one Azure DevOps Git remote. If your project has no Azure DevOps remote, the tool window is hidden to reduce clutter.

### Showing the tool window

- Click the **Pull Requests** icon on the left toolbar.
- Or use <ui-path>View | Tool Windows | Pull Requests</ui-path>.
- Or run *Find Action* (<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>) and type **Pull Requests**.

## Filtering the list

A row of filter chips sits above the PR list. Click any chip to refine the list:

| Filter           | What it does                                                                  |
|------------------|-------------------------------------------------------------------------------|
| **State**        | Open · Draft · Completed · Abandoned · All                                    |
| **Repository**   | Limit to one repo when the project has multiple Azure DevOps remotes          |
| **Author**       | Show only PRs created by selected users                                       |
| **Reviewer**     | Show only PRs where selected users are reviewers                              |
| **Label**        | Filter by Azure DevOps PR labels                                              |

Filters persist **per project** across IDE restarts — your filter state in one project doesn't carry over to another. Click the **×** on a chip to clear it.

### Common quick filters

- **Open · Reviewer: me** — what you need to review.
- **Open · Author: me** — your own pending PRs.
- **Draft** — work-in-progress PRs you've started but not published.

## Sorting

Click the sort icon in the toolbar to choose:

- **Created (newest)** — default
- **Created (oldest)**
- **Updated (newest)**
- **PR number**

## Background sync

The plugin polls Azure DevOps every **60 seconds** to keep the list up to date. New PRs, vote changes, and new comments appear without manual refresh.

If you've been notified that you've been added as a reviewer on a PR, a balloon notification appears in the lower-right corner — click it to jump straight to the PR.

To force an immediate refresh, click the **Reload** icon in the toolbar or press <shortcut>F5</shortcut> while the tool window is focused.

> On cold start, the list shows its **last-known cached state** while the first sync runs in the background — so you can act on PRs immediately instead of staring at a spinner.
> {style="note"}

## "Seen" tracking

Unseen PRs (new since your last visit) render in **bold**; seen PRs render in the normal weight. Opening a PR's detail view marks it seen for the rest of the session. You can also **Mark as seen** / **unseen** from the right-click menu.

## Search Everywhere integration

Press <shortcut>⇧ Shift</shortcut> twice to open *Search Everywhere* and type a PR title or number — Azure DevOps PRs appear alongside your usual search results. Selecting one opens its detail view directly.

## Create a pull request

Click the **+** button in the tool window toolbar to open the Create PR wizard.

### Wizard fields

- **Source branch** — defaults to your current Git branch.
- **Target branch** — defaults to the repository's default branch (typically `main`).
- **Title** — pre-filled from the last commit on the source branch.
- **Description** — markdown supported.
- **Reviewers** — start typing a name; the plugin offers @-mention-style autocomplete.
- **Work items** — attach Azure Boards work items by ID or by search.
- **Draft** — check this to create the PR as a draft (not yet ready for review).

> **AI-assisted titles & descriptions**: if you have an [AI provider configured](AI-Features.md), the wizard exposes a **Generate** button that drafts a PR title and description from your commits.
> {style="tip"}

## Current branch shortcut

If you're already checked out on the branch you want to review, you don't have to scroll the PR list. The action **Open Current Branch PR** (in <ui-path>VCS | Azure DevOps</ui-path>, or via *Find Action*) jumps you straight to the PR associated with your current branch.

The current branch's PR is also shown in the Git status bar widget — see [Git Integration](Git-Integration.md).

## Context menu actions

Right-click any PR in the list for quick actions:

- **Open** — open the detail view (same as double-click).
- **Open in browser** — open in the Azure DevOps web UI.
- **Copy link**
- **Mark as seen** / **unseen**
- **Reload**

## Detail view tabs

Each PR detail view is a closable editor tab with three sections — see [Code Review](Code-Review.md) for details on each one.
