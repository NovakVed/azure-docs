# Settings

Reference for every setting the plugin exposes. Open **Settings** with <shortcut>⌘,</shortcut> (macOS) or <shortcut>Ctrl+Alt+S</shortcut> (Windows/Linux).

## Version Control → Azure DevOps

The main account management panel.

- **Accounts** — list of every signed-in Azure DevOps account. Add (**+**), remove, or edit credentials per row.
- **Default account for this project** — used when the project has remotes matching multiple accounts. Affects API calls and Git HTTPS auth handoff.
- **Background sync interval** — how often the tool window polls Azure DevOps. **Default: 60 seconds.** Set higher on slower connections.
- **Show drafts in PR list** — toggle whether draft PRs appear in the unfiltered list. **Default: on.**
- **Mark files as viewed on open** — when enabled, simply opening a file in the diff marks it as viewed. **Default: off.**

### Adding an account

Click **+**. The Add Account dialog asks for:

| Field          | Description                                                                            |
|----------------|----------------------------------------------------------------------------------------|
| **Server URL** | `https://dev.azure.com` for cloud; your server URL for Azure DevOps Server.            |
| **Organization** | Slug from the Azure DevOps URL (e.g. `my-company`).                                  |
| **Auth method** | Personal Access Token or Microsoft Entra ID (OAuth).                                  |
| **Token / Sign-in** | Paste the PAT, or launch the browser OAuth flow.                                  |

See [Authentication](Authentication.md) for required PAT scopes.

## Version Control → Azure DevOps → AI Settings

A sub-page under the main Azure DevOps settings. Configures the optional AI helpers — see [AI Features](AI-Features.md) for what each does.

- **Enable AI assistance** — master switch. **Default: off.** Off hides every AI affordance and makes zero outbound calls.
- **Max diff size** — cap the diff payload sent to AI providers, in KB. Range 10-2000, **default 200.**
- **Cache AI responses** — when on, identical requests for the same PR + diff return cached results. **Default: on.**
- **AI Providers table** — one row per provider instance. Multiple rows of the same provider are allowed (e.g. two OpenAI configs). The first **enabled** row acts as the default.
- **Per-Feature Provider** — pin each feature (Summarize / Review / Explain / Commit&nbsp;+&nbsp;Title) to a specific instance. Blank = use the default.
- **Configure Prompts** — edit the built-in system prompt for each feature slot. Editing a prompt bumps the cache generation so cached responses are invalidated.

> Switching providers mid-session bumps the cache generation: in-flight requests finish but their responses aren't cached. New requests use the new provider immediately.
> {style="note"}

## Appearance & Behavior → Notifications

The plugin registers two notification groups:

| Group                                  | What it's for                                                                         |
|----------------------------------------|---------------------------------------------------------------------------------------|
| `AzureDevOps.PullRequests`             | Toast notifications: status check results, push confirmations, refresh errors.        |
| `AzureDevOps.PullRequests.Sticky`      | Sticky balloons: added as reviewer, policy failures.                                  |

Each group has Popup / Tool window / Log-only settings; configure to taste.

## Keymap

Open <ui-path>Settings | Keymap</ui-path> and search for **Azure DevOps** to remap any of the plugin's actions. The full list with action IDs lives in [Keyboard Shortcuts](Keyboard-Shortcuts.md). Defaults:

| Action                       | macOS              | Windows / Linux                  |
|------------------------------|--------------------|----------------------------------|
| Add Review Comment           | <shortcut>⌘⇧M</shortcut>      | <shortcut>Ctrl+Shift+M</shortcut> |
| Mark File as Viewed          | <shortcut>⌘⇧S</shortcut>      | <shortcut>Ctrl+Shift+S</shortcut> |
| Refresh List / Timeline / Details | <shortcut>F5</shortcut>  | <shortcut>F5</shortcut>           |
| Open Current Branch PR       | *no default — bind it yourself* | *no default — bind it yourself* |

## Search Everywhere

Azure DevOps PRs are exposed as a Search Everywhere contributor. Configure its prominence in <ui-path>Settings | Advanced Settings | Search Everywhere</ui-path>.

## Reset to defaults

Each settings page has a **Restore Defaults** button at the bottom. Stored credentials are *not* deleted by this — use the Accounts panel to remove signed-in accounts.

## Per-project vs application-level

Most settings are **application-level** (apply to every project): accounts, AI provider, notification preferences. Two settings are **per-project**:

- **Default account** — which signed-in account is used for this project's API calls and Git HTTPS auth.
- **PR list filters** — your last-used filters in the tool window are remembered per project.
