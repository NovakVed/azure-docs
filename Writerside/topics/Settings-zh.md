# 设置

插件提供的每一项设置的参考。使用 <shortcut>⌘,</shortcut>（macOS）或 <shortcut>Ctrl+Alt+S</shortcut>（Windows/Linux）打开 **Settings**。

## Version Control → Azure DevOps

主页面。顶部是 **accounts** 面板（添加 **+**、编辑 ✏、移除 ✕、按项目设置默认值）——参见[身份验证](Authentication-zh.md)。

![Azure DevOps 设置页面的账户面板](accounts-panel.png){ width="700" border-effect="line" }

- **Sync interval (seconds)** —— 工具窗口轮询 Azure DevOps 的频率。**默认 60**，范围 **15–3600**。

### Polling & notifications

| 设置 | 默认值 |
|---------|---------|
| **Notify when I'm asked to review a pull request** | 开 |
| **Notify when someone @mentions me in a pull request** | 开 |
| **Notify on replies in threads I participated in** | 开 |
| **Notify when reviewer votes change on my PRs** | 开 |
| **Offer Create PR after I push to an Azure DevOps remote** | 开 |
| **Include my own pull requests and @mentions** | 关 |

关于这些设置的作用，参见[通知与关注](Notifications-and-Attention-zh.md)。

### Pull request review

| 设置 | 默认值 |
|---------|---------|
| **Mark files as viewed when their diff is opened** | 关 |
| **Show attention markers on pull-request rows** | 关 |
| **Show keyboard shortcut on comment buttons** | 开 |

最后一个开关会在编辑器的 **Comment** / **Reply** / **Save** 按钮标签之前显示提交快捷键（<shortcut>⌘↵</shortcut> / <shortcut>Ctrl+Enter</shortcut>）。快捷键无论如何都有效——此选项只是显示提示。

> **Show unread markers** 不在这里——它是一个工具窗口开关（齿轮菜单），而不是设置中的复选框。草稿是列表**筛选器**，而不是一项设置。
> {style="note"}

### Go to Pull Requests

| 设置 | 默认值 |
|---------|---------|
| **Show in the Search Everywhere window** | 开 |

控制 **Go to Pull Requests** 的打开方式。启用时，该操作会在 Search Everywhere 中添加一个 **Pull Requests** 选项卡（位于 Files / Symbols / Actions 旁边）。取消勾选后，则改为打开一个独立的快速选择对话框。

## Version Control → Azure DevOps → AI Settings

用于配置可选 AI 助手的子页面——参见 [AI 功能](AI-Features-zh.md)。

![AI Settings 页面](ai-settings.png){ width="720" border-effect="line" }

- **General AI Settings → Enable AI assistance** —— 主开关。**默认关闭。** 关闭时会隐藏所有 AI 相关功能，且不进行任何外发调用。
- **AI Providers** —— 每个提供程序实例一行（**Provider / Model / Enabled**）。第一个启用的行为默认项。通过 **Add AI Provider** 对话框添加（OpenAI、Claude、Gemini、Ollama、GitHub Copilot；HTTP-API 或 CLI 模式）。
- **Per-Feature Provider** —— 将 **AI Summary**、**AI Review**、**Title + Description** 和 **Explain Code** 路由到特定实例，或保持其为 **Default**。
- **Configure Prompts** —— 编辑每项功能的系统提示词。
- **Advanced** —— **Cache AI responses per commit SHA**（默认开启）、**Max diff size**（默认 200 KB，范围 10–2000）以及 **Clear AI Response Cache**。

## Appearance & Behavior → Notifications {id="notifications"}

插件注册了两个可路由的通知组（弹窗 / 工具窗口 / 仅日志）：

| 通知组 | 用途 |
|-------|-----|
| **Azure DevOps Pull Requests** | 审查请求、@提及、回复、投票变更、推送提示。 |
| **Azure DevOps AI** | AI 摘要 / 审查完成气泡。 |

## Keymap

打开 <ui-path>Settings | Keymap</ui-path> 并搜索 **Azure DevOps**，即可重新绑定任意操作。包含操作 ID 的完整列表见[键盘快捷键](Keyboard-Shortcuts-zh.md)。

## Per-project vs application-level

大多数设置是**应用程序级别**的（对所有项目生效）：账户、通知偏好、AI 提供程序。其中两项是**按项目**（存储在项目工作区中）：**默认账户**和你的 **PR 列表筛选器**。
