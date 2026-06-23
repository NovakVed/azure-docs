# Discussions & Comments

Have full conversations in pull requests without leaving the IDE: a markdown editor, @mentions, work-item and PR references, suggested edits, image attachments, AI grammar polish, and thread resolution.

## Where threads appear

The same threads show up in three places:

- **Inline in the diff** — anchored to the line they reference. See [Code Review](Code-Review.md).
- **The timeline** — a chronological view of every thread and PR event. Open it from the **View Timeline** link in the PR detail view. (Use **Find in timeline** to search it.)
- **In the editor** — overlaid on your normal editor when the PR's branch is checked out. See [Review in Editor](Review-in-Editor.md).

## The comment editor

Every comment editor — timeline, diff inlay, inline edit, and the Create-PR description — shares one markdown toolbar:

![The comment editor with its formatting toolbar](comment-toolbar.png){ width="640" border-effect="line" }

| Group | Buttons |
|-------|---------|
| **References** | Mention user (`@`), Reference work item (`#`), Reference pull request (`!`) |
| **Formatting** | Heading, Bold, Italic, Inline code, Link |
| **Lists** | Bulleted, Numbered, Task list |
| **AI** | **Polish grammar &amp; spelling with AI** |

In the diff/editor inlays you also get **Insert code suggestion**. Keyboard: <shortcut>⌘B</shortcut> bold, <shortcut>⌘I</shortcut> italic, <shortcut>⌘E</shortcut> inline code, <shortcut>⌘K</shortcut> link, <shortcut>⌘↵</shortcut> submit (or <shortcut>Ctrl</shortcut> equivalents).

> **Polish grammar &amp; spelling with AI** rewrites your draft (or selection) in place as one undoable edit. It needs an [AI provider configured](AI-Features.md); when AI is off, the button is hidden.
> {style="tip"}

## @mentions

Click **Mention user** or type `@` to open an autocomplete of people in your organization. Pick one with the arrow keys and <shortcut>Enter</shortcut>; mentioned users get an Azure DevOps notification.

Click an existing `@mention` to open a small **author card** with the person's avatar and name. When their email is known (the PR author or a reviewer), the card offers **Copy email** and **Send email**.

> @-mention autocomplete needs the **Identity (Read)** scope (PAT) or **Full access** (OAuth). See [Authentication](Authentication.md).
> {style="note"}

## Images and attachments

- **Paste** an image from the clipboard (<shortcut>⌘V</shortcut> / <shortcut>Ctrl+V</shortcut>).
- **Drag &amp; drop** image files (`png`, `jpg`, `gif`, `webp`, `bmp`, `svg`).

Each upload shows an *Uploading…* placeholder, then becomes an inline markdown image. Right-click a posted image for **Copy Image Link** or **Download Image…**.

## Suggested edits

To propose a concrete change instead of describing it, use a **suggestion**. In a diff/editor inlay, click **Insert code suggestion** (it pre-fills the commented line) or type a ```` ```suggestion ```` block.

![A suggested change with the Apply Locally action](suggestion-block.png){ width="560" border-effect="line" }

The thread renders a **Suggested change** card with **Apply Locally** (and **Commit…** to apply and commit in one step). Apply is disabled until the PR branch is checked out, and on resolved threads.

## Reply, resolve, and manage threads

- **Reply** — add a follow-up. Azure DevOps threads are flat; your reply lands at the end of the thread.
- **Resolve / Reopen** — close a thread when it's done, or reopen it. Resolved threads are de-emphasized and hidden when the diff filter is set to *Show only unresolved*.
- **Edit / Delete** — on your own comments, via the hover actions in the comment header. Anyone can give a comment a **👍 (Thumbs up)**.

### Thread status

Beyond resolved/unresolved, a thread carries a status chip. Click it (**Change status**) to switch between:

| Status | Meaning |
|--------|---------|
| **Active** | A new thread (no chip shown). |
| **Pending** | Awaiting the author's change. |
| **Resolved** | Change applied. |
| **Won't fix** | Acknowledged, but the change isn't going in. |
| **Closed** | Discussion done, no action. |

## Timeline events

The timeline also shows system events alongside comments: vote changes, reviewers added/removed, work items linked/unlinked, completed status checks, and force pushes (with a link to compare commits).
