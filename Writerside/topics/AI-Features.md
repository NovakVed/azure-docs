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

> **Run AI Review** proposes inline suggestions in the diff. Each one offers **Add to review** — which drops the AI's text into a new-comment editor on that line so you can edit it and queue it as a draft — or **Discard**, which hides it. **Nothing is posted to Azure DevOps until you submit your pending comments.** A failed run surfaces a balloon with a one-click **Open AI Settings** jump.
> {style="tip"}

### Tune the summary

The **Summary settings** gear in the top-right corner of the **AI summary** card opens a popup that controls how the summary is generated:

| Control | Options |
|---------|---------|
| **Generate automatically on open** | Checkbox — off by default. When on, the card drafts a summary as soon as the PR opens. |
| **Verbosity** | Slider: **Brief** · **Neutral** · **Verbose**. |
| **Formality tone** | Slider: **Informal** · **Neutral** · **Formal**. |
| **Personality** | Free-text — an optional persona, e.g. "a slightly sarcastic principal engineer". |
| **Customization prompt** | Free-text — leave blank to use the default. It's the same override as **Configure Prompts → Pull Request summary** in AI Settings, so edits in either surface stay in sync. |

There's no Save button — edit the controls and dismiss the popup to apply.

![The Summary settings popup off the AI summary card's gear](ai-summary-settings-popup.png){ width="520" border-effect="line" }

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

> The **Model** dropdown in the Add/Edit dialog populates itself: it shows a bundled suggested list instantly, then refreshes from a live query to the provider (for example OpenAI and Claude's `/v1/models`) so newly-shipped models appear without a plugin update. The live list is cached for about 30 minutes; it refreshes on every dialog open and whenever you change the family or mode, so there's no manual refresh button. Discovery needs a saved key — until one is entered the dropdown falls back to the suggested list. The field stays editable, so you can always type a model id by hand.
> {style="note"}

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
