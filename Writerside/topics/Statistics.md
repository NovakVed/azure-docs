# Statistics

A dedicated editor tab that turns your PR history into KPIs and charts — no custom Azure DevOps queries, no leaving the IDE.

![The Pull Request Statistics dashboard](statistics-dashboard.png){ width="720" border-effect="line" }

> **Computed from cached data, not live polling.** Statistics use whatever the tool window has already fetched — opening the panel is instant and makes no extra API calls. The numbers update as background sync brings new data in.
> {style="note"}

## Open it

Click the **Pull Request Statistics** (chart) icon in the tool-window toolbar, or run *Find Action* → **Pull Request Statistics**. The tab opens in the editor area; **Refresh statistics** recomputes it.

## KPI tiles

A row of headline numbers across the top:

| KPI | Meaning |
|-----|---------|
| **Created** · **Merged** · **Abandoned** · **Open now** | PR counts in the window |
| **Merge rate** | Share of resolved PRs that merged |
| **Median merge (h)** | Typical hours from creation to completion |
| **Approval rate** | Share of reviewer votes that were Approved (incl. with suggestions) |
| **First response (h)** | Median hours to the first non-author comment |

> Time-based KPIs use the **median**, not the average — a couple of week-long stragglers shouldn't skew the typical-PR number. Where an average is shown, it's labelled.
> {style="note"}

## Charts

The charts are grouped into three sections:

- **Workload** — *Top creators*, *Top reviewers*, *Top commenters*, *Open PR aging*.
- **Process health** — *Vote distribution*, *PR status*, *Time to merge*, *PR cycle time (days)*, *Review velocity*.
- **Where work goes** — *Target branches*, *Daily activity*, *Day-of-week activity*, *PRs merged per week*, *Reviewer × Author* collaboration.

## Filter and scope

A sticky header scopes every metric at once:

- **Window** — Last 7 days, 30 days, 90 days, 6 months, 1 year, or All time.
- **Author**, **Reviewer**, **Target branch** — narrow to specific people or branches.
- **Clear filters** — reset to the defaults.

## Caveats

> **Local view only.** Statistics cover the PRs your account can see. Repositories you don't have access to aren't counted.
> {style="warning"}

This isn't a replacement for Azure DevOps Analytics — it's quick, in-editor signal. For org-wide reporting, use the Analytics service in Azure DevOps directly.
