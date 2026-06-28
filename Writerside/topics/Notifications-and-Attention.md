# Notifications & Attention

The plugin watches for pull requests that need *you* — ones awaiting your review or where someone @mentioned you — and surfaces them three ways: **balloons**, the **tool-window badge**, and **row chips**. It uses data it already polls, so there are no extra network calls.

## Notification balloons

When something needs your attention, a balloon appears in the lower-right with a one-click action:

![A notification balloon for a PR that needs you](attention-balloon.png){ width="420" border-effect="line" }

You can be notified about:

- A PR where you're **asked to review**.
- A comment that **@mentions you**.
- A **reply** in a thread you took part in.
- A **reviewer vote change** on a PR you authored.
- A chance to **Create a PR** right after you push a branch.

A single event opens straight to the PR — **Open pull request** for a review request or vote change, **View comment** for a mention or reply (it lands on the exact comment). Several at once coalesce into one balloon (*"N pull requests need your review"*) whose **Show pull requests** action opens the tool window. Balloons dismiss themselves once you act or after a moment — there's no button to click to clear them.

## The tool-window badge

The **Pull Requests** stripe icon shows a badge dot while something awaits your review, so you notice without the window open. (The dot recolors to stay visible when the stripe button is selected.)

## Attention chips on rows

Turn on **attention chips** to see *why* a PR wants you, right in the list:

![Attention chips on pull-request rows](attention-row-chips.png){ width="640" border-effect="line" }

| Chip | Meaning |
|------|---------|
| **Review requested** | You're a reviewer who hasn't voted yet. |
| **Mentions you** | A comment @mentions you. |
| **Replied** | New activity in a thread you took part in. |

Chips are **off by default**. Turn them on with **Show attention markers on pull-request rows** in [Settings](Settings.md). Hover a chip for the *"Why this pull request wants your attention"* tooltip.

> **Unread markers** are separate: a blue dot marks PRs with new commits *or* new comment activity, and clears the moment you open the PR. Toggle it from the tool-window gear → **Show unread markers**.
> {style="note"}

## Tune what you're notified about

Open <ui-path>Settings | Version Control | Azure DevOps</ui-path> → **Polling &amp; notifications**:

| Setting | Default |
|---------|---------|
| **Notify when I'm asked to review a pull request** | On |
| **Notify when someone @mentions me in a pull request** | On |
| **Notify on replies in threads I participated in** | On |
| **Notify when reviewer votes change on my PRs** | On |
| **Offer Create PR after I push to an Azure DevOps remote** | On |
| **Include my own pull requests and @mentions** | Off |

> **Testing solo?** Turn on **Include my own pull requests and @mentions** to see attention signals from your own activity — handy when you're the only one in the repo.
> {style="tip"}

You can also route the plugin's notification groups (popup / tool window / log-only) in <ui-path>Settings | Appearance &amp; Behavior | Notifications</ui-path> — see [Settings](Settings.md#notifications).
