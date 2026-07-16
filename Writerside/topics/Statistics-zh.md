# 统计

一个专用的编辑器选项卡，将你的 PR 历史转化为 KPI 和图表——无需自定义 Azure DevOps 查询，也无需离开 IDE。

![拉取请求统计仪表板](statistics-dashboard.png){ width="720" border-effect="line" }

> **基于缓存数据计算，而非实时轮询。** 统计使用工具窗口已经获取的数据——打开面板是即时的，不会产生额外的 API 调用。随着后台同步引入新数据，这些数字会随之更新。
> {style="note"}

## 打开它

在工具窗口工具栏中点击 **Pull Request Statistics**（图表）图标，或运行 *Find Action* → **Pull Request Statistics**。该选项卡会在编辑器区域中打开；**Refresh statistics** 会重新计算它。

## KPI 磁贴

顶部有一行醒目的数字：

| KPI | 含义 |
|-----|---------|
| **Created** · **Merged** · **Abandoned** · **Open now** | 时间窗口内的 PR 数量 |
| **Merge rate** | 已解决的 PR 中已合并的占比 |
| **Median merge (h)** | 从创建到完成的典型小时数 |
| **Approval rate** | 审查者投票中为 Approved（含带建议的批准）的占比 |
| **First response (h)** | 到第一条非作者评论的中位小时数 |

> 基于时间的 KPI 使用**中位数**，而非平均值——个别耗时长达一周的滞后项不应扭曲典型 PR 的数字。凡是显示平均值的地方，都会明确标注。
> {style="note"}

## 图表

图表分为三个部分：

- **Workload** - *Top creators*、*Top reviewers*、*Top commenters*、*Reviewer × Author* 协作。
- **Process health** - *Vote distribution*、*Time to merge*、*PR status*、*Open PR aging*、*PR cycle time (days)*、*PRs merged per week*。
- **Where work goes** - *Target branches*、*Day-of-week activity*、*Daily activity*。

## 筛选与范围

一个固定的标题栏可一次性限定所有指标的范围：

- **Window** - 最近 7 天、30 天、90 天、6 个月、1 年，或全部时间。
- **Author**、**Reviewer**、**Target branch** - 缩小到特定的人员或分支。
- **Clear filters** - 重置为默认值。

## 注意事项

> **仅本地视图。** 统计涵盖你的账户可见的 PR。你无权访问的仓库不会被计入。
> {style="warning"}

这不是 Azure DevOps Analytics 的替代品——它是快速的、编辑器内的信号。若需组织范围的报告，请直接使用 Azure DevOps 中的 Analytics 服务。
