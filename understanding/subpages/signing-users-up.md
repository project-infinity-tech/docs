---
title: "Signing Users Up"
---

Scram provides two ways to sign users up to your app — email and password, and social providers. Both create a new record in the Users table and log the user in automatically on success.

---

## Email and Password

Use the **Signup New User with Email and Password** action in a workflow triggered by your signup form's submit button.

The action requires:
- An email address
- A password

### Password requirements

Passwords must be at least 6 characters and include at least one capital letter and one symbol.

### After signup

Users are created with **no roles by default**. Your signup workflow must immediately assign at least one role after a successful signup — otherwise the user will be locked out of any role-protected pages or workflows.

The recommended pattern after a successful signup:

1. **Execute SQL** — insert the user's role into the `roles` column on the Users table
2. **Reload User** — refreshes the session so the new role takes effect immediately
3. **Navigate** — redirect the user to the appropriate page

<Warning>
  If you skip the role assignment step, users who sign up will appear to be logged in but will be blocked from accessing any page or workflow that requires a role. This is a common source of confusion during testing.
</Warning>

---

## Social Provider

Use the **Signup or Login with Social Provider** action to authenticate via Google, Facebook, or Microsoft. This action handles both new signups and returning logins — if the user already exists, it logs them in; if not, it creates a new account.

Before this action will work, the relevant provider must be configured in the [Users](/resources/users) section of the Resource View. See [Setting Up Google Login](/understanding/subpages/setting-up-google-login) for a step-by-step example.

### After signup

The same role assignment requirement applies — social signups also create users with no roles. Apply the same post-signup pattern: assign a role via Execute SQL, then call Reload User.

---

## Related

<CardGroup cols={2}>
  <Card title="Setting Up Google Login" href="/understanding/subpages/setting-up-google-login" />
  <Card title="Workflow Auth" href="/understanding/subpages/workflow-auth" />
  <Card title="The Users Resource" href="/resources/users" />
  <Card title="Understanding User Management" href="/understanding/understanding-user-management" />
</CardGroup>