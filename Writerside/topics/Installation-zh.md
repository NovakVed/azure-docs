# 安装

在任何运行 %min_ide_build% 或更新版本的 JetBrains IDE 中安装 %product%。

> **摘要** - 在 <ui-path>Settings | Plugins | Marketplace</ui-path> 中搜索 **Azure DevOps Pull Requests**，点击 **Install**，然后重启。接着打开一个带有 Azure DevOps 远程仓库的项目并[登录](Authentication-zh.md)。
> {style="tip"}

## 支持的 IDE

该插件面向 IntelliJ 平台，可在任何基于它构建的 IDE 上运行：

- IntelliJ IDEA（Ultimate 和 Community）
- JetBrains Rider
- PyCharm（Professional 和 Community）
- WebStorm、PhpStorm、GoLand、RubyMine、CLion、DataGrip、RustRover
- Android Studio（可能可用；未正式支持）

### 最低构建版本

该插件需要 IDE 构建版本 `%min_ide_build%.*` 或更新版本 - 即每个 JetBrains IDE 的 **%min_ide_version%** 发行版 - 因为它使用了该版本引入的平台 API。

> **检查你的版本：** 从 IDE 菜单打开 **About**，查找以 `%min_ide_build%` 开头的构建号。如果版本较低，请先运行 **Help → Check for Updates**。
> {style="note"}

## 从 Marketplace 安装

<procedure title="安装插件">
    <step>打开 <ui-path>Settings | Plugins | Marketplace</ui-path>（macOS 上按 <shortcut>⌘,</shortcut>，Windows/Linux 上按 <shortcut>Ctrl+Alt+S</shortcut>）。</step>
    <step>搜索 <b>Azure DevOps Pull Requests</b>。</step>
    <step>点击 <b>Install</b>。</step>
    <step>出现提示时重启 IDE。</step>
</procedure>

![从 JetBrains Marketplace 安装](marketplace-install.png){ width="700" border-effect="line" }

### 验证是否成功

打开一个带有 Azure DevOps Git 远程仓库的项目，然后检查：

- **Pull Requests** 条纹图标出现在左侧工具窗口栏中。
- <ui-path>Settings | Version Control | Azure DevOps</ui-path> 已存在。

> **看不到工具窗口？** 当项目**没有 Azure DevOps 远程仓库**时，它会被隐藏。运行 `git remote -v` 并确认某个 URL 包含 `dev.azure.com` 或 `visualstudio.com`。参见[故障排除](Troubleshooting-zh.md)。
> {style="note"}

## 从磁盘安装

对于预发布的 `.zip` 构建：

<procedure title="从磁盘安装">
    <step>打开 <ui-path>Settings | Plugins</ui-path>。</step>
    <step>点击齿轮图标 → <b>Install Plugin from Disk…</b></step>
    <step>选择 <code>.zip</code> 文件并重启。</step>
</procedure>

## 系统要求

| 组件 | 最低要求 | 说明 |
|-----------|---------|-------|
| IDE 构建版本 | %min_ide_build%.* | JetBrains %min_ide_version% 或更新版本 |
| JDK | 21 | 随 IDE 捆绑 |
| Git | 2.20+ | 分支检测与 HTTPS 认证交接 |
| 操作系统 | macOS / Windows / Linux | IDE 支持的任何平台 |
| 网络 | 到 Azure DevOps 的 HTTPS | `dev.azure.com` 或你的自托管服务器 |

> **使用代理？** 该插件使用 IDE 自身的 HTTP 代理。只需在 <ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path> 中设置一次，Azure DevOps 和（HTTP）AI 调用都会继承它。基于 CLI 的 AI 提供程序是外部二进制文件，不会通过它路由。
> {style="note"}

## 必需的捆绑插件

该插件**依赖于**两个 IDE 捆绑插件（在所有环境中默认启用）。如果其中任一被禁用，插件将无法加载 - 请在 <ui-path>Settings | Plugins | Installed</ui-path> 中重新启用它们：

- **Git**（`Git4Idea`）- 分支检测与 HTTPS 凭据。
- **Markdown** - 为评论和描述编辑器提供支持。

## 更新与卸载

更新会显示在 <ui-path>Settings | Plugins | Installed</ui-path> 中 - 当有更新时点击 **Update**，然后**重启 IDE**，以便新版本完全加载。要卸载，请使用齿轮图标 → **Uninstall**；你存储的凭据也会从钥匙串中移除。

> **安装或更新后请重启。** 该插件会注册若干启动挂钩（例如工具窗口激活快捷键），因此它不会原地热重载 - 完整重启 IDE 可确保一切都连接就绪。
> {style="note"}

> **下一步：** 阅读[快速入门](Quick-Start-zh.md)进行一分钟的快速了解，或阅读[身份验证](Authentication-zh.md)进行登录。要启用摘要和 AI 审查，请参见 [AI 功能](AI-Features-zh.md)。
> {style="tip"}
