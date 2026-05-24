# Privacy and Data

What leaves your machine when you use %product%, where it goes, and how to keep everything local.

## Credentials

| Credential               | Where it's stored                                                                                                   |
|--------------------------|---------------------------------------------------------------------------------------------------------------------|
| Azure DevOps PAT         | IDE's `PasswordSafe` → system keychain (macOS Keychain, Windows Credential Manager, GNOME Keyring / KWallet).       |
| OAuth refresh tokens     | Same — `PasswordSafe`. Plaintext on disk is never used.                                                             |
| AI provider API keys     | Same — `PasswordSafe`, keyed per provider instance.                                                                 |

See [Authentication](Authentication.md) for the per-OS keychain details and how to rotate or revoke a PAT.

## What's sent to Azure DevOps

The plugin is a thin client over the Azure DevOps REST API. Every call goes directly to the org you configured (`dev.azure.com/<org>` or your on-prem Azure DevOps Server). Nothing is routed through third-party servers.

Calls are made when:

- You open the PR tool window (initial list fetch).
- The 60-second background sync ticks.
- You open a PR (timeline + diff fetches).
- You post a comment, vote, mark viewed, complete, or abandon.
- You generate the `git fetch` / `git push` credential handoff for an Azure DevOps remote.

## What's sent to AI providers

Only when AI is **enabled** and a provider is configured. The plugin makes outbound calls only for the action you triggered.

### Per-feature data flow

| Feature                | What the provider sees                                                                                          |
|------------------------|-----------------------------------------------------------------------------------------------------------------|
| **Summarize PR**       | PR title + description + the diff (truncated to **Max diff size**, default 200 KB).                             |
| **AI review pass**     | The full per-file diff for each changed file. Files larger than **Max diff size** are skipped.                  |
| **Explain code**       | The selected file's contents (the whole file, not just the visible range).                                      |
| **Commit message**     | Your staged diff (whatever `git diff --cached` would produce).                                                  |
| **Title & description**| Branch name + commit messages + diff (truncated as above).                                                      |

Each AI request also carries the system prompt the plugin builds for that feature. You can override these prompts in <ui-path>Settings | Version Control | Azure DevOps | AI Settings | Configure Prompts</ui-path>.

### Provider data-flow matrix

| Provider                 | Where requests go                                                                                                                              |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **Claude (Anthropic)**   | `api.anthropic.com` (or your custom base URL).                                                                                                 |
| **OpenAI**               | `api.openai.com` by default, or whatever base URL you configure (Azure OpenAI, vLLM, self-hosted).                                             |
| **Gemini (Google)**      | Google's AI Studio / Vertex AI endpoints.                                                                                                      |
| **Ollama**               | The endpoint you set, typically `http://localhost:11434`. **No network egress** when this is a localhost address.                              |
| **Claude Code CLI**      | The `claude` binary handles auth and routing — data flow is controlled by Anthropic's CLI terms.                                               |
| **OpenAI Codex CLI**     | The `codex` binary's auth and routing.                                                                                                         |
| **GitHub Copilot CLI**   | The `copilot` binary uses your Copilot subscription — data flow is governed by GitHub Copilot's terms.                                         |

The plugin does not add headers, telemetry, or analytics on top of these requests. Whatever the upstream provider sees is exactly what the plugin sent.

## Caching AI responses

When a feature returns a result, the plugin caches it keyed by:

- The PR ID.
- The diff SHA at the time of the request.
- A monotonic `cacheGeneration` counter — bumped when you edit a prompt, change a provider, or click **Clear cached AI responses** in the summary card's gear popup.

A cache hit returns instantly with no outbound call. Cached responses live in IDE-local state and are cleared on plugin uninstall.

## Telemetry

The shipping version of the plugin **does not collect telemetry**. There are no usage analytics, crash reports, or "phone home" pings beyond the API calls listed above (to your Azure DevOps org and your chosen AI provider).

If a future version adds opt-in telemetry, it will be off by default and called out in the release notes.

## Keeping everything local

For organizations with data-residency requirements:

1. **Use on-prem Azure DevOps Server** (formerly TFS). PRs, comments, and the API all live on your own server.
2. **Disable AI** with the master switch, or **route every AI feature at an Ollama instance** running on `localhost`. Combine with an offline-capable model (Llama, Mistral, etc.) and no data leaves your machine.
3. **Avoid CLI AI providers** if you don't want to inherit a third-party CLI's terms — they're convenient but their data flow is opaque to the plugin.

## Custom AI providers (enterprise)

%product% exposes extension points so an enterprise's internal plugin can replace the built-in AI implementations and route AI calls through, say, an internal gateway. The extension points are declared in `plugin.xml` under the namespace `intellij.vcs.azuredevops` — refer to the plugin's GitHub repository for implementation details.

If a higher-priority extension is registered, the plugin's built-in default is bypassed for that feature.
