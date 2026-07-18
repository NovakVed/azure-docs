# 隐私与数据

使用 %product% 时哪些数据会离开你的机器、去往何处，以及如何将一切保持在本地。

## 凭据

| 凭据                    | 存储位置                                                                                                          |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|
| Azure DevOps PAT         | IDE 的 `PasswordSafe` → 系统钥匙串（macOS Keychain、Windows Credential Manager、GNOME Keyring / KWallet）。       |
| OAuth 刷新令牌           | 同上——`PasswordSafe`。绝不会在磁盘上使用明文。                                                                   |
| AI 提供商 API 密钥       | 同上——`PasswordSafe`，按每个提供商实例分别存储。                                                                 |

有关各操作系统的钥匙串细节以及如何轮换或吊销 PAT，请参阅 [身份验证](Authentication-zh.md)。

## 发送到 Azure DevOps 的内容

本插件是 Azure DevOps REST API 之上的一个轻量客户端。每次调用都直接发往你配置的组织（`dev.azure.com/<org>` 或你的本地部署 Azure DevOps Server）。任何内容都不会经过第三方服务器中转。

在以下情况下会发起调用：

- 你打开 PR 工具窗口时（首次列表获取）。
- 60 秒后台同步触发时。
- 你打开某个拉取请求时（时间线 + 差异获取）。
- 你发表评论、投票、标记为已查看、完成或放弃时。
- 你为某个 Azure DevOps 远程仓库生成 `git fetch` / `git push` 凭据移交时。

## 发送到 AI 提供商的内容 {id="whats-sent-to-ai-providers"}

仅当 AI 处于**启用**状态且已配置某个提供商时才会发送。插件仅针对你触发的操作发起出站调用。

> 当你添加或编辑 AI 提供商时，插件会使用其 API 密钥向该提供商发起一次经过身份验证的**模型列表**请求（例如 `GET /v1/models`），用于填充模型下拉列表。这是唯一在配置阶段而非你触发的操作时发起的 AI 请求。不会发送任何 PR 代码、差异或提示词——只发送模型列表调用——并且结果会缓存约 30 分钟。本地提供商（位于 localhost 地址的 Ollama）会将其保留在你的机器上。
> {style="note"}

### 各功能的数据流

| 功能                    | 提供商所看到的内容                                                                                              |
|------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Summarize PR**       | PR 标题 + 描述 + 差异（截断至 **Max diff size**，默认 200 KB）。                                                |
| **AI review pass**     | 每个已更改文件的完整逐文件差异。大于 **Max diff size** 的文件会被跳过。                                          |
| **Explain code**       | 所选文件的内容（整个文件，而不仅是可见范围）。                                                                  |
| **Commit message**     | 你的暂存差异（即 `git diff --cached` 会产生的内容）。                                                            |
| **Title & description**| 分支名 + 提交消息 + 差异（按上文所述截断）。                                                                    |

每个 AI 请求还会附带插件为该功能构建的系统提示词。你可以在 <ui-path>Settings | Version Control | Azure DevOps | AI Settings | Configure Prompts</ui-path> 中覆盖这些提示词。

### 提供商数据流矩阵

| 提供商                   | 请求去往何处                                                                                                                                   |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **Claude (Anthropic)**   | `api.anthropic.com`（或你自定义的基础 URL）。                                                                                                  |
| **OpenAI**               | 默认为 `api.openai.com`，或你配置的任何基础 URL（Azure OpenAI、vLLM、自托管）。                                                                |
| **Gemini (Google)**      | Google 的 AI Studio / Vertex AI 端点。                                                                                                         |
| **Ollama**               | 你设置的端点，通常是 `http://localhost:11434`。当它是 localhost 地址时**没有网络出口流量**。                                                    |
| **Claude Code CLI**      | `claude` 二进制程序负责身份验证与路由——数据流由 Anthropic 的 CLI 条款控制。                                                                    |
| **OpenAI Codex CLI**     | `codex` 二进制程序的身份验证与路由。                                                                                                           |
| **GitHub Copilot CLI**   | `copilot` 二进制程序使用你的 Copilot 订阅——数据流受 GitHub Copilot 的条款约束。                                                                |

插件不会在这些请求之上添加任何标头、遥测或分析数据。上游提供商所看到的内容，正是插件所发送的内容。

## 缓存 AI 响应 {id="caching-ai-responses"}

当某个功能返回结果时，插件会以下列内容为键进行缓存：

- PR ID。
- 请求发起时的差异 SHA。
- 一个单调递增的 `cacheGeneration` 计数器——当你编辑提示词、更换提供商，或在摘要卡片的齿轮弹出菜单中点击 **Clear cached AI responses** 时递增。

缓存命中会立即返回，不发起任何出站调用。缓存的响应存于 IDE 本地状态中，并在卸载插件时清除。

## 遥测

发布版本的插件**不收集遥测数据**。除了上文列出的 API 调用（发往你的 Azure DevOps 组织和你选择的 AI 提供商）之外，没有任何使用分析、崩溃报告或“回传”ping。

如果未来版本添加了选择加入的遥测功能，它将默认关闭，并会在发行说明中特别指出。

## 将一切保持在本地

对于有数据驻留要求的组织：

1. **使用本地部署的 Azure DevOps Server**（前身为 TFS）。PR、评论和 API 全部位于你自己的服务器上。
2. **用主开关禁用 AI**，或**将每一项 AI 功能都路由到运行在 `localhost` 上的 Ollama 实例**。再搭配一个可离线运行的模型（Llama、Mistral 等），就不会有任何数据离开你的机器。
3. 如果你不想承接第三方 CLI 的条款，请**避免使用 CLI 类 AI 提供商**——它们虽然方便，但其数据流对插件而言是不透明的。

## 自定义 AI 提供商（企业版） {id="custom-ai-providers-enterprise"}

%product% 提供了扩展点，使企业内部插件能够替换内置的 AI 实现，并将 AI 调用路由到（比如）内部网关。这些扩展点在 `plugin.xml` 中以命名空间 `intellij.vcs.azuredevops` 声明——实现细节请参阅插件的 GitHub 仓库。

如果注册了优先级更高的扩展，则该功能的插件内置默认实现会被绕过。
