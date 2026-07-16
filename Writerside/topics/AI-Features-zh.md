# AI 功能

可选的 AI 助手：PR 摘要、完整差异审查、代码解释、提交消息、PR 标题/描述草稿以及语法润色。**自带服务商** - OpenAI、Claude、Gemini、Ollama 或 GitHub Copilot - 并可将每项功能路由到你喜欢的任意服务商。

> 这里的所有功能**在你开启之前都是关闭的**。关于具体发送给服务商的内容，请参阅[隐私与数据](Privacy-and-Data-zh.md)。
> {style="note"}

## 插件能用 AI 做什么

| 功能 | 作用 | 位置 |
|---------|--------------|-------|
| **Summarize Pull Request** | 起草一份差异摘要，可直接放入描述中。 | 时间线卡片 / 溢出菜单 |
| **Run AI Review** | 遍历差异并提出内联审查评论。 | 差异工具栏 / 变更树菜单 / 溢出菜单 |
| **Explain This File** | 流式输出对某个文件或选区的通俗英文解释。 | 在差异中右键单击 |
| **Generate Commit Message with AI** | 根据你暂存的更改起草一条提交消息。 | Commit 工具窗口 |
| **Title + Description** | 根据分支的差异预填 Create-PR 表单。 | Create Pull Request 表单 |
| **Polish grammar &amp; spelling with AI** | 就地清理任意评论或描述。 | 每个评论编辑器 |

![PR 时间线上的 AI 摘要卡片](ai-summary-card.png){ width="700" border-effect="line" }

> **Run AI Review** 会在差异中提出内联建议。每条建议都提供 **Add to review** - 将 AI 的文本放入该行的新评论编辑器中，方便你编辑并将其作为草稿排队 - 或 **Discard**，将其隐藏。**在你提交待处理评论之前，不会有任何内容发布到 Azure DevOps。** 运行失败会弹出一个气泡提示，带有一键跳转的 **Open AI Settings**。
> {style="tip"}

### 调整摘要

**AI summary** 卡片右上角的 **Summary settings** 齿轮会打开一个弹窗，用于控制摘要的生成方式：

| 控件 | 选项 |
|---------|---------|
| **Generate automatically on open** | 复选框 - 默认关闭。开启后，PR 一打开卡片就会起草摘要。 |
| **Verbosity** | 滑块：**Brief** · **Neutral** · **Verbose**。 |
| **Formality tone** | 滑块：**Informal** · **Neutral** · **Formal**。 |
| **Personality** | 自由文本 - 可选的人设，例如"一位略带讽刺的首席工程师"。 |
| **Customization prompt** | 自由文本 - 留空则使用默认值。它与 AI Settings 中的 **Configure Prompts → Pull Request summary** 是同一个覆盖项，因此在任一处的编辑都会保持同步。 |

没有保存按钮 - 编辑控件后关闭弹窗即可应用。

![从 AI 摘要卡片齿轮弹出的 Summary settings 弹窗](ai-summary-settings-popup.png){ width="520" border-effect="line" }

## 配置服务商

打开 <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path> 并开启 **Enable AI assistance**（总开关）。然后在 **AI Providers** 表中添加服务商。

![AI Settings 页面：服务商与按功能路由](ai-settings.png){ width="720" border-effect="line" }

每一行代表一个服务商实例，包含 **Provider**、**Model** 和 **Enabled** 列；第一个启用的行即为默认。**Add AI Provider** 对话框提供五个系列：

| 系列 | 说明 |
|--------|-------|
| **OpenAI** | GPT 模型。可与任意兼容 OpenAI 的 base URL 配合使用（Azure OpenAI、vLLM，……）。 |
| **Claude** | Anthropic Claude 模型。 |
| **Gemini** | Google Gemini 模型。 |
| **Ollama** | 本地模型 - 免费，无需密钥。 |
| **GitHub Copilot** | 使用你的 Copilot 订阅（仅限 CLI）。 |

> Add/Edit 对话框中的 **Model** 下拉框会自动填充：它会立即显示一份内置的建议列表，然后通过对服务商的实时查询进行刷新（例如 OpenAI 和 Claude 的 `/v1/models`），这样新发布的模型无需更新插件即可出现。实时列表会缓存约 30 分钟；它会在每次打开对话框以及你更改系列或模式时刷新，所以没有手动刷新按钮。发现功能需要一个已保存的密钥 - 在输入密钥之前，下拉框会回退到建议列表。该字段始终可编辑，因此你随时可以手动输入模型 id。
> {style="note"}

大多数系列以两种**模式**之一运行：

- **HTTP API (use an API key)** - 粘贴一个密钥；可选择设置 **API URL** 以指向自定义端点。密钥存储在 IDE 密钥链（PasswordSafe）中。
- **CLI (use the local command-line tool)** - 无需密钥；本地二进制文件自行处理鉴权。这是阻力最小的路径，但你需要接受 CLI 供应商的条款。

在对话框中使用 **Test Connection** 以在保存前确认服务商可用。

## 将功能路由到服务商

**Per-Feature Provider** 面板将每项功能固定到特定实例 - 便于将廉价功能发送给小模型，而将繁重的审查发送给智能模型：

```
AI Summary          → [Default ▾]
AI Review           → [Default ▾]
Title + Description → [Default ▾]   (also used by Generate Commit Message)
Explain Code        → [Default ▾]
```

将某一行保留为 **Default** 即可使用第一个启用的服务商。你可以**多次添加同一系列**（例如两个 OpenAI 行，一个廉价模型和一个智能模型），并分别独立路由。

### Configure Prompts

**Configure Prompts** 面板让你可以编辑每项功能背后的系统提示。编辑某个提示会使其缓存的响应失效。

## 缓存、成本与限制

AI 响应按 **每个 PR + 每个提交 SHA** 缓存（开关：**Cache AI responses per commit SHA**，默认开启）。缓存命中会立即返回且不产生 API 调用；新的提交或编辑过的提示会使其失效。可通过 **Advanced** 中的 **Clear AI Response Cache** 强制刷新。

你为所使用的 token 向服务商付费。为了控制用量：

- 通过按功能路由，将廉价功能（提交消息、标题）路由到小模型。
- 在 **Advanced** 中降低 **Max diff size**，在发送前截断大型差异。
- 保持缓存开启，这样重新打开 PR 不会再次向你计费。

> 服务商配额和用量限制错误直接来自服务商 - 插件会对其分类并显示清晰、可操作的措辞，而不是无声地失败。它不会添加自己的速率限制或重试。
> {style="note"}

## 保持一切本地，或完全关闭

- **本地推理：** 将每项功能都路由到 `localhost` 上的 **Ollama** 实例 - 没有任何代码离开你的机器。
- **完全关闭：** 取消勾选 **Enable AI assistance**。所有 AI 功能都会从菜单和工具栏中消失，插件也不会发出任何对外的 AI 调用。
