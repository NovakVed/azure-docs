# AI Features

Optional AI helpers: PR summaries, full-diff reviews, code explanations, commit messages, PR title/description drafts, and grammar polish. **Bring your own provider** — OpenAI, Claude, Gemini, Ollama, or GitHub Copilot — and route each feature wherever you like.

> Everything here is **off until you turn it on**. For exactly what's sent to a provider, see [Privacy and Data](Privacy-and-Data.md).
> {style="note"}

## What the plugin can do with AI

| Feature | What it does | Where |
|---------|--------------|-------|
| **Summarize Pull Request** | Drafts a summary of the diff you can drop into the description. | Timeline card / overflow menu |
| **Run AI Review** | Walks the diff and proposes inline review comments. | Diff toolbar / changes-tree menu / overflow |
| **Explain This File** | Streams a plain-English explanation of a file or selection. | Right-click in the diff |
| **Generate Commit Message with AI** | Drafts a commit message from your staged changes. | Commit tool window |
| **Title + Description** | Pre-fills the Create-PR form from your branch's diff. | Create Pull Request form |
| **Polish grammar &amp; spelling with AI** | Cleans up any comment or description in place. | Every comment editor |

![The AI summary card on a PR timeline](ai-summary-card.png){ width="700" border-effect="line" }

> **Run AI Review** proposes suggestions for you to accept, edit, or dismiss — **nothing is posted to Azure DevOps until you act**. A failed run surfaces a balloon with a one-click **Open AI Settings** jump.
> {style="tip"}

## Configure providers

Open <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path> and turn on **Enable AI assistance** (the master switch). Then add providers in the **AI Providers** table.

![The AI Settings page: providers and per-feature routing](ai-settings.png){ width="720" border-effect="line" }

Each row is one provider instance with a **Provider**, **Model**, and **Enabled** column; the first enabled row is the default. The **Add AI Provider** dialog offers five families:

| Family | Notes |
|--------|-------|
| **OpenAI** | GPT models. Works with any OpenAI-compatible base URL (Azure OpenAI, vLLM, …). |
| **Claude** | Anthropic Claude models. |
| **Gemini** | Google Gemini models. |
| **Ollama** | Local models — free, no key. |
| **GitHub Copilot** | Uses your Copilot subscription (CLI only). |

Most families run in one of two **modes**:

- **HTTP API (use an API key)** — paste a key; optionally set an **API URL** to point at a custom endpoint. Keys are stored in the IDE keychain (PasswordSafe).
- **CLI (use the local command-line tool)** — no key; the local binary handles its own auth. The lowest-friction path, but you take on the CLI vendor's terms.

Use **Test Connection** in the dialog to confirm a provider works before saving.

## Route features to providers

The **Per-Feature Provider** panel pins each feature to a specific instance — handy for sending cheap features to a small model and heavy reviews to a smart one:

```
AI Summary          → [Default ▾]
AI Review           → [Default ▾]
Title + Description → [Default ▾]   (also used by Generate Commit Message)
Explain Code        → [Default ▾]
```

Leave a row on **Default** to use the first enabled provider. You can add the **same family more than once** (e.g. two OpenAI rows, a cheap model and a smart one) and route to each independently.

### Configure Prompts

The **Configure Prompts** panel lets you edit the system prompt behind each feature. Editing a prompt invalidates cached responses for it.

## Caching, cost, and limits

AI responses are cached **per PR + per commit SHA** (toggle: **Cache AI responses per commit SHA**, on by default). A cache hit returns instantly with no API call; a new commit or an edited prompt invalidates it. Force a refresh with **Clear AI Response Cache** in **Advanced**.

You pay your provider's bill for the tokens you use. To keep usage down:

- Route cheap features (commit message, title) to a small model via per-feature routing.
- Lower **Max diff size** in **Advanced** to truncate big diffs before they're sent.
- Keep the cache on so re-opening a PR doesn't re-bill you.

> Provider quota and usage-limit errors come straight from the provider — the plugin classifies them and shows clear, actionable wording rather than failing silently. It doesn't add its own rate limits or retries.
> {style="note"}

## Keep everything local, or off

- **Local inference:** route every feature at an **Ollama** instance on `localhost` — no code leaves your machine.
- **Off entirely:** uncheck **Enable AI assistance**. Every AI affordance disappears from menus and toolbars, and the plugin makes zero outbound AI calls.
