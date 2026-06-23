# Settings

Reference for every setting the plugin exposes. Open **Settings** with <shortcut>⌘,</shortcut> (macOS) or <shortcut>Ctrl+Alt+S</shortcut> (Windows/Linux).

## Version Control → Azure DevOps

The main page. At the top is the **accounts** panel (add **+**, edit ✏, remove ✕, per-project default) — see [Authentication](Authentication.md).

![The Azure DevOps settings page accounts panel](accounts-panel.png){ width="700" border-effect="line" }

- **Sync interval (seconds)** — how often the tool window polls Azure DevOps. **Default 60**, range **15–3600**.

### Polling & notifications

| Setting | Default |
|---------|---------|
| **Notify when I'm asked to review a pull request** | On |
| **Notify when someone @mentions me in a pull request** | On |
| **Notify on replies in threads I participated in** | On |
| **Notify when reviewer votes change on my PRs** | On |
| **Offer Create PR after I push to an Azure DevOps remote** | On |
| **Include my own pull requests and @mentions** | Off |

See [Notifications &amp; Attention](Notifications-and-Attention.md) for what these drive.

### Pull request review

| Setting | Default |
|---------|---------|
| **Mark files as viewed when their diff is opened** | Off |
| **Show attention markers on pull-request rows** | Off |

> **Show unread markers** isn't here — it's a tool-window toggle (gear menu), not a settings checkbox. Drafts are a list **filter**, not a setting.
> {style="note"}

## Version Control → Azure DevOps → AI Settings

A sub-page configuring the optional AI helpers — see [AI Features](AI-Features.md).

![The AI Settings page](ai-settings.png){ width="720" border-effect="line" }

- **General AI Settings → Enable AI assistance** — master switch. **Default off.** Off hides every AI affordance and makes zero outbound calls.
- **AI Providers** — one row per provider instance (**Provider / Model / Enabled**). The first enabled row is the default. Add via the **Add AI Provider** dialog (OpenAI, Claude, Gemini, Ollama, GitHub Copilot; HTTP-API or CLI mode).
- **Per-Feature Provider** — route **AI Summary**, **AI Review**, **Title + Description**, and **Explain Code** to specific instances, or leave them on **Default**.
- **Configure Prompts** — edit the system prompt for each feature.
- **Advanced** — **Cache AI responses per commit SHA** (default on), **Max diff size** (default 200 KB, range 10–2000), and **Clear AI Response Cache**.

## Appearance & Behavior → Notifications {id="notifications"}

The plugin registers two notification groups you can route (popup / tool window / log-only):

| Group | For |
|-------|-----|
| **Azure DevOps Pull Requests** | Review requests, @mentions, replies, vote changes, push offers. |
| **Azure DevOps AI** | AI summary / review completion balloons. |

## Keymap

Open <ui-path>Settings | Keymap</ui-path> and search **Azure DevOps** to rebind any action. The full list with action IDs is in [Keyboard Shortcuts](Keyboard-Shortcuts.md).

## Per-project vs application-level

Most settings are **application-level** (every project): accounts, notification preferences, AI providers. Two are **per-project** (stored in the project's workspace): the **default account** and your **PR-list filters**.
