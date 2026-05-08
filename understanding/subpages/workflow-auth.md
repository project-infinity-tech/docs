---
title: "Workflow Auth"
description: "Controlling who can trigger workflows in Scram."
---

Workflow authorisation controls who can trigger a workflow — restricting certain actions to logged-in users or specific roles.

Workflows inherit their authorisation settings from the page they're on by default. You can then override this per workflow. Authorisation cannot be set at the individual step level.

For page-level authorisation settings, see [Page Authorisation](/understanding/subpages/page-authorisation).

---

## Two levels of protection

**Requires login** — the workflow will only run if the user is signed in. If they're not, it won't execute.

**Requires a specific role** — on top of login, you can restrict the workflow to users with a particular role. For example, only users with the "Admin" role can trigger a delete action.

<Warning>
  If you enable role-based protection, you must select at least one role. Leaving roles empty while requiring authentication will block everyone from triggering the workflow — including admins.
</Warning>

---

## Where it applies

Workflow authorisation applies across all workflow types:

- **Button and event workflows** — e.g. only an Admin can click "Delete" and have it do anything
- **Page data workflows** — controls who can load data when a page opens
- **API endpoints** — controls which external calls are accepted

---

## How roles get assigned

Users sign up with no roles by default. Your signup workflow must explicitly assign a role — such as "Registered User" — immediately after signup. Without this, users will be locked out of any role-protected workflow.

<Note>
  Role IDs, not display names, are used when assigning or checking roles in workflows and expressions. You can find role IDs in the [Users](/resources/users) section of the Resource View.
</Note>