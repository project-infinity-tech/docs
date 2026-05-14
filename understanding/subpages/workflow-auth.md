---
title: "Workflow Auth"
description: "Controlling who can trigger workflows in Scram."
---

Workflow authorisation controls who can trigger a workflow — restricting certain actions to logged-in users or specific roles.

Workflows inherit their authorisation settings from the page they're on by default. You can then override this per workflow. Authorisation cannot be set at the individual step level.

For page-level authorisation settings, see [Page Authorisation](/understanding/subpages/page-authorisation).

---

## How authentication works

When you enable **Authentication Required**, you must select which roles are permitted. The user must be logged in and have one of the listed roles to proceed.

By default, all roles are listed — which means any logged-in user with any role can access the workflow. You can narrow this down by removing roles from the list.

<Warning>
  Leaving the roles list empty blocks everyone — including admins. Always select at least one role when authentication is enabled.
</Warning>

<Note>
  Users sign up with no roles by default. Make sure your signup workflow assigns at least one role — otherwise newly signed-up users will be blocked from any authenticated workflow or page, even if all roles are listed.
</Note>

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