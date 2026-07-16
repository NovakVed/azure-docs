# 管道

无需离开 IDE 即可浏览、运行和审查 Azure Pipelines —— 一个专用的 **Pipelines** 工具窗口，具备交互式阶段图、自适应运行选项卡、实时作业日志、IDE 内审批以及运行完成通知。

> 管道集成**默认开启** —— 由 [Settings](Settings-zh.md) 中的单一主开关控制。工具窗口、运行通知、条纹徽标和 IDE 内管道检查都依赖于它；将其关闭，它们会一起消失。
> {style="note"}

## 管道设置

管道开箱即用地处于启用状态。它的主开关及配套选项位于 <ui-path>Settings | Version Control | Azure DevOps</ui-path>，在 **Pipelines** 分组下。

| 设置 | 作用 |
|---------|--------------|
| **Enable Pipelines integration** | 显示 Pipelines 工具窗口，并在 IDE 内打开拉取请求的管道检查。关闭时，工具窗口图标被隐藏，不会触发管道通知或徽标，管道检查将改为在浏览器中打开。 |
| **Notify when a pipeline run of mine finishes** | 当你触发的运行达到终止状态时弹出气泡提示。仅在集成开启时可用。 |
| **Badge the Pipelines tool-window icon when my runs finish** | 在 Pipelines 条纹图标上添加一个彩色圆点 —— 失败为红色、部分成功为琥珀色、成功为蓝色 —— 直到你打开该窗口。仅在集成开启时可用。 |

> **Pipelines** 条纹图标只有在项目具有 **Azure DevOps remote** *且*集成开关开启后才会出现。它锚定在左侧，位于 **Pull Requests** 下方，并与 Pull Requests 窗口共享同一个已登录账户和仓库。
> {style="note"}

用 <shortcut>⌘⇧W</shortcut> / <shortcut>Ctrl+Shift+W</shortcut> 打开（或聚焦）该窗口。在 Windows / Linux 上，插件会改为选取第一个可用的组合键 —— **将鼠标悬停在条纹图标上以查看实际按键**。该快捷键在 IDE 启动时植入，因此在安装或更新插件后，你必须**完全重启 IDE**。参见 [Keyboard Shortcuts](Keyboard-Shortcuts-zh.md)。

## Pipelines 工具窗口

窗口在一个 **Pipelines** 列表选项卡上打开。它的标题操作（右上角）是 **Run Pipeline…**（触发一次管道运行）和 **Refresh**（重新加载管道运行）；齿轮菜单还提供 **Switch Account / Repository…**。

![带有运行导航栏和定义列表的 Pipelines 工具窗口](pipelines-tool-window.png){ width="720" border-effect="line" }

### 浏览运行

顶部横贯一个搜索栏，与 Pull Requests 窗口相呼应：

- 一个**自由文本搜索字段**，匹配名称、分支、构建编号以及请求该运行的人。
- 一个 **View** 标签，具有三种范围 —— **Recent**、**All** 和 **Runs**（默认 **Recent**）。
- 一个 **Status** 标签，按最近一次运行的结果筛选：**Succeeded**、**Partially succeeded**、**Failed**、**Running**、**Canceled**。
- 一个 **Filter** 快捷菜单（带有实时指示徽标），标题为 **Quick filters**：**All pipelines**、**Recently run**、**All runs**、**Failed only**，以及在任意筛选处于活动状态时出现的 **Clear filters**。

每种 **View** 范围显示不同的主体：

| 范围 | 显示内容 | 打开一次运行 |
|-------|-------|------------|
| **Recent** | 一个扁平的管道**定义**列表，每项带有其最近一次运行的状态图标以及 `folder · last run <relative>` 副标题。 | 双击 / <shortcut>↵ Enter</shortcut> 打开最近一次运行；右键单击 → **Run Pipeline…**。 |
| **All** | 以可折叠的**文件夹树**（`\Team\SubTeam`）形式呈现的管道定义，带有后代计数。 | 双击 / <shortcut>↵ Enter</shortcut> 叶节点打开其最近一次运行；在文件夹上则切换展开状态；右键单击叶节点 → **Run Pipeline…**。 |
| **Runs** | 一个扁平、可滚动的近期**运行**列表。 | 双击 / <shortcut>↵ Enter</shortcut> 打开该运行。 |

### 跟踪一次运行的作业

打开一次运行会添加一个可关闭的 `#<n>` 选项卡 —— 一个纯粹的导航器，没有日志。它的标题是运行状态字形加上管道名称，以及一个可点击的 `#<run number>`，用于在浏览器中打开该运行。下方是**作业导航条**：一个 **Summary** 链接、一个 **All jobs** 标题，然后是**分组在可折叠阶段标题下**的作业。

点击 **Summary** 打开运行概览编辑器，点击某个**作业**打开该作业步骤日志的编辑器，点击某个**阶段标题**将其折叠。<shortcut>↵ Enter</shortcut> 与点击效果一致。

### 条纹徽标

当**你触发的**某次运行完成而你尚未打开该窗口时，Pipelines 条纹图标会出现一个彩色圆点 —— **失败为红色、部分成功为琥珀色、成功为蓝色**。它会在你打开或聚焦窗口的那一刻清除，并在切换账户或组织时被抹去。用 [Settings](Settings-zh.md) 中的 **Badge the Pipelines tool-window icon when my runs finish** 控制它。参见 [Notifications &amp; Attention](Notifications-and-Attention-zh.md)。

## 打开一次运行的概览

点击 **Summary**（或某个作业）会将**运行概览**作为一个主编辑器选项卡打开，标题为运行标签（例如 `#20260101.1`）。重新打开同一次运行会聚焦已有的选项卡。

![一次管道运行概览：标题、选项卡和交互式阶段图](pipeline-run-overview.png){ width="720" border-effect="line" }

标题显示运行状态图标、管道名称和运行编号，以及一行灰显的元信息（`status • branch • requestedFor • duration`）。右对齐的操作有 **Cancel**（运行中时）、**Re-run**（终止后，在同一源分支上重新排队），以及一个 **Open in Browser** 链接。如果某个阶段正在等待你处理，标题正下方会有一条**审批门控**条带 —— 参见 [IDE 内审批](#approvals)。

### 交互式阶段图

**Summary** 选项卡打开时会显示一个 **Stages** 标题以及一个可缩放、可平移的阶段卡片 DAG。当服务器省略 `dependsOn` 时，该图回退为作业卡片或顺序链，且互不相连的流程被排布到各自独立的垂直条带中。

![带有聚焦阶段并追踪其流程的阶段图](pipeline-stage-graph.png){ width="700" border-effect="line" }

- 缩放工具栏（右上角）具有 **Zoom out**、**Zoom in**、**Fit to view** 和 **Keyboard shortcuts**（打开 `?` 速查表）。
- 在任意处**拖动**可平移；**滚轮**围绕光标缩放（适应视图从不会缩放超过 1.0×）。
- 悬停或点击某个阶段会点亮其流程 —— **Depends on** 边为蓝色，**Runs after** 边为绿色，其他则变暗 —— 并以覆盖层形式显示说明卡片和图例。
- 每张卡片的**折叠箭头**会将其展开，列出其作业以及一个 **Rerun stage** 按钮。
- 点击某个作业（或某个阶段）会将编辑器导航至该作业的步骤日志。

> 使用 <shortcut>=</shortcut> / <shortcut>-</shortcut> / <shortcut>0</shortcut> 放大、缩小和适应该图，用 <shortcut>?</shortcut> 弹出 **Pipeline run shortcuts** 速查表。
> {style="tip"}

## 运行选项卡

始终存在三个选项卡 —— **Summary**、**Environments** 和 **Code coverage**。另外两个**仅在某次终止运行发布了相应数据时**插入，按 Azure 网页顺序紧跟在 Summary 之后：**Tests**（当运行报告了测试时）和 **Extensions**（当它发布了扩展摘要时）。

| 选项卡 | 显示内容 |
|-----|---------------|
| **Summary** | 阶段图，加上一个 **Repositories** 卡片（列为 **Resource Name、Repository、Branch/Tag、Version、Related**），前提是该运行具有仓库资源。 |
| **Tests** | 一个圆环摘要以及关联的测试用例（见下文）。 |
| **Extensions** | 扩展发布的 markdown 摘要（例如一个 SonarQube 质量门），以圆角卡片形式呈现。 |
| **Environments** | 一个 **Environment、Last stage、Result、Finished** 表格。 |
| **Code coverage** | 逐指标行，每行带有一个圆环（绿色 ≥80%、琥珀色 ≥50%、低于则为红色）以及一个 `X / Y covered` 数字。 |

当某次终止运行有产物时，底部会有一条 **Artifacts:** 条带，链接每一个产物（在浏览器中打开下载 URL）。在你离线时无法加载的部分会如实说明，并在你重新连接时加载。

### Tests 选项卡

![Tests 选项卡：结果圆环、统计块和可筛选的结果表](pipeline-tests-tab.png){ width="720" border-effect="line" }

一个**圆环**（绿色 **Passed**、红色 **Failed**、灰色 **Others**）位于统计块旁边 —— **Total tests**、**Pass percentage**、**Run duration** 和 **Tests not reported**。其下方，**Test results** 卡片带有一个筛选栏：

- 一个搜索框（**Filter by test or run name**）；<shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> 在 Tests 选项卡显示时聚焦它，<shortcut>Esc</shortcut> 清除它。
- 分面标签 —— **Test file** 和 **Owner**（各自仅在有两个或更多不同值时显示），加上一个 **Outcome** 标签。结果分桶为 **Failed、Aborted、Passed、Not Impacted、Others**，默认筛选为 **Failed + Aborted**。

表格列会根据数据自适应 —— **Test**、**Owner**（如有）、**Duration**（如有）、**Outcome** —— 并被限制在 300 行。当某个筛选隐藏了全部内容时，一个 **Show all tests** 链接会清除所有筛选。

## 查看作业日志

点击某个作业（从作业导航条或某张阶段卡片）会打开 **GitHub Actions 风格的可折叠步骤区块**：每个标题是一个折叠箭头、状态图标、步骤名称和时长；将其展开会显示以编辑器字体渲染的带编号、按颜色编码的日志（`##[error]` 红色、`##[warning]` 琥珀色、`##[section]` 加粗、`##[command]` 蓝色）。失败的步骤会自动展开，且在运行处于实时状态时日志会就地流式传输。

![一个作业的可折叠步骤日志，带有按颜色编码的输出](pipeline-job-logs.png){ width="720" border-effect="line" }

日志上方有一条纤细的标题栏，带有一个 **← Summary** 返回链接（工具提示“Back to the run overview (L)”），然后是作业的状态图标、名称和元信息。

> **搜索日志：** 在某个作业的日志内按 <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> 打开 IDE 查找栏（带有匹配计数器以及 Case / Words / Regex 切换）。<shortcut>↵ Enter</shortcut> 和 <shortcut>⇧↵</shortcut> 在匹配项之间移动 —— 展开折叠的步骤并将每个命中项滚动到视野中 —— 而 <shortcut>Esc</shortcut> 隐藏该栏。
> {style="tip"}

## IDE 内审批 {id="approvals"}

当某个阶段被门控在一个指派给你的手动审批上时，运行标题下方会出现一条审批条带 —— **每个待处理门控一张说明卡片**，采用与 Complete-PR “blocked by” 横幅相同的红色着色外观。

![带有评论字段和 Approve / Reject 按钮的审批门控卡片](pipeline-approval-gate.png){ width="640" border-effect="line" }

每张卡片显示 **Approval needed — &lt;Stage&gt;**、一行 `N of M approved · in sequence · waiting since <time>` 元信息、该检查的说明，以及逐审批人行及其状态（**Approved**、**Rejected**、**Reassigned**、**Pending**）。操作行有一个可选评论字段（**Add an optional comment…**）以及右对齐的 **Reject** 和 **Approve** 按钮，其中 **Approve** 位于主要位置。

> 如果不允许运行的请求者审批他们自己的运行，按钮会被替换为一段解释和一个 **Review in browser** 链接。权限和离线问题会就地显示在卡片上，而不是无声地失败。
> {style="note"}

## 运行管道

从工具窗口标题操作或某个定义的右键菜单中选择 **Run Pipeline…** 以打开 **Run Pipeline** 对话框（其 OK 按钮显示为 **Run**）。

![Run Pipeline 对话框：管道和分支选择器、参数和变量](pipeline-run-dialog.png){ width="560" border-effect="line" }

- **Pipeline** 和 **Branch** 选择器 —— 可搜索的组合框。管道行显示名称和文件夹副标题；分支行显示短分支名称，加上一个 **Enter a branch or ref…** 出口，用于自定义 ref（例如 `main` 或 `refs/tags/v1.0`）。仅对 Azure Repos 管道枚举分支。
- **Parameters** 部分将 YAML 声明的 `parameters:` 渲染为一个带类型的表单 —— 对 `values:` 用下拉框，对布尔值用复选框，对对象用等宽 YAML 区域，其余用文本字段；必填参数标有 `*`。
- **Variables** 部分公开可在排队时设置的定义变量（密钥保持空白以保留已存储的值）。
- 两个复选框：**Enable system diagnostics**（添加 `system.debug=true`）和 **Preview only (render final YAML, don't queue)**。

真实的一次运行会刷新列表并打开新运行的详情。**Preview only** 则改为打开一个只读的 **Pipeline Preview — final YAML** 对话框。

## 运行完成通知

当**你触发的**某次运行达到终止状态时，会出现一个气泡，标题为 `<pipeline> <run#> <verb>`（succeeded / partially succeeded / failed / was canceled），正文中带有分支，并有一个 **Open run** 操作，用于在 IDE 中打开运行详情。它按运行和结果去重，并同时受主开关和 **Notify when a pipeline run of mine finishes** 门控。参见 [Notifications &amp; Attention](Notifications-and-Attention-zh.md)。

![带有 Open run 操作的运行完成通知气泡](pipeline-notification.png){ width="420" border-effect="line" }

## 在 IDE 中打开某个 PR 的管道检查

在集成开启的情况下，点击拉取请求的管道 CI 检查上的 **Details…** 会**在 IDE 内**打开该次运行，直接跳转到相关作业的日志 —— 如果 URL 指明了某个作业则为该深链作业，否则为第一个失败或正在运行的作业。进行中的检查会绘制 Pipelines 蓝色“waiting”圆盘。在主开关关闭的情况下，管道检查会像任何其他状态一样在浏览器中打开。

## 键盘快捷键

运行概览有自己的视图内按键，在它处于聚焦状态时激活。按 <shortcut>?</shortcut>（或阶段图工具栏上的 **?** 按钮）可查看同一列表。它们不在 Keymap 中，无法重新绑定。

| 操作 | 快捷键 |
|--------|----------|
| **查看日志 / 返回**阶段图 | <shortcut>L</shortcut> |
| **上一个 / 下一个选项卡** | <shortcut>[</shortcut> / <shortcut>]</shortcut> |
| **放大 / 缩小 / 适应**阶段图 | <shortcut>=</shortcut> / <shortcut>-</shortcut> / <shortcut>0</shortcut> |
| **在浏览器中打开此次运行** | <shortcut>B</shortcut> |
| **筛选测试**（Tests 选项卡） | <shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> |
| **显示此列表** | <shortcut>?</shortcut> |

> 在某个作业的**日志**内，<shortcut>⌘F</shortcut> / <shortcut>Ctrl+F</shortcut> 会改为打开日志搜索栏。完整的插件快捷键参考见 [Keyboard Shortcuts](Keyboard-Shortcuts-zh.md)。
> {style="note"}

> **下一步：** 在 [Notifications &amp; Attention](Notifications-and-Attention-zh.md) 中调整触发内容，或在 [Settings](Settings-zh.md) 中查看每一项插件设置。
> {style="tip"}
