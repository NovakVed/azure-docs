# AI Features

Optional AI-powered helpers: PR summaries, full-diff reviews, code explanations, commit message drafts, and PR title/description generation. Bring your own provider — Claude, OpenAI, Gemini, Ollama, or any of the supported CLIs (Claude Code, OpenAI Codex, GitHub Copilot).

> For what's sent to your provider and how the plugin handles caching and telemetry, see [Privacy and Data](Privacy-and-Data.md).
> {style="note"}

## What the plugin can do with AI

| Feature                            | What it does                                                                                                |
|------------------------------------|-------------------------------------------------------------------------------------------------------------|
| **Summarize PR**                   | Reads the diff and produces a paragraph or bulleted summary you can paste into the PR description.          |
| **AI review pass**                 | Walks the diff and posts inline review comments where it spots bugs, performance issues, or style problems. |
| **Explain code**                   | Streams a plain-English explanation of any selected file or code range.                                     |
| **Generate commit message**        | Drafts a commit message from your staged changes.                                                           |
| **Title & description generator**  | Used by the *Create PR* wizard to pre-fill title and description from commits.                              |

Internally, the first three each have their own provider slot (`SUMMARY`, `REVIEW`, `EXPLAIN`). Commit message and PR title/description share the `TITLE_DESC` slot — point them at a small, fast model.

## Supported providers

Configure at <ui-path>Settings | Version Control | Azure DevOps | AI Settings</ui-path>.

### HTTP providers (need an API key)

| Provider              | Notes                                                                       |
|-----------------------|-----------------------------------------------------------------------------|
| **Claude (Anthropic)**| Messages API. Set the model in the row (e.g. `claude-opus-4-7`).            |
| **OpenAI**            | Default endpoint, or any OpenAI-compatible base URL (Azure OpenAI, vLLM, …).|
| **Gemini (Google)**   | Google AI Studio or Vertex AI key.                                          |
| **Ollama**            | Local server. Default endpoint `http://localhost:11434`. Free, no key.      |

### CLI providers (no API key — use the binary's own auth)

If the CLI binary is on `PATH` and signed in, the plugin shells out to it — you don't paste an API key.

| Provider                  | Binary               | Auth handled by                          |
|---------------------------|----------------------|------------------------------------------|
| **Claude Code CLI**       | `claude`             | `claude /login`                          |
| **OpenAI Codex CLI**      | `codex`              | The CLI's own login flow                 |
| **GitHub Copilot CLI**    | `copilot`            | Your GitHub Copilot subscription         |

> CLI providers are the lowest-friction path: no key management, the binary handles auth. The trade-off is that you take on the CLI vendor's terms for what they do with your code. See [Privacy and Data](Privacy-and-Data.md) for the per-provider data flow.
> {style="tip"}

## Multi-instance routing

You can add the **same provider type more than once**. Each row in the providers table is one instance — useful when you want, for example, two OpenAI configurations: a small/cheap model for commit messages and a bigger one for code review.

In the providers table:

- The first **enabled** row acts as the default for any feature that has no override.
- Toggle the **Enabled** column to disable an instance without deleting it.
- Each instance has an independent API key, model, base URL, and display name.

### Per-feature provider override

The **Per-Feature Provider** panel (below the providers table) lets you pin each AI feature to a specific instance:

```
Summarize PR        → [instance ▾]
AI review           → [instance ▾]
Explain code        → [instance ▾]
Commit / Title-desc → [instance ▾]
```

Leaving an override blank falls back to the default (first enabled row). Override targets are instance IDs, not provider types — so two OpenAI rows are distinguishable.

## Use the features

### Summarize a pull request

<procedure title="Generate a PR summary">
    <step>Open a PR. The summary card sits at the top of the timeline.</step>
    <step>Click <b>Generate summary</b>. The plugin sends the diff + title + description to your provider and streams the result back.</step>
    <step>Click the gear icon on the card to customize verbosity (Brief / Neutral / Verbose), tone (Informal / Neutral / Formal), or paste a custom prompt.</step>
    <step>Use <b>Insert into description</b> to apply it to the PR (only if you have write permission).</step>
</procedure>

Summaries are cached per PR-revision. Opening a PR you've already summarized returns the cached result instantly until the head commit changes — or until you click **Clear cached AI responses** in the gear popup.

### AI review pass

In a PR's diff view, click **Run AI Review** in the toolbar. The plugin walks every changed file and asks the provider to identify issues. Each issue arrives as a **draft** inline comment that you can:

- **Add to review** — promotes the draft into a real pending review comment.
- **Edit** before adding.
- **Dismiss** if the model got it wrong.

Nothing is posted to Azure DevOps without your click.

Use **Prev / Next AI Suggestion** in the toolbar to skim only the AI's findings.

### Explain code

Right-click any file in a PR's diff → **Explain This File**. A streaming popup explains what the file does.

The same action also appears in the PR overflow menu (⋮) when AI is configured.

### Generate commit message

With files staged in the **Commit** tool window, click the AI sparkle icon next to the message field. The plugin sends the staged diff and inserts a draft message.

### PR title and description (in Create PR)

When you open <ui-path>VCS | Create Pull Request</ui-path>, an AI button appears in the toolbar of the title and description fields. Click it to pre-fill from the commits on your branch.

## Caching and clearing the cache

AI responses are cached **per PR + per diff SHA + per cache generation**:

- Same PR, same diff → cached response, no API call.
- New commit pushed → diff SHA changes → fresh call.
- Edit a prompt template or click **Clear cached AI responses** in the summary card's gear popup → the cache generation bumps and everything is invalidated.

Changing the configured provider or model also bumps the cache generation: in-flight requests complete but won't be reused.

## Latency expectations

Typical end-to-end latencies (your mileage will vary):

- **PR summary** on a 200 KB diff: 3-15s on hosted providers, 10-60s on Ollama with a 7-13B local model.
- **AI review** on the same diff: 10-30s, longer for larger diffs.
- **Explain code** on a single file: 2-10s.
- **Commit message** on small staged changes: 1-5s.

The plugin sets a 5-minute request timeout — anything longer is treated as a hang and surfaced as an error notification.

## Cost and rate limits

The plugin doesn't add its own rate limits. You pay your provider's bill for the tokens you use. To keep usage low:

- Route the cheap features (commit message, title) to a small model via per-feature override.
- Lower **Max diff size** in AI settings (10-2000 KB; default 200 KB) to truncate big diffs before they're sent.
- Keep the response cache on so re-opening a PR doesn't re-bill you.
- Disable individual features you don't use via per-feature override → blank, then disable all instances.

## Disable AI entirely

Uncheck **Enable AI assistance** at the top of AI settings. This is a master switch — every AI action is hidden from menus and toolbars, and the plugin makes zero outbound AI calls.

You can also leave AI on but route every feature at an Ollama instance for fully local inference.
