# 拉取请求

**Pull Requests** 工具窗口是你的指挥中心：浏览队列、筛选与搜索、打开某个拉取请求，并对其执行操作——完成、还原、比较等等。

## 打开工具窗口

只要打开的项目至少包含一个 Azure DevOps Git 远程，工具窗口就会出现在左侧边栏。（没有 Azure DevOps 远程？它会保持隐藏，以减少杂乱。）

- 点击边栏中的 **Pull Requests** 条纹图标。
- 或使用 <ui-path>View | Tool Windows | Pull Requests</ui-path>。
- 或运行 *Find Action*（<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>）并输入 **Pull Requests**。

![带有搜索字段、筛选器纸片和已填充列表的 Pull Requests 工具窗口](pr-tool-window.png){ width="720" border-effect="line" }

## 查找拉取请求

### 默认视图：属于你的

未启用任何筛选器时，列表显示的内容与 Azure DevOps 网页版的 **Mine** 标签完全一致——由你**创建**、**分配给你**或**分配给你所在某个团队**的活动拉取请求。这是你进入时所处的视图，也是 *Clear filters* 将你带回的视图。

选择任意纸片、预设或搜索后，列表会切换为完整集合；清除它们后即可回到属于你的视图。

> 分配给团队的拉取请求需要正确的[权限](Permissions-zh.md)。如果你的凭据无法读取团队成员关系，插件会提示你一次——视图的其余部分照常工作。
> {style="note"}

### 快速筛选器

点击纸片行左侧的**筛选器图标**即可使用一键预设。图标上的徽标会显示当前有多少个筛选器处于活动状态。

![带有各种预设的快速筛选器菜单](quick-filters-menu.png){ width="380" border-effect="line" }

| 预设 | 显示内容 |
|--------|-------|
| **All pull requests** | 全部——脱离默认“属于你的”视图的出口 |
| **Open pull requests** | 所有活动拉取请求 |
| **Awaiting my review** | 你作为审阅者但尚未投票的拉取请求 |
| **Involving me** | 你创作、审阅或被提及的拉取请求 |
| **Clear N filter(s)** | 重置所有活动筛选器——回到默认“属于你的”视图 |

### 筛选器纸片

搜索字段下方有一行可滚动的纸片。点击任意纸片即可细化列表：

| 纸片 | 选项 |
|------|---------|
| **State** | Active · Completed · Abandoned |
| **Author** | 跨用户的即时输入搜索 |
| **Tags** | Azure DevOps 拉取请求标签（tags） |
| **Assignee** | 跨用户的即时输入搜索 |
| **Review** | Approved · Approved with suggestions · Waiting for author · Rejected · Awaiting my review |
| **Work Items** | 关联的 Azure Boards 工作项 |
| **Draft** | 仅草稿 · 仅非草稿 |
| **Sort** | Newest · Oldest · Most/Least commented · Recently/Least recently updated |

筛选器**按项目**在 IDE 重启后持久保存。要清除它们，请使用快速筛选器菜单中的 **Clear N filter(s)**。

> **搜索**——在纸片上方的字段中输入，即可匹配拉取请求的标题、编号、作者和分支名称。按两次 <shortcut>⇧ Shift</shortcut> 打开 *Search Everywhere*，Azure DevOps 拉取请求也会出现在其中——选中某个即可直接打开。
> {style="tip"}

### 跳转到特定拉取请求 {id="jump-to-a-specific-pr"}

当你已经知道想要哪个拉取请求时，可跳过列表。**Go to Pull Requests…** 会对每个已缓存的拉取请求进行模糊搜索——按 **id、标题、作者或仓库**——并直接在其时间线上打开。空搜索会列出每个已缓存的拉取请求（未读优先，然后是最新的）。

- 按 <shortcut>⌘⇧P</shortcut> / <shortcut>Ctrl+Shift+P</shortcut>。
- 或使用 <ui-path>VCS | Go to Pull Requests…</ui-path>。
- 或运行 *Find Action*（<shortcut>⌘⇧A</shortcut> / <shortcut>Ctrl+Shift+A</shortcut>）并输入 **Go to Pull Requests**。

默认情况下，它会在 IDE 的 *Search Everywhere* 弹出窗口中打开一个 **Pull Requests** 标签，与 Files、Symbols 和 Actions 并列；按 <shortcut>↵ Enter</shortcut> 打开高亮的拉取请求。

![Go to Pull Requests 结果：Search Everywhere 中的 Pull Requests 标签](go-to-pr-popup.png){ width="560" border-effect="line" }

> 更喜欢专用对话框？在[设置](Settings-zh.md)中**关闭** **Show in the Search Everywhere window**，该操作便会改为打开自己的快速选取弹出窗口——一个带有状态**漏斗**的搜索字段，以及 <shortcut>↵</shortcut> 打开 / <shortcut>⎋</shortcut> 关闭键。
> {style="tip"}

## 读懂一行拉取请求 {id="read-a-pr-row"}

每一行都一目了然地呈现状态：

![一行拉取请求的构成剖析](pr-row-anatomy.png){ width="640" border-effect="line" }

- **标题和 `!` 编号**，并在相关时附带**状态标签**：*Draft*、*Merged*、*Abandoned* 或 *Has merge conflicts*。
- **审阅者投票图标**——已批准、已批准并附建议、等待中或已拒绝。
- **琥珀色讨论徽标**，显示线程数量（以及仍有多少未解决）。
- **注意力纸片**——*Review requested*、*Mentions you* 或 *Replied*——当某个拉取请求需要你关注时出现。这些默认关闭；参见[通知与注意力](Notifications-and-Attention-zh.md)来开启它们。

未读的拉取请求可显示一个蓝色**未读标记**圆点，它会对新提交*以及*新评论活动作出反应。可从工具窗口齿轮 → **Show unread markers** 切换。

## 打开并操作拉取请求 {id="open-and-act-on-a-pr"}

**点击**某个拉取请求，即可在编辑器标签中打开其单窗格详情视图。底部的操作栏会根据你的角色自适应：

| 你的身份是… | 主要操作 |
|----------|-----------------|
| **审阅者** | **Approve ▾**（拆分按钮：Approve with suggestions、Wait for author、Reject、Reset feedback） |
| **作者，需要审阅** | **Request review** |
| **作者，审阅进行中** | **Complete ▾**（Set auto-complete…、Mark as draft、Abandon） |
| **未参与** | **Set myself as reviewer** |

每种状态还会显示一个包含完整操作集的 **⋮**（More）菜单：

![拉取请求操作栏的溢出菜单](pr-overflow-menu.png){ width="440" border-effect="line" }

| 操作 | 作用 |
|--------|--------------|
| **Share Pull Request…** | 通过电子邮件将拉取请求发送给他人（不会添加审阅者，也不会发布评论） |
| **Submit Pending Comments (N)** | 将你排队的评论作为一次审查发布（仅当 N > 0 时） |
| **Restart Merge** | 重新排队卡住的合并（冲突 / 失败 / 策略拒绝） |
| **Change Target Branch…** | 将拉取请求重新指向另一个目标分支 |
| **Cherry-Pick…** | 创建一个分支，将此拉取请求的提交挑选（cherry-pick）到另一个分支上 |
| **Review Changes Since…** | 将差异重新限定为自所选更新以来的变更——参见[代码审查](Code-Review-zh.md#compare) |
| **Revert…** | *（已合并的拉取请求）* 创建一个还原此拉取请求变更的分支 |
| **Open on Web** · **Copy Link** | 跳转到 / 复制 dev.azure.com URL |
| **Summarize Pull Request** · **Run AI Review** | [AI 辅助](AI-Features-zh.md) |

### 完成拉取请求 {id="complete-a-pull-request"}

点击 **Complete** 打开 **Complete Pull Request** 对话框。选择一个 **Merge type**——实时图示会显示所得历史的形状：

![带有合并策略图示的 Complete Pull Request 对话框](complete-pr-dialog.png){ width="560" border-effect="line" }

- **Merge (no fast forward)** · **Squash commit** · **Rebase and fast-forward** · **Semi-linear merge**
- **完成后选项：** 完成关联的工作项、删除源分支，并可选地自定义合并提交消息。

> **分支策略会被遵守。** 如果必需的审阅者或状态检查未满足，对话框会列出阻碍项。只有当你持有绕过（bypass）权限时，才会看到 **Override branch policies and enable merge**（需填写理由）。
> {style="warning"}

也可右键点击任意行以使用快速操作：**View Pull Request**、**View Pull Request in Browser**、**Copy Pull Request URL** 和 **Refresh List**。

## 创建拉取请求

点击工具窗口工具栏中的 **+**（Create Pull Request）。表单会预填充源分支（你的当前分支）和默认目标分支。

![Create Pull Request 表单：Write/Preview 描述编写器以及审阅者、标签和工作项行](create-pr-ai.png){ width="640" border-effect="line" }

**description**（描述）使用与拉取请求评论相同的编写器：一条 **Write | Preview** 标签条，编辑器上方有格式工具栏。输入 `@`、`#` 或 `!` 可对人员、工作项和拉取请求进行内联自动补全。按 <shortcut>⌘↵</shortcut> / <shortcut>Ctrl+Enter</shortcut> 创建。

描述下方的元数据区块是四个内联行——每行都带有一支用于编辑的铅笔，并在显示时带有一个用于清除的 **X**：

| 行 | 你设置的内容 |
|-----|--------------|
| **Required reviewers** | 必须审阅的人员 |
| **Optional reviewers** | 受邀审阅的人员 |
| **Tags** | Azure DevOps 拉取请求标签——选择现有的，或使用 **+** 创建全新标签 |
| **Work items** | 关联的 Azure Boards 工作项 |

主按钮是一个拆分按钮：**Create Pull Request**，其下拉菜单中有 **Create Draft Pull Request**。

> 在[启用 AI](AI-Features-zh.md) 后，描述编写器工具栏会新增一个 AI 按钮（工具提示 **Generate title &amp; description with AI**），它会根据你分支的提交起草标题和描述。如果尚未设置任何 AI 提供程序，点击它会提示打开 AI Settings。
> {style="tip"}

## 刷新与后台同步

Azure DevOps 没有 webhook，因此插件会轮询。列表会自行更新，但你也可以按需刷新：

- 在工具窗口获得焦点时按 <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> 或 <shortcut>F5</shortcut>。
- 或右键点击某一行 → **Refresh List**。

> 轮询节奏为[设置](Settings-zh.md)中的 **Sync interval**（默认 60 秒）。冷启动时，列表会在首次同步进行期间显示其**最近已知的缓存状态**，因此你可以立即操作，而不必等待加载图标。
> {style="note"}

## 切换账户或仓库

对于绑定到多个组织或仓库的项目，请使用工具窗口齿轮 → **Switch Account / Repository…**。当前分支的拉取请求还会显示在 Git 分支小组件和状态栏中——参见 [Git 集成](Git-Integration-zh.md)。
