# Statistics

A dedicated editor tab that turns your PR history into useful metrics — without leaving the IDE or running custom Azure DevOps queries.

> **Computed from cached data, not live polling.** Statistics use whatever the tool window has already fetched — opening the panel is instant and makes no extra API calls. The numbers update as the 60-second background sync brings new data in.
> {style="note"}

## Open the Statistics tab

From the Pull Requests tool window toolbar, click the chart icon, or run *Find Action* → **Show Pull Request Statistics**. The tab opens in the editor area.

## A typical day's numbers

For a team with ~15 active PRs, you might see something like:

| KPI                    | Value     |
|------------------------|-----------|
| Created (last 30 days) | 42        |
| Merged                 | 38        |
| Abandoned              | 2         |
| Open now               | 12        |
| Merge rate             | 90%       |
| **Median** merge time  | 18 h      |
| Approval rate          | 76%       |
| First response (h)     | 4 h       |

The KPIs use **median**, not average, for time-based metrics — a couple of week-long stragglers shouldn't shift the typical-PR number. Where an average is shown, it's labelled explicitly.

## Available metrics

### Open PRs by author

A horizontal bar chart of how many open PRs each author currently has. Useful for spotting unbalanced load on the team.

### Vote distribution

A pie / donut chart of the current vote state across all open PRs:

- **Approved**
- **Approved with suggestions**
- **Wait for author**
- **Rejected**
- **No vote**

Hover a slice to see the PRs in that bucket; click to open them in a filtered list.

### Time to merge

Histogram (or average + median) of how long PRs take from creation to completion, computed over completed PRs in the current filter window.

By default the window is the last 30 days; switch to 7, 90, or 365 days with the chips at the top of the tab.

### Review velocity

Median time from PR creation to first reviewer vote. Helps identify where PRs sit idle waiting for attention.

## Filtering

Statistics respect the same filters as the PR list, with a few extras specific to the panel:

- **Time window** — Last 7 / 30 / 90 / 365 days, or all-time.
- **Include drafts** — off by default.
- **Repository** — same as the tool window filter.

Changing a filter updates every metric on the panel.

## Caveats

> **Local view only.** Statistics are calculated from the PRs your account has permission to see. If you don't have access to a repository, its PRs aren't counted.
> {style="warning"}

The plugin is not a replacement for Azure DevOps Analytics. It gives you quick, in-editor signal — for org-wide reporting, use the Analytics service in Azure DevOps directly.

## Export

Right-click any chart to **Copy as image** (PNG) or **Copy data as CSV**. Useful for paste-into-Slack moments.
