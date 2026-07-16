# Installation

Install %product% in any JetBrains IDE running build %min_ide_build% or newer.

> **TL;DR** - In <ui-path>Settings | Plugins | Marketplace</ui-path>, search **Azure DevOps Pull Requests**, click **Install**, and restart. Then open a project with an Azure DevOps remote and [sign in](Authentication.md).
> {style="tip"}

## Supported IDEs

The plugin targets the IntelliJ Platform and runs on any IDE built on it:

- IntelliJ IDEA (Ultimate &amp; Community)
- JetBrains Rider
- PyCharm (Professional &amp; Community)
- WebStorm, PhpStorm, GoLand, RubyMine, CLion, DataGrip, RustRover
- Android Studio (may work; not officially supported)

### Minimum build

The plugin requires IDE build `%min_ide_build%.*` or later - the **%min_ide_version%** release of every JetBrains IDE - because it uses platform APIs introduced then.

> **Check your version:** open **About** from the IDE menu and look for a build number starting with `%min_ide_build%`. If it's lower, run **Help → Check for Updates** first.
> {style="note"}

## Install from the Marketplace

<procedure title="Install the plugin">
    <step>Open <ui-path>Settings | Plugins | Marketplace</ui-path> (<shortcut>⌘,</shortcut> on macOS, <shortcut>Ctrl+Alt+S</shortcut> on Windows/Linux).</step>
    <step>Search for <b>Azure DevOps Pull Requests</b>.</step>
    <step>Click <b>Install</b>.</step>
    <step>Restart the IDE when prompted.</step>
</procedure>

![Installing from the JetBrains Marketplace](marketplace-install.png){ width="700" border-effect="line" }

### Verify it worked

Open a project that has an Azure DevOps Git remote, then check:

- The **Pull Requests** stripe icon appears in the left tool-window bar.
- <ui-path>Settings | Version Control | Azure DevOps</ui-path> exists.

> **Don't see the tool window?** It's hidden when the project has **no Azure DevOps remote**. Run `git remote -v` and confirm a URL contains `dev.azure.com` or `visualstudio.com`. See [Troubleshooting](Troubleshooting.md).
> {style="note"}

## Install from disk

For a pre-release `.zip` build:

<procedure title="Install from disk">
    <step>Open <ui-path>Settings | Plugins</ui-path>.</step>
    <step>Click the gear icon → <b>Install Plugin from Disk…</b></step>
    <step>Select the <code>.zip</code> and restart.</step>
</procedure>

## System requirements

| Component | Minimum | Notes |
|-----------|---------|-------|
| IDE build | %min_ide_build%.* | JetBrains %min_ide_version% or newer |
| JDK | 21 | Bundled with the IDE |
| Git | 2.20+ | Branch detection and HTTPS auth handoff |
| OS | macOS / Windows / Linux | Any platform the IDE supports |
| Network | HTTPS to Azure DevOps | `dev.azure.com` or your self-hosted server |

> **Behind a proxy?** The plugin uses the IDE's own HTTP proxy. Set it once at <ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path> and both Azure DevOps and (HTTP) AI calls inherit it. CLI-based AI providers are external binaries and don't route through it.
> {style="note"}

## Required bundled plugins

The plugin **depends on** two IDE-bundled plugins (enabled by default everywhere). If either is disabled, the plugin won't load - re-enable them in <ui-path>Settings | Plugins | Installed</ui-path>:

- **Git** (`Git4Idea`) - branch detection and HTTPS credentials.
- **Markdown** - powers the comment and description editors.

## Update and uninstall

Updates show up in <ui-path>Settings | Plugins | Installed</ui-path> - click **Update** when one is offered, then **restart the IDE** so the new version loads fully. To uninstall, use the gear icon → **Uninstall**; your stored credentials are removed from the keychain too.

> **Restart after installing or updating.** The plugin registers a couple of start-up hooks (for example, the tool-window activation shortcuts), so it isn't hot-reloaded in place - a full IDE restart makes sure everything is wired up.
> {style="note"}

> **Next up:** [Quick Start](Quick-Start.md) for a one-minute tour, or [Authentication](Authentication.md) to sign in. To enable summaries and AI review, see [AI Features](AI-Features.md).
> {style="tip"}
