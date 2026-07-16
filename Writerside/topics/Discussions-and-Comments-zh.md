# 讨论与评论

无需离开 IDE 即可在拉取请求中进行完整的对话：markdown 编辑器、@提及、工作项和拉取请求引用、建议的修改、图片附件、AI 语法润色以及线程解决。

## 线程出现的位置

同一批线程会显示在三个地方：

- **差异中的内联位置** - 锚定到它们所引用的行。参见[代码审查](Code-Review-zh.md)。
- **时间线** - 按时间顺序展示每个线程和拉取请求事件的视图。从拉取请求详情视图中的 **View Timeline** 链接打开它。（使用 **Find in timeline** 进行搜索。）
- **编辑器中** - 当检出拉取请求的分支时，叠加在你正常的编辑器上。参见[在编辑器中审查](Review-in-Editor-zh.md)。

## 评论编辑器

每个评论编辑器 - 时间线、差异内嵌、内联编辑以及 Create-PR 描述 - 都共享同一个 GitHub 风格的编辑器。左上角是 **Write | Preview** 选项卡条；格式化工具栏沿着同一条顶部条排布，紧靠选项卡右侧对齐，其中 **Polish grammar &amp; spelling with AI** 在一个分隔符之后固定在最右端。底部一行有一个浅色的 **Add files** 链接，位于提交按钮的左侧。

![带有 Write | Preview 选项卡和顶部格式化工具栏条的评论编辑器，以及底部一行提交按钮旁边的 Add files 链接](comment-toolbar.png){ width="640" border-effect="line" }

| 分组 | 按钮 |
|-------|---------|
| **References** | Mention user (`@`)、Reference work item (`#`)、Reference pull request (`!`) |
| **Formatting** | Heading、Bold、Italic、Inline code、Link |
| **Lists** | Bulleted、Numbered、Task list |
| **AI** | **Polish grammar &amp; spelling with AI** |

在差异/编辑器内嵌中，你还会看到 **Insert code suggestion**。键盘快捷键：<shortcut>⌘B</shortcut> 加粗、<shortcut>⌘I</shortcut> 斜体、<shortcut>⌘E</shortcut> 内联代码、<shortcut>⌘K</shortcut> 链接、<shortcut>⌘↵</shortcut> 提交（或对应的 <shortcut>Ctrl</shortcut> 组合键）。

点击 **Preview** 可将编辑器切换为你的 markdown 的渲染视图 - 与已发布评论所用的渲染相同，因此你预览的内容与你将要发布的内容一致。在显示 Preview 时格式化工具栏会隐藏；点击 **Write** 返回编辑。空白草稿预览为 *Nothing to preview*。

> **Polish grammar &amp; spelling with AI** 会就地将你的草稿（或所选内容）重写为一次可撤销的编辑。它需要[配置 AI 提供程序](AI-Features-zh.md)；当 AI 关闭时，该按钮会被隐藏。
> {style="tip"}

## @提及

点击 **Mention user** 或输入 `@` 可打开你组织中人员的自动完成列表。用方向键选择一个并按 <shortcut>Enter</shortcut>；被提及的用户会收到 Azure DevOps 通知。

点击已有的 `@mention` 可打开一张小巧的**作者卡片**，其中包含此人的头像和姓名。当已知其电子邮件时（拉取请求作者或某位审查者），该卡片会提供 **Copy email** 和 **Send email**。

> @提及自动完成需要 **Identity (Read)** 范围（PAT）或 **Full access**（OAuth）。参见[身份验证](Authentication-zh.md)。
> {style="note"}

## 图片与附件

附加图片的三种方式：

- **Add files** - 点击底部一行（提交按钮左侧）的 **Add files** 链接，从磁盘选择图片文件。
- **Paste** - 从剪贴板粘贴图片（<shortcut>⌘V</shortcut> / <shortcut>Ctrl+V</shortcut>）。
- **Drag &amp; drop** - 将图片文件拖放到编辑器上。

支持的类型有 `png`、`jpg`、`jpeg`、`gif`、`webp`、`bmp` 和 `svg`。每次上传都会显示一个 *Uploading…* 占位符，然后变为内联 markdown 图片。右键点击已发布的图片可使用 **Copy Image Link** 或 **Download Image…**。

## 建议的修改

要提出一处具体的更改而非描述它，请使用**建议**。在差异/编辑器内嵌中，点击 **Insert code suggestion**（它会预填被评论的行）或输入一个 ```` ```suggestion ```` 代码块。

![带有 Apply Locally 操作的建议更改](suggestion-block.png){ width="560" border-effect="line" }

该线程会渲染一张 **Suggested change** 卡片，带有 **Apply Locally**（以及 **Commit…**，可一步完成应用并提交）。在检出拉取请求分支之前以及在已解决的线程上，Apply 会被禁用。

## 回复、解决与管理线程

- **Reply** - 添加一条后续内容。Azure DevOps 线程是扁平的；你的回复会落在线程末尾。
- **Resolve / Reopen** - 在线程完成时关闭它，或将其重新打开。已解决的线程会被弱化显示，并在差异筛选器设为 *Show only unresolved* 时被隐藏。
- **👍 Thumbs up** - 位于评论正文下方的反应行中的点赞按钮（在审查线程上与 **Reply** / **Resolve** 共用一行）。一旦至少有一个赞，它就会显示计数，并在你点赞后变为金色；其工具提示会在 **Thumbs up** 和 **Remove thumbs up** 之间切换。
- **More actions (⋯)** - 评论标题中的溢出菜单。对任何评论：**Copy link**、**Copy Markdown** 和 **Quote reply**（将该评论作为 `>` 块引用插入到此线程的回复编辑器中），外加 **Hide** - 一种仅本地的折叠操作，就地隐藏正文，并在重建和重启后保留。在你自己的评论上，你还会看到 **Edit** 和 **Delete**。

### 线程状态

除了已解决/未解决之外，线程还带有一个状态标记。点击它（**Change status**）可在以下状态之间切换：

| 状态 | 含义 |
|--------|---------|
| **Active** | 新线程（不显示标记）。 |
| **Pending** | 等待作者的修改。 |
| **Resolved** | 更改已应用。 |
| **Won't fix** | 已知悉，但不会进行该更改。 |
| **Closed** | 讨论完成，无需操作。 |

## 时间线事件

时间线还会在评论旁边显示系统事件：投票更改、审查者的添加/移除、工作项的链接/取消链接、已完成的状态检查，以及强制推送（带有比较提交的链接）。
