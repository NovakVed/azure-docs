# Git 集成

该插件与 IDE 内置的 Git 插件协同工作，用于检测 Azure DevOps 远程仓库、将当前分支匹配到对应的拉取请求，并交接 HTTPS 凭据，从而让 `git fetch` 和 `git push` 顺畅运行。

## 仓库检测

当你打开一个项目时，插件会扫描每个 Git 远程仓库，查找以下模式：

- `https://dev.azure.com/<org>/<project>/_git/<repo>`
- `https://<org>.visualstudio.com/<project>/_git/<repo>`（旧版）
- `git@ssh.dev.azure.com:v3/<org>/<project>/<repo>`（SSH）
- 来自你的账户的自托管 Azure DevOps Server URL

如果任一远程仓库匹配成功，**Pull Requests** 工具窗口就会出现，并开始后台同步。否则插件不会干扰你的工作。

## 当前分支 → 拉取请求

插件会监视你签出的分支，并将其解析为匹配的开放拉取请求（按源分支名称匹配）。找到后，两个小组件会亮起。

### 主工具栏分支小组件

**main toolbar** 中的 Git 分支小组件会显示一个 Azure DevOps 徽章 - `!1234 on feature/login`。点击它可查看该拉取请求的操作：

![主工具栏分支小组件弹出菜单](branch-widget-popup.png){ width="440" border-effect="line" }

- **Show in Tool Window** - 打开该拉取请求的详情视图。
- **Update Pull Request Branch** - 当你的本地分支与拉取请求头分支产生分歧时出现（运行 *Update Project*）。
- **Review in Editor** - 切换编辑器内审查叠加层。参阅 [在编辑器中审查](Review-in-Editor-zh.md)。

### 状态栏小组件

**status bar** 中另有一个小组件，显示 `ADO PR !1234`。点击它可在工具窗口中打开该拉取请求。（可通过状态栏小组件选择器隐藏或显示它 - 其名称为 *Azure DevOps PR (current branch)*。）

当你切换分支时，两个小组件都会更新 - 并在新分支没有拉取请求时消失。

## HTTPS 身份验证

当 Git 需要为 Azure DevOps 远程仓库提供 HTTPS 凭据时，插件会自动提供已存储的令牌：

<procedure title="HTTPS 身份验证交接的工作原理">
    <step>你在 IDE 内部运行 <code>git fetch</code> 或 <code>git push</code>（通过 Update Project、Git 工具窗口或内嵌终端）。</step>
    <step>Git 向 IDE 请求凭据。</step>
    <step>插件将远程仓库匹配到已登录的账户，并提供其令牌。</step>
    <step>Git 继续执行 - 无需密码提示。</step>
</procedure>

如果有多个已登录账户匹配同一个 URL，则使用项目的 **default account**（参阅 [设置](Settings-zh.md)）。

> 从 IDE 之外的 **system shell** 运行的 Git 命令不会看到此凭据提供程序。如果你主要在外部终端中工作，请配置一个系统级的 Git 凭据助手 - 参阅 [疑难解答](Troubleshooting-zh.md#git-push-asks-for-a-password)。
> {style="note"}

## 推送 → 创建拉取请求

当你推送一个尚无拉取请求的分支后，插件可以在气泡中提示 **Create a pull request** - 这比使用工具栏更快捷。可通过 [设置](Settings-zh.md) 中的 **Offer Create PR after I push to an Azure DevOps remote** 来开关此功能。其他由 Git 驱动的通知（审查请求、投票变更、回复）在 [通知与关注](Notifications-and-Attention-zh.md) 中介绍。

## 多仓库与自托管

- **Multiple repositories** 在同一项目中会被各自独立检测；使用工具窗口的 **Switch Account / Repository…** 可聚焦于其中一个。
- **Azure DevOps Server (on-prem)** 的用法与云端产品完全相同 - 登录时添加服务器 URL，并使用从该服务器生成的令牌。
