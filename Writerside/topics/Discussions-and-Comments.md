# Discussions & Comments

Have full-featured conversations in pull requests without leaving the IDE: markdown editor, @mentions with autocomplete, image attachments, suggested edits, and thread resolution.

## Where threads appear

Comment threads show up in three places:

- **Inline in the diff** — anchored beneath the line of code they reference. See [Code Review](Code-Review.md).
- **Discussion tab** — a chronological timeline of every thread and PR event.
- **In the editor** — overlaid on your normal editor when the PR's source branch is checked out. See [Review in Editor](Review-in-Editor.md).

## Comment editor

The comment editor uses Markdown. It includes a formatting toolbar with these actions:

| Button             | Output                                       |
|--------------------|----------------------------------------------|
| Bold               | `**text**`                                   |
| Italic             | `_text_`                                     |
| Strikethrough      | `~~text~~`                                   |
| Inline code        | `` `text` ``                                 |
| Code block         | Triple-backtick block with language picker   |
| Bulleted list      | `- item`                                     |
| Numbered list      | `1. item`                                    |
| Quote              | `> text`                                     |
| Link               | `[label](https://…)`                         |
| Image / attachment | Opens file picker, uploads, inserts markdown reference |

Keyboard shortcuts inside the editor: <shortcut>⌘B</shortcut> bold, <shortcut>⌘I</shortcut> italic, <shortcut>⌘K</shortcut> insert link, <shortcut>⌘↵</shortcut> submit comment (or <shortcut>Ctrl</shortcut> equivalents on Windows/Linux).

## @mentions

Type `@` to open an autocomplete dropdown of people in your Azure DevOps organization. The dropdown shows avatars and display names, scored by best match.

- Use arrow keys to navigate, <shortcut>Enter</shortcut> to insert.
- Mentioned users receive an Azure DevOps notification.
- **Team mentions** (`@teamname`) resolve when the org exposes the team via the Identity API — Azure DevOps treats them as a group notification.

> @-mention autocomplete requires the **Identity (Read)** scope on your PAT, or the equivalent OAuth scope. See [Authentication](Authentication.md).
> {style="note"}

## Images and attachments

Attach screenshots or files to a comment:

- **Drag & drop** a file onto the editor — it uploads and inserts a markdown reference.
- **Paste** an image directly from your clipboard.
- **Click** the attachment button in the toolbar to open a file picker.

Attachments are uploaded to Azure DevOps as PR attachments and referenced via signed URLs. Preview thumbnails render inline; click them to view full-size.

## Suggested edits

To suggest a concrete code change rather than describe it in prose, use a **suggestion block**. From the toolbar, click **Insert suggestion**, or type:

````markdown
```suggestion
const result = computeValue(input)
```
````

The PR author sees an **Apply suggestion** button on the thread, which commits the change directly. Suggestion blocks can include multiple lines and are anchored to the same range as the parent comment.

## Replying to a thread

Click **Reply** on any thread to add a follow-up comment. Azure DevOps threads are flat — replies belong to the thread, not to a specific comment within it. Your reply appears below the last comment in the thread chronologically.

## Resolve and unresolve

When a thread's discussion is done, click **Resolve**. Resolved threads are visually de-emphasized and hidden by default when the thread filter is set to **Unresolved only**.

Resolved threads can be unresolved at any time by clicking **Unresolve** — useful if the change wasn't actually applied or the reviewer wants more discussion.

## Edit or delete your comments

Click the **⋯** menu on a comment you authored:

- **Edit** — opens the editor inline with your original markdown.
- **Delete** — removes the comment. The deletion is permanent.
- **Copy link** — copies a deep link to the comment in the Azure DevOps web UI.

## Per-thread status

In addition to resolved/unresolved, threads have an Azure DevOps status. The plugin exposes the user-settable subset as a chip next to the thread title — click the chip to open a popup and switch between them:

| Status         | Settable | When to use                                                                   |
|----------------|----------|-------------------------------------------------------------------------------|
| **Active**     | ✓ (default) | A new thread. No chip is rendered for the default state.                    |
| **Pending**    | ✓        | Author is working on the change; awaiting their reply.                        |
| **Resolved**   | ✓        | Change applied; matches the standard Resolve action.                          |
| **Won't fix**  | ✓        | Reviewer acknowledges the comment but the change isn't going in.              |
| **Closed**     | ✓        | Discussion is done — no action will be taken.                                 |
| **Unknown** / **By design** | — | Read-only states that may arrive from older Azure DevOps clients. The plugin doesn't expose a setter for these. |

## Timeline events

The **Discussion** tab also shows system events alongside comments:

- Vote changes (Approve, Reject, Wait for author, …)
- Reviewer added / removed
- Work item linked / unlinked
- Status check completed
- Force pushes (with link to compare commits)
