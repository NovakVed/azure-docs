# 快速入门

从零开始，大约一分钟即可完成你的第一次 PR 审查。本页假设你已经[安装](Installation-zh.md)了该插件。

## 1. 打开托管在 Azure DevOps 上的项目

按常规方式克隆任意 Azure DevOps 仓库：

```bash
git clone https://dev.azure.com/your-org/your-project/_git/your-repo
cd your-repo
```

在 IDE 中打开该文件夹。插件会在启动时扫描 Git 远程仓库——当它检测到 `dev.azure.com` 或 `*.visualstudio.com` 远程仓库时便会激活，并显示 **Pull Requests** 工具窗口。

> **看不到工具窗口？** 当未检测到 Azure DevOps 远程仓库时，插件会自行隐藏。运行 `git remote -v` 确认某个远程 URL 中包含 `dev.azure.com`。
> {style="note"}

## 2. 登录

从左侧边栏打开 Pull Requests 工具窗口。在其登录界面上，你有两种选择：

- **Log In with Token…**（使用令牌登录）——粘贴一个来自 Azure DevOps 用户设置的个人访问令牌（Personal Access Token）。这是最快的方式，也是本地部署（on-prem）Azure DevOps Server 的唯一选项。
- **Log In via Microsoft…**（通过 Microsoft 登录）——通过 Microsoft Entra ID 进行基于浏览器的 OAuth 登录（仅适用于云端 `dev.azure.com`）。首先会弹出一个对话框，询问授予 **Full access** 还是 **Standard access**。

![Sign in with Microsoft 权限选择器，显示 Full access（推荐）和 Standard access](oauth-scope-dialog.png){ width="520" border-effect="line" }

如果你选择令牌，插件需要以下作用域：**Code (Read &amp; write + Status), User Profile (Read), Identity (Read), Work Items (Read), Security (Manage)**。登录对话框会列出这些作用域，其 **Generate…** 按钮会在浏览器中打开你所在组织的令牌页面。

> 有关完整的登录流程、作用域以及 Full 与 Standard 层级的选择，请参阅[身份验证](Authentication-zh.md)。
> {style="note"}

## 3. 浏览拉取请求

登录后，工具窗口会列出该仓库的拉取请求。

![Pull Requests 工具窗口，带有搜索字段、筛选器标签以及已填充的列表](pr-tool-window.png){ width="720" border-effect="line" }

要缩小列表范围：

- **Quick Filters**（快速筛选器）——点击标签行左侧的筛选器图标，一键使用预设：**Open pull requests**、**Awaiting my review**、**Involving me**。
- **Filter chips**（筛选标签）——**State**（Active / Completed / Abandoned）、**Author**、**Tags**、**Assignee**、**Review**（你的投票状态）、**Work Items** 和 **Draft**。
- **Sort**（排序）——最后一个标签：Newest、Oldest、Most/Least commented，或 Recently/Least recently updated。
- **Search**（搜索）——在标签上方的字段中输入内容，以匹配 PR 的标题和描述。

**点击**任意 PR，即可在编辑器标签页中打开其详情视图。

> **没有显示任何 PR？** 常见原因：(1) 你的账户无法访问此仓库——请先在 Azure DevOps 网页界面中打开它；(2) 项目指向了多个组织——通过工具窗口的齿轮图标 → **Switch Account / Repository…** 进行切换；(3) 确实没有活动的 PR——将 **State** 标签设为 **Completed** 以确认连接正常。
> {style="note"}

## 4. 审查代码

详情视图是**单一面板**——没有子标签页。从上到下依次为：带 `!` 编号的标题和一个 **View Timeline** 链接、源分支 → 目标分支、显示每位审查者投票的状态检查、变更文件树，以及一个操作栏。

![在单一面板详情视图中打开的拉取请求](pr-detail.png){ width="720" border-effect="line" }

- **阅读差异**——点击变更树中的任意文件以打开差异。点击某一行的行槽（gutter）即可评论。
- **阅读讨论**——点击 **View Timeline** 可在单独的标签页中打开完整的评论时间线。
- **投票**——操作栏的 **Approve** 按钮是一个拆分按钮。其下拉菜单包含 **Approve with suggestions**、**Wait for author**、**Reject** 和 **Reset feedback**。

![展开投票选项的 Approve 拆分按钮](vote-approve-dropdown.png){ width="380" border-effect="line" }

> **无需离开编辑器即可审查：** 检出某个 PR 的分支，插件便会将其评论直接叠加显示在你的常规编辑器上。请参阅[在编辑器中审查](Review-in-Editor-zh.md)。
> {style="tip"}

## 5. 创建拉取请求

从工具窗口的工具栏中，点击 **+**（Create Pull Request）。表单会预填源分支（你当前的分支）和默认目标分支。添加标题、描述和审查者，然后创建它。

![使用 AI 生成的标题和描述创建拉取请求](create-pr-ai.png){ width="640" border-effect="line" }

> **AI 辅助的标题和描述：** 在[已配置 AI 提供程序](AI-Features-zh.md)的情况下，表单的标题和描述字段会新增一个 **Generate** 操作，可根据你分支的差异同时起草两者。
> {style="tip"}

## 后续步骤

- [拉取请求](Pull-Requests-zh.md)——筛选、搜索、操作栏，以及溢出菜单（Complete、Revert、Compare）。
- [代码审查](Code-Review-zh.md)——内联差异、建议、投票，以及文件已查看跟踪。
- [通知与关注](Notifications-and-Attention-zh.md)——当某个 PR 需要你审查或 @提及 你时收到提醒。
- [AI 功能](AI-Features-zh.md)——摘要、AI 审查和语法润色。
