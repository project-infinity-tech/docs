---
title: "Page Authorisation"
---

Every page in your app can be protected so that only users with the right role can access it. This is controlled in the page settings by enabling **Requires Authentication**.

---

## How It Works

When you enable **Requires Authentication** on a page, you must select which roles are permitted. A user must be logged in and have one of the listed roles to view the page.

By default, all roles are listed — which means any logged-in user with any role can access the page. You can narrow this down by removing roles from the list.

<Warning>
  Leaving the roles list empty blocks everyone from accessing the page — including admins. Always select at least one role when authentication is enabled.
</Warning>

<Tip>
  Want a public landing page? Leave **Requires Authentication** turned off and anyone can visit it.
</Tip>

---

## Multiple Roles

Users can have multiple roles, and pages can allow multiple roles. A user only needs **one** of the allowed roles to access a page. This gives you a lot of flexibility — for example, both `Admin` and `Manager` roles could be permitted on the same page.

---

## Redirects

If a user tries to access a page they don't have permission for, they are redirected to your root page (`/`) by default.

You can change this in [Frontend Configuration](/understanding/subpages/frontend-configuration) — for example, redirecting to a dedicated "You don't have permission to access this page" screen rather than silently sending users to the home page.

---

## Example

A `Dashboard` page might allow the `Registered User` role, while an `Admin Panel` only allows the `Admin` role. A user with only `Registered User` can access the dashboard but will be redirected if they try to reach the admin panel.

---

## Related

<CardGroup cols={2}>
  <Card title="Workflow Auth" href="/understanding/subpages/workflow-auth" />
  <Card title="Frontend Configuration" href="/understanding/subpages/frontend-configuration" />
  <Card title="Understanding User Management" href="/understanding/understanding-user-management" />
  <Card title="Signing Users Up" href="/understanding/subpages/signing-users-up" />
</CardGroup>