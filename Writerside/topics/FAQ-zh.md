# 常见问题

关于是否以及如何使用 %product% 的决策类问题。对于"它出问题了，我该如何修复？"这类问题，请参阅[疑难解答](Troubleshooting-zh.md)。

## 该插件支持 Azure DevOps Server（本地部署）吗？

支持。在创建帐户时添加服务器的 URL。Azure DevOps Server 2019+ 和 Azure DevOps Services（云端）均受支持。

云端产品使用 `dev.azure.com/<org>`。本地部署使用你自己的服务器 URL（例如 `https://devops.example.com`）。PAT 身份验证对两者都有效。通过 Microsoft Entra 的 OAuth **仅限云端**。

## 它支持 Azure Pipelines 吗？

支持。专用的 **Pipelines** 工具窗口让你可以浏览管道和运行、观看交互式阶段图、阅读彩色编码的步骤日志，以及审批或拒绝手动审批门——全部都在 IDE 内完成。当拉取请求的 CI 检查指向某个 Azure 构建时，点击 **Details…** 会在 IDE 内而不是浏览器中打开该运行。

它默认开启。在 <ui-path>Settings | Version Control | Azure DevOps</ui-path> 下切换 **Enable Pipelines integration**——关闭时，工具窗口会被隐藏，不会触发任何管道通知或徽章，管道检查会在浏览器中打开。请参阅[管道](Pipelines-zh.md)。

## 它能与传统的 TFVC（非 Git）仓库一起使用吗？

不能。该插件仅适用于以 Git 为后端的 Azure Repos。**TFVC**（Team Foundation Version Control，微软在 Azure DevOps 中先于 Git 的集中式版本控制系统）不受支持。

## 我可以在没有 Azure DevOps 帐户的情况下使用它吗？

不能——该插件专用于 Azure DevOps。对于 GitHub 或 GitLab，请分别使用捆绑的 GitHub 插件或 JetBrains GitLab 插件。

## 我可以在同一个 IDE 中同时安装 GitHub 和 Azure DevOps 的 PR 插件吗？

可以。它们注册各自独立的工具窗口，且不共享状态。如果单个项目的远程同时指向 GitHub 和 Azure DevOps，两个工具窗口都会出现；每个窗口只列出它自己远程的 PR。

## OAuth 还是 PAT——我该选哪个？

| 你应该使用…      | 何时                                                                                              |
|-----------------|--------------------------------------------------------------------------------------------------------------|
| **OAuth**       | 你使用的是云端产品（`dev.azure.com`），你的组织不禁止 OAuth，并且你希望内联的 MFA 提示。  |
| **PAT**         | 你使用的是 Azure DevOps Server（本地部署），你的组织策略强制要求使用 PAT，或者你遇到了 OAuth 处理程序问题。|

OAuth 令牌会自动刷新；PAT 会在你创建时设定的日期到期。PAT 在设计上会绕过 MFA——生成一个 PAT 要求用户已经完成身份验证，但令牌本身不会再次提示。

## 我的代码会被发送到 Azure DevOps 以外的任何地方吗？

除非你已明确启用 AI 功能并配置了提供程序，否则不会。完整的按功能数据流请参阅[隐私与数据](Privacy-and-Data-zh.md)。

如果 AI 已禁用（总开关关闭），则该插件除了你的 Azure DevOps 组织之外不会发出任何出站调用。

## 我如何在不进行任何 AI 调用的情况下使用该插件？

取消勾选 <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path> 顶部的 **Enable AI assistance**。所有 AI 功能都会从菜单和工具栏中消失，并且不会进行任何 AI 调用。

你也可以保持 AI 开启，并将每项功能路由到本地的 **Ollama** 实例，以实现完全在设备上进行的推理。

## 我在哪里查看 PR 指标？

[统计](Statistics-zh.md)选项卡显示 KPI 和图表——合并耗时、审查速度、投票分布等等——这些都是根据缓存数据在本地计算的。它是一个只读仪表板；如需可导出的、组织范围的报告，请使用 Azure DevOps Analytics。

## 内存和 CPU 占用是多少？

该插件是构建在 IDE 捆绑的 `collaboration-tools` 工具包（与 GitHub 插件使用的工具包相同）之上的一个轻量级 Swing UI。在空闲时，它会在 IDE 基线之上增加约 30-60 MB 的堆内存。活动同步——获取 PR 列表、评论和差异——会再增加几 MB。

对于超大型组织（跨多个仓库有 1000+ 个 PR），PR 列表会虚拟化——只有可见的行才持有 UI 组件。

## 该插件会匿名上传任何内容吗？遥测？

不会。发行版本不收集遥测数据、崩溃报告或使用情况分析。唯一的出站调用是发往你的 Azure DevOps 组织，以及（如果启用了 AI）你配置的 AI 提供程序。请参阅[隐私与数据](Privacy-and-Data-zh.md)。

## 它支持 Azure Repos Wiki 吗？

不支持。该插件的范围限定于拉取请求。如需编辑 wiki，请使用 Azure DevOps 的 Web UI。
