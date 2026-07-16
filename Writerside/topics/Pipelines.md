# Pipelines

Browse, run, and review Azure Pipelines without leaving the IDE - a dedicated **Pipelines** tool window with an interactive stage graph, adaptive run tabs, live job logs, in-IDE approvals, and run-finished notifications.

> Pipelines integration is **on by default** - a single master switch in [Settings](Settings.md). The tool window, run notifications, stripe badge, and in-IDE pipeline checks all ride on it; turn it off and they disappear together.
> {style="note"}

## Pipelines settings

Pipelines is enabled out of the box. Its master switch and companion options live at <ui-path>Settings | Version Control | Azure DevOps</ui-path>, under the **Pipelines** group.

| Setting | What it does |
|---------|--------------|
| **Enable Pipelines integration** | Shows the Pipelines tool window and opens pull-request pipeline checks inside the IDE. When off, the tool-window icon is hidden, no pipeline notifications or badges fire, and pipeline checks open in the browser instead. |
| **Notify when a pipeline run of mine finishes** | Fires a balloon when a run you triggered reaches a terminal state. Enabled only when integration is on. |
| **Badge the Pipelines tool-window icon when my runs finish** | Adds a coloured dot to the Pipelines stripe icon - red on failure, amber on partial, blue on success - until you open the window. Enabled only when integration is on. |

> The **Pipelines** stripe icon only appears once the project has an **Azure DevOps remote** *and* the integration switch is on. It's anchored on the left, below **Pull Requests**, and shares the same signed-in account and repository as the Pull Requests window.
> {style="note"}

Open (or focus) the window with <shortcut>⌘⇧W</shortcut> / <shortcut>Ctrl+Shift+W</shortcut>. On Windows / Linux the plugin picks the first free combo instead - **hover the stripe icon to see the actual key**. The shortcut is seeded at IDE startup, so after installing or updating the plugin you must **fully restart the IDE**. See [Keyboard Shortcuts](Keyboard-Shortcuts.md).

## The Pipelines tool window

The window opens on a **Pipelines** list tab. Its title actions (top-right) are **Run Pipeline…** (trigger a pipeline run) and **Refresh** (reload pipeline runs); the gear menu adds **Switch Account / Repository…**.

![The Pipelines tool window with the runs navigation bar and definitions list](pipelines-tool-window.png){ width="720" border-effect="line" }

### Navigate runs

A search bar sits across the top, mirroring the Pull Requests window:

- A **free-text search field** that matches name, branch, build number, and who requested the run.
- A **View** chip with three scopes - **Recent**, **All**, and **Runs** (default **Recent**).
- A **Status** chip that filters by last-run result: **Succeeded**, **Partially succeeded**, **Failed**, **Running**, **Canceled**.
- A **Filter** quick-menu (with a live-indicator badge) titled **Quick filters**: **All pipelines**, **Recently run**, **All runs**, **Failed only**, and **Clear filters** once any are active.

Each **View** scope shows a different body:

| Scope | Shows | Open a run |
|-------|-------|------------|
| **Recent** | A flat list of pipeline **definitions**, each with its latest-run status icon and a `folder · last run <relative>` subtitle. | Double-click / <shortcut>↵ Enter</shortcut> opens the latest run; right-click → **Run Pipeline…**. |
| **All** | Pipeline definitions as a collapsible **folder tree** (`\Team\SubTeam`), with descendant counts. | Double-click / <shortcut>↵ Enter</shortcut> a leaf opens its latest run; on a folder it toggles expansion; right-click a leaf → **Run Pipeline…**. |
| **Runs** | A flat, scrollable list of recent **runs**. | Double-click / <shortcut>↵ Enter</shortcut> opens the run. |

### Follow a run's jobs

Opening a run adds a closeable `#<n>` tab - a pure navigator, no logs. Its header is the run status glyph plus the pipeline name and a clickable `#<run number>` that opens the run in the browser. Below sits the **jobs rail**: a **Summary** link, an **All jobs** heading, then jobs **grouped under collapsible stage headers**.

Click **Summary** to open the run overview editor, click a **job** to open the editor on that job's step logs, and click a **stage header** to collapse it. <shortcut>↵ Enter</shortcut> mirrors clicks.

### The stripe badge

When a run **you triggered** finishes and you haven't opened the window, the Pipelines stripe icon gets a coloured dot - **red on failure, amber on partial, blue on success**. It clears the moment you open or focus the window, and is wiped on an account or org switch. Gate it with **Badge the Pipelines tool-window icon when my runs finish** in [Settings](Settings.md). See [Notifications &amp; Attention](Notifications-and-Attention.md).

## Open a run's overview

Clicking **Summary** (or a job) opens the **run overview** as a main-editor tab titled with the run label (for example `#20260101.1`). Re-opening the same run focuses the existing tab.

![A pipeline run overview: header, tabs, and the interactive stage graph](pipeline-run-overview.png){ width="720" border-effect="line" }

The header shows the run status icon, the pipeline name and run number, and a muted meta line (`status • branch • requestedFor • duration`). Right-aligned actions are **Cancel** (while running), **Re-run** (when terminal, re-queuing on the same source branch), and an **Open in Browser** link. If a stage is waiting on you, an **approval gate** band sits directly under the header - see [In-IDE approvals](#approvals).

### The interactive stage graph

The **Summary** tab opens on a **Stages** heading and a zoomable, pannable DAG of stage cards. When the server omits `dependsOn` the graph falls back to job cards or a sequential chain, and disconnected flows are laid into separate vertical bands.

![The stage graph with a focused stage tracing its flow](pipeline-stage-graph.png){ width="700" border-effect="line" }

- The zoom toolbar (top-right) has **Zoom out**, **Zoom in**, **Fit to view**, and **Keyboard shortcuts** (opens the `?` cheat sheet).
- **Drag** anywhere to pan; the **wheel** zooms around the cursor (fit never zooms past 1.0×).
- Hovering or clicking a stage lights its flow - **Depends on** edges in blue, **Runs after** edges in green, others dimmed - and a caption card and legend appear as overlays.
- Each card's **chevron** expands it to list its jobs and a **Rerun stage** button.
- Clicking a job (or a stage) navigates the editor to that job's step logs.

> Use <shortcut>=</shortcut> / <shortcut>-</shortcut> / <shortcut>0</shortcut> to zoom in, out, and fit the graph, and <shortcut>?</shortcut> to pop the **Pipeline run shortcuts** cheat sheet.
> {style="tip"}

## The run tabs

Three tabs are always present - **Summary**, **Environments**, and **Code coverage**. Two more are inserted **only when a terminal run published that data**, in Azure-web order right after Summary: **Tests** (when the run reported tests) and **Extensions** (when it published extension summaries).

| Tab | What it shows |
|-----|---------------|
| **Summary** | The stage graph, plus a **Repositories** card (columns **Resource Name, Repository, Branch/Tag, Version, Related**) when the run has repository resources. |
| **Tests** | A donut summary and the associated test cases (see below). |
| **Extensions** | Extension-published markdown summaries (for example a SonarQube quality gate) as rounded cards. |
| **Environments** | A table of **Environment, Last stage, Result, Finished**. |
| **Code coverage** | Per-metric rows, each with a donut (green ≥80%, amber ≥50%, red below) and an `X / Y covered` figure. |

When a terminal run has artifacts, an **Artifacts:** strip at the bottom links each one (opens the download URL in the browser). Sections that can't load while you're offline say so and load when you reconnect.

### The Tests tab

![The Tests tab: outcome donut, stat blocks, and the filterable results table](pipeline-tests-tab.png){ width="720" border-effect="line" }

A **donut** (green **Passed**, red **Failed**, grey **Others**) sits beside stat blocks - **Total tests**, **Pass percentage**, **Run duration**, and **Tests not reported**. Below it, the **Test results** card carries a filter bar:

- A search box (**Filter by test or run name**); <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> focuses it while the Tests tab is showing, and <shortcut>Esc</shortcut> clears it.
- Facet chips - **Test file** and **Owner** (each shown only with two or more distinct values), plus an **Outcome** chip. Outcome buckets are **Failed, Aborted, Passed, Not Impacted, Others**, and the default filter is **Failed + Aborted**.

The table columns adapt to the data - **Test**, **Owner** (if any), **Duration** (if any), **Outcome** - and are capped at 300 rows. When a filter hides everything, a **Show all tests** link clears every filter.

## View job logs

Clicking a job (from the jobs rail or a stage card) opens **GitHub-Actions-style collapsible step sections**: each header is a chevron, status icon, step name, and duration; expanding it reveals a numbered, colour-coded log rendered in the editor font (`##[error]` red, `##[warning]` amber, `##[section]` bold, `##[command]` blue). The failed step auto-expands, and logs stream in place while the run is live.

![A job's collapsible step logs with colour-coded output](pipeline-job-logs.png){ width="720" border-effect="line" }

A slim header bar above the logs has a **← Summary** back-link (tooltip "Back to the run overview (L)"), then the job's status icon, name, and meta.

> **Search the logs:** press <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> inside a job's logs to open the IDE find bar (with a match counter and Case / Words / Regex toggles). <shortcut>↵ Enter</shortcut> and <shortcut>⇧↵</shortcut> walk matches - expanding collapsed steps and scrolling each hit into view - and <shortcut>Esc</shortcut> hides the bar.
> {style="tip"}

## In-IDE approvals {id="approvals"}

When a stage is gated on a manual approval you're assigned to, an approval band appears under the run header - **one callout card per pending gate**, in the same red-tinted chrome as the Complete-PR "blocked by" banner.

![An approval gate card with the comment field and Approve / Reject buttons](pipeline-approval-gate.png){ width="640" border-effect="line" }

Each card shows **Approval needed — &lt;Stage&gt;**, a `N of M approved · in sequence · waiting since <time>` meta line, the check's instructions, and per-approver rows with their state (**Approved**, **Rejected**, **Reassigned**, **Pending**). The action row has an optional-comment field (**Add an optional comment…**) and right-aligned **Reject** and **Approve** buttons, with **Approve** in the primary slot.

> If the run's requester isn't allowed to approve their own run, the buttons are replaced by an explanation and a **Review in browser** link. Permission and offline problems surface inline on the card rather than failing silently.
> {style="note"}

## Run a pipeline

Choose **Run Pipeline…** from the tool-window title actions or a definition's right-click menu to open the **Run Pipeline** dialog (its OK button reads **Run**).

![The Run Pipeline dialog: pipeline and branch pickers, parameters, and variables](pipeline-run-dialog.png){ width="560" border-effect="line" }

- **Pipeline** and **Branch** pickers - searchable combo boxes. Pipeline rows show a name and folder subtitle; branch rows show short branch names plus an **Enter a branch or ref…** escape for a custom ref (for example `main` or `refs/tags/v1.0`). Branches are enumerated only for Azure Repos pipelines.
- A **Parameters** section renders the YAML's declared `parameters:` as a typed form - a dropdown for `values:`, a checkbox for booleans, a monospace YAML area for objects, and a text field otherwise; required parameters are marked `*`.
- A **Variables** section exposes queue-time-settable definition variables (secrets stay blank to keep the stored value).
- Two checkboxes: **Enable system diagnostics** (adds `system.debug=true`) and **Preview only (render final YAML, don't queue)**.

A real run refreshes the list and opens the new run's detail. **Preview only** instead opens a read-only **Pipeline Preview — final YAML** dialog.

## Run-finished notifications

When a run **you triggered** reaches a terminal state, a balloon appears titled `<pipeline> <run#> <verb>` (succeeded / partially succeeded / failed / was canceled), with the branch in the body and an **Open run** action that opens the run detail in the IDE. It's deduped per run and outcome, and gated on both the master switch and **Notify when a pipeline run of mine finishes**. See [Notifications &amp; Attention](Notifications-and-Attention.md).

![A run-finished notification balloon with the Open run action](pipeline-notification.png){ width="420" border-effect="line" }

## Open a PR's pipeline check in the IDE

With the integration on, clicking **Details…** on a pull request's pipeline CI check opens that run **inside the IDE**, jumping straight to the relevant job's logs - the deep-linked job if the URL names one, otherwise the first failed or running job. In-progress checks paint the Pipelines blue "waiting" disc. With the master switch off, pipeline checks open in the browser like any other status.

## Keyboard shortcuts

The run overview has its own in-view keys, active while it's focused. Press <shortcut>?</shortcut> (or the **?** button on the stage-graph toolbar) for the same list. They aren't in Keymap and can't be rebound.

| Action | Shortcut |
|--------|----------|
| **View logs / back** to the stage graph | <shortcut>L</shortcut> |
| **Previous / next tab** | <shortcut>[</shortcut> / <shortcut>]</shortcut> |
| **Zoom in / out / fit** the stage graph | <shortcut>=</shortcut> / <shortcut>-</shortcut> / <shortcut>0</shortcut> |
| **Open this run in the browser** | <shortcut>B</shortcut> |
| **Filter tests** (Tests tab) | <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> |
| **Show this list** | <shortcut>?</shortcut> |

> Inside a job's **logs**, <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> opens the log search bar instead. The full plugin shortcut reference lives in [Keyboard Shortcuts](Keyboard-Shortcuts.md).
> {style="note"}

> **Next up:** tune what fires in [Notifications &amp; Attention](Notifications-and-Attention.md), or review every plugin setting in [Settings](Settings.md).
> {style="tip"}
