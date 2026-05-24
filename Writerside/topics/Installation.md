# Installation

Install %product% in any JetBrains IDE running build %min_ide_build% or newer.

## Supported IDEs

The plugin targets the IntelliJ Platform and runs on any IDE built on top of it:

- IntelliJ IDEA (Ultimate & Community)
- JetBrains Rider
- PyCharm (Professional & Community)
- WebStorm, PhpStorm, GoLand, RubyMine, CLion, DataGrip, RustRover
- Android Studio (untested but compatible)

### Minimum build

The plugin requires IDE build `%min_ide_build%.*` or later — this corresponds to the **%min_ide_version%** release of all JetBrains IDEs. Older builds aren't supported because the plugin uses platform APIs introduced in %min_ide_version%.

> **Check your IDE version**: open **About** from the IDE menu and look for a build number starting with `%min_ide_build%`. If it's lower, run **Help → Check for Updates** first.
> {style="note"}

## Install from JetBrains Marketplace

<procedure title="Install the plugin">
    <step>Open your IDE.</step>
    <step>Go to <ui-path>Settings | Plugins | Marketplace</ui-path> (or <shortcut>⌘,</shortcut> on macOS, <shortcut>Ctrl+Alt+S</shortcut> on Windows/Linux).</step>
    <step>Search for <b>Azure DevOps Pull Requests</b>.</step>
    <step>Click <b>Install</b>.</step>
    <step>Restart the IDE when prompted.</step>
</procedure>

After restart, you should see the **Pull Requests** tool window icon on the left toolbar of any project that has an Azure DevOps Git remote.

## Install from disk

If you have a `.zip` distribution of the plugin (for example a pre-release build):

<procedure title="Install from disk">
    <step>Open <ui-path>Settings | Plugins</ui-path>.</step>
    <step>Click the gear icon and choose <b>Install Plugin from Disk…</b></step>
    <step>Select the <code>.zip</code> file.</step>
    <step>Restart the IDE.</step>
</procedure>

## System requirements

| Component | Minimum         | Notes                                                                  |
|-----------|-----------------|------------------------------------------------------------------------|
| IDE build | %min_ide_build%.*           | JetBrains %min_ide_version% or newer                                                |
| JDK       | 21              | Bundled with the IDE — no separate install needed                      |
| Git       | 2.20+           | Required for branch detection and HTTPS auth handoff                   |
| OS        | macOS / Windows / Linux | Any platform the IDE supports                                  |
| Network   | HTTPS to Azure DevOps   | `dev.azure.com` or your self-hosted Azure DevOps Server        |

> **Behind a corporate proxy or firewall?** The plugin uses the IDE's own HTTP proxy settings — there's no separate plugin proxy. Configure it once at <ui-path>Settings | Appearance &amp; Behavior | System Settings | HTTP Proxy</ui-path> and both Azure DevOps API calls and AI provider calls inherit it.
> {style="note"}

## Bundled dependencies

The plugin depends on two IDE-bundled plugins that are already enabled by default in every JetBrains IDE:

- **Git** (`Git4Idea`) — for branch detection and HTTPS credential provider integration.
- **Markdown** — for the comment formatting toolbar in PR discussions.

If you've disabled either plugin manually, re-enable them from <ui-path>Settings | Plugins | Installed</ui-path>.

## Update the plugin

The IDE checks for plugin updates automatically. When a new version is available, you'll see a notification in the lower-right corner. To check manually:

<procedure>
    <step>Open <ui-path>Settings | Plugins | Installed</ui-path>.</step>
    <step>Find <b>Azure DevOps Pull Requests</b>.</step>
    <step>If an <b>Update</b> button appears next to it, click it.</step>
</procedure>

Updates do not require an IDE restart — the plugin uses dynamic loading.

## Uninstall

Open <ui-path>Settings | Plugins | Installed</ui-path>, find the plugin, click the gear icon, and choose **Uninstall**. Your stored credentials are removed from the IDE keychain as well.

> **Next up**: head to [Quick Start](Quick-Start.md) for a 60-second tour, or jump straight to [Authentication](Authentication.md) to sign in.
> {style="tip"}
