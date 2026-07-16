# 疑难解答

针对用户最常遇到的问题的快速修复方法。对于决策类问题（例如“我应该使用 OAuth 还是 PAT？”“它支持本地部署吗？”），请参阅 [常见问题](FAQ-zh.md)。如果此处未涵盖你的问题，请参阅底部的 [提交缺陷](#filing-a-bug)。

## 工具窗口没有出现

当未检测到 Azure DevOps Git 远程时，Pull Requests 工具窗口会被隐藏。请检查：

<procedure>
    <step>在项目根目录中运行 <code>git remote -v</code>。至少要有一个远程 URL 包含 <code>dev.azure.com</code> 或 <code>visualstudio.com</code>（或你配置的自托管服务器）。</step>
    <step>确认捆绑的 <b>Git</b> 插件（<code>Git4Idea</code>）已在 <ui-path>Settings | Plugins | Installed</ui-path> 中启用。</step>
    <step>重启 IDE — 远程扫描会在项目打开时运行。</step>
</procedure>

## 登录后出现“401 Unauthorized”

- PAT 可能缺少所需的作用域 — 请参阅 [身份验证](Authentication-zh.md)。最简单的修复方法：使用 **Full access** 重新生成。
- PAT 可能已过期。令牌会在你创建时设定的日期过期。
- 你的组织可能已禁用 PAT — 这种情况下请改用 OAuth。

## 特定操作出现“403 Forbidden”

PAT 有效，但你的 Azure DevOps 账户没有执行该操作的权限（例如你可以读取拉取请求但不能投票，或无法合并）。请让你的 Azure DevOps 管理员在相应项目或仓库上授予所需权限。

## OAuth 浏览器没有返回到 IDE

OAuth 通过**本地回环重定向**完成 — 浏览器会被重定向回 `http://127.0.0.1:<port>/azure-oauth/callback`，该地址由 IDE 的内置 Web 服务器提供服务，随后会显示 *“Sign-in complete. You can close this tab.”*。如果这一往返过程失败：

- 防火墙或安全工具可能正在阻止到 IDE 内置服务器的 localhost 连接（端口范围 **63342–63352**）。
- 被拦截的弹出窗口或非默认浏览器可能会中断重定向 — 请确保你想使用的浏览器是默认浏览器。
- 登录窗口有 **5 分钟** 的时限；如果已超时，请重新开始。

变通方法：改用个人访问令牌（Personal Access Token）而非 OAuth。

## 同步后拉取请求不显示新评论

<procedure>
    <step>按 <shortcut>⌘R</shortcut> / <shortcut>Ctrl+R</shortcut> / <shortcut>F5</shortcut>（或右键单击 → <b>Refresh List</b>）立即强制同步 — 工具栏上没有 Reload 按钮。</step>
    <step>检查 <b>idea.log</b> 中是否有同步错误（<a anchor="enabling-debug-logs">启用调试日志</a> 以获取更多详情）。</step>
    <step>默认的同步间隔为 60 秒。如果你在 <a href="Settings-zh.md">设置</a> 中增大了该间隔，延迟会更长。</step>
</procedure>

## 内联评论没有出现在差异中

- 插件仅在你拥有 **Code (Read)** 权限的拉取请求上渲染内联评论线程。
- 如果你查看的是本地工作树中的差异（而非拉取请求），内联线程不会渲染 — 请从工具窗口打开拉取请求，以便加载其变更树和评论线程。
- 如果你的本地分支与拉取请求头已发生分叉，编辑器内审查会自行禁用。请推送你的更改，或精确检出拉取请求头。

## Git 推送时要求输入密码

插件的 HTTPS 凭据提供程序仅对**在 IDE 内**运行的 Git 操作生效（从 IDE 内启动的终端也算作“内部”）。对于外部终端，请配置系统级别的 Git 凭据助手：

```bash
# macOS Keychain
git config --global credential.helper osxkeychain

# Windows
git config --global credential.helper manager

# Linux (libsecret)
git config --global credential.helper libsecret
```

## AI 功能缺失或返回错误

- 打开 <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path>，确认已勾选 **Enable AI assistance**，并且至少配置并启用了一个提供程序。
- 在提供程序行上单击 **Test connection** — 如果失败，请仔细核对 API 密钥、模型名称和端点 URL。
- 对于 **Ollama**，请确认守护进程正在本地运行（`ollama serve`），并且你指定的模型已拉取（`ollama list`）。
- 对于 **CLI providers**（Claude Code、Codex、Copilot CLI），请确保二进制文件位于 `PATH` 中并已登录（`claude /login` 等）。
- 提供程序的速率限制或配额错误直接来自提供程序 — 它们不会被重试。

## 插件冲突

本插件与捆绑的 **GitHub** 插件和 **GitLab** 插件共享 IDE 的 `collaboration-tools` 工具包。它与两者共存 — 各自拥有独立的工具窗口和独立的状态。有两个已知的交互点：

- 如果一个项目同时具有 Azure DevOps 和 GitHub 远程，两个工具窗口都会出现；右键上下文菜单可能会同时显示来自两者的操作。
- 如果第三方插件覆盖了 AI 扩展点（`intellij.vcs.azuredevops.aiSummaryExtension` 等，参见 [隐私与数据](Privacy-and-Data-zh.md)），则该功能的内置默认实现会被绕过。如果 AI 功能表现异常，请在 <ui-path>Settings | Plugins</ui-path> 中检查是否有其他可能挂接这些扩展点的 Azure DevOps 或 AI 插件。

## 网络超时或“request failed”

插件使用 IntelliJ 的 HTTP 代理配置 — 没有单独的代理设置。如果公司网络限制阻止了出站 HTTPS：

- 检查 <ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path>。插件会遵循你在此处设置的内容。
- AI 流式请求的 HTTP 超时时间为 **5 分钟**。超过该时间的都会被视为挂起，并作为通知报告。
- Azure DevOps API 调用的重试行为是“快速失败” — 瞬时错误不会被重试，以免 UI 堆积重复调用。60 秒的后台同步会从失败请求中断处继续。

## 插件更新导致某些功能失效

回滚到先前版本：

<procedure>
    <step>打开 <ui-path>Settings | Plugins | Installed</ui-path>，找到 <b>Azure DevOps Pull Requests</b>。</step>
    <step>单击齿轮图标 → <b>Manage Plugin Versions</b>。</step>
    <step>选择一个较旧的版本并安装。</step>
    <step>重启 IDE。</step>
</procedure>

## 启用调试日志 {id="enabling-debug-logs"}

若需更深入的疑难解答，请启用跟踪日志记录：

<procedure>
    <step>打开 <ui-path>Help | Diagnostic Tools | Debug Log Settings…</ui-path></step>
    <step>添加以下行：
        <code-block lang="text">
#com.vednovak.azure
#com.vednovak.azure.sync
#com.vednovak.azure.api
        </code-block>
    </step>
    <step>重现该问题。</step>
    <step>打开 <ui-path>Help | Show Log in Explorer/Finder</ui-path> 以找到 <code>idea.log</code>。</step>
</procedure>

日志位于你的 IDE 缓存目录中：

<tabs>
    <tab title="macOS">
        <code>~/Library/Logs/JetBrains/&lt;IDE&gt;&lt;Version&gt;/idea.log</code>
    </tab>
    <tab title="Windows">
        <code>&#37;LOCALAPPDATA&#37;\JetBrains\&lt;IDE&gt;&lt;Version&gt;\log\idea.log</code>
    </tab>
    <tab title="Linux">
        <code>~/.cache/JetBrains/&lt;IDE&gt;&lt;Version&gt;/log/idea.log</code>
    </tab>
</tabs>

## 提交缺陷 {id="filing-a-bug"}

如果你发现了可复现的问题：

<procedure>
    <step>运行 <ui-path>Help | Diagnostic Tools | Collect Logs and Diagnostic Data</ui-path>。</step>
    <step>打开 <a href="%repo_url%/issues/new">一个新的 GitHub issue</a> 并包含以下内容：
        <ul>
            <li>你的 IDE 版本（<b>About</b>）</li>
            <li>插件版本</li>
            <li>操作系统与架构</li>
            <li>重现步骤</li>
            <li>预期行为与实际行为</li>
            <li>一段经过脱敏的 <code>idea.log</code> 片段（发布前请移除令牌）</li>
        </ul>
    </step>
</procedure>

> **切勿在公开的 issue 中粘贴 PAT 或 OAuth 刷新令牌**。日志默认会捕获经过脱敏的令牌，但提交前请务必再次检查。
> {style="warning"}
