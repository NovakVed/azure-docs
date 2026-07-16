# 代码审查

使用 IntelliJ 原生的差异查看器审查拉取请求：阅读改动、留下行内评论和建议、投票，并跟踪你已经查看过的文件。

## 详情视图

打开一个 PR 会创建一个可关闭的编辑器选项卡——**单一面板**，没有子选项卡。从上到下依次为：标题和 `!` 编号（带有 **View Timeline** 链接）、源 → 目标分支、状态检查（CI、冲突、必需审查者及其投票）、**changed-files 树**，以及操作栏。

![在单面板详情视图中打开的拉取请求](pr-detail.png){ width="720" border-effect="line" }

- **改动的文件**位于树中——点击其中一个即可打开差异。
- **讨论**通过 **View Timeline** 链接在其自己的选项卡中打开——参见 [讨论与评论](Discussions-and-Comments-zh.md)。
- **投票和操作**位于操作栏及其溢出菜单中——参见 [拉取请求](Pull-Requests-zh.md#open-and-act-on-a-pr)。

## 阅读差异

点击某个文件会在每个 PR 的单一选项卡中打开差异——点击另一个文件会就地替换它，因此 <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> 可以逐个浏览整个 PR 中所有改动的区域。差异选项卡带有一个 **Review:** 工具栏，包含 **Refresh**、**Submit review** 和 **Previous / Next Comment**。

| 导航 | macOS | Windows / Linux |
|----------|-------|------------------|
| 下一个 / 上一个改动区域 | <shortcut>F7</shortcut> / <shortcut>⇧F7</shortcut> | <shortcut>F7</shortcut> / <shortcut>Shift+F7</shortcut> |
| 下一个 / 上一个评论 | *Review: 工具栏* | *Review: 工具栏* |

### 显示或隐藏讨论线程

在差异的边栏设置中，**Review Discussions** 菜单控制渲染哪些行内讨论线程：**Show all discussions**、**Show only unresolved** 或 **Don't show**。

## 对某一行评论

<procedure title="添加行内评论">
    <step>将鼠标悬停在改动行的边栏上——会出现一个 <b>+</b>。点击它（或在行号上拖动以跨越一个范围）。你也可以在光标处按 <shortcut>⌃⇧M</shortcut> / <shortcut>Ctrl+Shift+M</shortcut>。</step>
    <step>输入你的评论。编辑器使用与 PR 讨论相同的 GitHub 风格外观——带有格式工具栏的 <b>Write</b> / <b>Preview</b> 选项卡条位于顶部，还支持 @提及 和图片粘贴。完整的编辑器介绍参见 <a href="Discussions-and-Comments-zh.md">讨论与评论</a>。</step>
    <step>通过拆分式提交按钮发布评论。主操作是 <b>Start Review</b>，它会将评论作为待处理审查的一部分排队；其下拉菜单包含 <b>Add Single Comment</b>（立即发布）和 <b>Suggest change</b>（将所选内容包装为作者可应用的建议改动）。</step>
</procedure>

![在差异查看器中打开的行内评论](diff-comment.png){ width="720" border-effect="line" }

> **待处理审查。** 你排队的评论会保持为草稿状态（计入 **Submit (N)** 按钮），直到你将它们与你的投票一起提交——这与 GitHub 用户所熟悉的审查流程相同。从 **Review:** 工具栏或溢出菜单的 **Submit Pending Comments** 提交。
> {style="note"}

### 复制代码链接

在差异查看器中右键点击某一行——或在你正常编辑器中审查时右键点击——并选择 **Copy Link to Code**，即可复制指向该代码的 Azure DevOps Web 深层链接（文件、行和列范围），这与 Web UI 的 **Copy link** 生成的链接相同。选中文本后，该菜单项会显示为 **Copy Link to Selected Code** 并链接到确切的字符跨度；未选中时，它会复制光标处的整行链接。快捷键是 <shortcut>⌘⇧L</shortcut> / <shortcut>Ctrl+Shift+L</shortcut>。

> 该操作仅在 Azure PR 审查界面（差异查看器或在编辑器中审查界面）内出现——在普通编辑器中它会保持隐藏。
> {style="note"}

## 投票

操作栏的 **Approve** 按钮是一个拆分式按钮：其下拉菜单包含 **Approve with suggestions**、**Wait for author**、**Reject** 和 **Reset feedback**。

![Approve 拆分按钮的投票选项](vote-approve-dropdown.png){ width="380" border-effect="line" }

完成或放弃 PR（包括合并策略）的相关内容在 [拉取请求](Pull-Requests-zh.md#complete-a-pull-request) 中介绍。

## 将文件标记为已查看

对于大型 PR，请随着审查进度将每个文件标记为**已查看**——已查看的文件会在改动树中变暗。

- 按 <shortcut>⌘⇧S</shortcut> / <shortcut>Ctrl+Shift+S</shortcut>，或右键 → **Mark File as Viewed**。
- 选中多个文件后右键点击可 **Mark All as Viewed**。

![在改动树中的 Mark File as Viewed](mark-file-viewed.png){ width="560" border-effect="line" }

> 想让文件在你打开时自动标记为已查看？在 [设置](Settings-zh.md) 中打开 **Mark files as viewed when their diff is opened**（默认关闭，与 GitHub 一致）。
> {style="tip"}

## 只审查自某次更新以来的改动 {id="compare"}

当作者推送新的提交时，你不必重新阅读整个 PR。从溢出 **⋮** 菜单中选择 **Review Changes Since…**，选取一次更新，改动树就会重新限定为仅显示该差异——期间合并进来的目标分支提交会被过滤掉。

![改动树上方的迭代范围横幅](compare-updates-banner.png){ width="700" border-effect="line" }

一个横幅——*“Reviewing only what changed since update N”*——位于树的上方；点击 **Show all changes** 可返回完整的 PR。（当 PR 至少有两次更新后，该操作才会出现。）

## 改为在编辑器中审查

当 PR 的源分支已检出时，你可以直接在正常编辑器中对改动的行进行评论——无需差异选项卡。参见 [在编辑器中审查](Review-in-Editor-zh.md)。
