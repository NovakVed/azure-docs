# Permissions

What %product% can show depends on what your credentials are allowed to read. Here's the whole map - one permission you can't skip, five that quietly unlock extras.

> **Quick recipe:** pick **Full access** when creating a PAT, or the **Full access** tier when signing in with Microsoft - everything below just works.
> {style="tip"}

## The one you can't skip

**Code (Read &amp; write)** is the plugin's foundation - listing pull requests, reading diffs, commenting, voting, completing. A token without it can't do anything useful, so the login dialog refuses it on the spot with a message telling you which scope to add. You'll never end up signed in to an empty, broken tool window.

## Everything else is optional

Each of these enriches the experience; missing ones simply switch their feature off - no errors, no broken panels.

| Permission (PAT scope)          | Unlocks                                                                                                    | Without it                                                                                       |
|---------------------------------|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Code → Status**               | The **Checks** panel - build/policy results on a PR.                                                        | Checks can't load; the rest of the PR view is unaffected.                                        |
| **User Profile → Read**         | Real profile photos everywhere.                                                                             | Avatars render as initials.                                                                       |
| **Identity → Read**             | @-mention autocomplete, resolving mentions to names, and the team-membership lookup behind the default view. | Mention search returns nothing; team-assigned PRs may disappear from the default list.            |
| **Project and Team → Read**     | Team memberships for the **assigned to my team** part of the default PR list.                               | The plugin falls back to Identity → Read for the same information.                                |
| **Work Items → Read**           | Linked work items on PR details and the Work Items filter.                                                  | The work-items section stays empty.                                                               |
| **Security → Manage**           | The **Override branch policies** option in the Complete dialog.                                             | The option is hidden.                                                                             |

## How missing permissions behave

- **Required permission missing** - sign-in is blocked, with the exact scope named in the login dialog.
- **Optional permission missing** - the feature degrades quietly (initials instead of photos, empty sections) and everything else keeps working.
- **Team-assigned PRs unavailable** - because this changes what the default PR list shows, you get a one-time notification explaining which permission to add. See [Pull Requests](Pull-Requests.md) for how the default "mine" view works.

## Fixing a missing permission

Permissions are baked into the token at creation - they can't be added to an existing one from the plugin.

<procedure title="Re-authenticate with more permissions">
    <step><b>PAT:</b> create a new token with the missing scope granted, then <ui-path>Settings | Version Control | Azure DevOps</ui-path> → pencil icon → paste it.</step>
    <step><b>Microsoft (OAuth):</b> remove the account and sign in again, choosing <b>Full access</b> in the permission picker.</step>
</procedure>

See [Authentication](Authentication.md) for the full sign-in walkthrough.
