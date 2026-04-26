# Login Existing User

**Login** authenticates a returning user with their email address and password. It verifies their credentials, establishes a session, and makes the `user` object available throughout the app.

---

## What is Login?

Login is a **built-in authentication action** that takes an email and password, checks them against the stored credentials in the Users table, and signs the user in if they match. It is the counterpart to Signup — where Signup creates an account, Login resumes one.

On its own, Login does nothing visible. The page does not change, the user is not redirected, and nothing is displayed. What happens after a successful login is entirely defined by the steps that follow it in the workflow.

---

## Inputs

### Email

The email address the user is attempting to sign in with:

```
components.emailInput.vars.value
```

### Password

The password to verify:

```
components.passwordInput.vars.value
```

Both should come directly from input components on the login form. Do not store passwords in page variables or pass them through intermediate steps.

---

## What Happens on Success

- The user's session is established
- The server-side `user` object is populated with the user's data
- The client-side `user` object remains stale until **ReloadUser** runs

That last point is the same as with Signup, and equally important. Login does not automatically refresh the client-side `user` snapshot. Without a ReloadUser step immediately after, `user.id`, `user.roles`, and all other user properties are not yet available to subsequent workflow steps or page expressions.

---

## The Recommended Pattern

```
1. Login
   — email:    components.emailInput.vars.value
   — password: components.passwordInput.vars.value

2. If/Else (steps.login.output.success)
   true:
     3. ReloadUser
        — Populates user.id, user.roles, and all user properties
     4. NavigateToPath → dashboard / home / wherever logged-in users belong
   false:
     3. SetVariable vars.loginError = "Invalid email or password."
```

This is intentionally simpler than the Signup pattern — there are no roles to assign, no second ReloadUser. Login finds an existing user with roles already set. One ReloadUser is all that is needed.

---

## Common Failure Cases

| **Scenario** | **What to show** |
| --- | --- |
| Wrong password | "Invalid email or password." |
| Email not registered | "Invalid email or password." |
| Account suspended | "Your account has been suspended." |
| Network or server error | "Something went wrong. Please try again." |

Notice that wrong password and unrecognised email return the **same message**. This is intentional. Telling a user which of the two is wrong is a small but real security leak — it lets someone enumerate which email addresses have accounts. Keep the message deliberately ambiguous.

---

## Error Message Wording

Use `steps.login.output.message` as a starting point, but do not show it raw. System error messages are written for developers, not users. Translate them into friendly, plain-language copy before surfacing them in the UI.

---

## Navigating After Login

Where to send the user after a successful login depends on the app. Common approaches:

**Always go to the same place**

```
NavigateToPath → pages.dashboard
```

**Go to the page they were trying to reach** If your app redirects unauthenticated users to the login page, you may have stored their intended destination in a query parameter. Read it and navigate there:

```
NavigateToPath → page.queryParams.returnTo (if present), otherwise pages.dashboard
```

**Branch by role**

```
If/Else (user.roles.some(r => r.id === 'adminRoleId'))
  true:  NavigateToPath → pages.adminDashboard
  false: NavigateToPath → pages.userDashboard
```

---

## What Login is Not

- ❌ **Not a session checker** — it does not tell you if a user is already logged in. Check `user !== null` in an expression for that.
- ❌ **Not a role assigner** — roles were assigned at signup. Login simply loads them.
- ❌ **Not a redirect** — it does not navigate anywhere on its own. Navigation is always a separate step.
- ❌ **Not suitable for social login** — for Google, Facebook, or other OAuth providers, use **Social Signup** instead.

---

## Relationship to Other Auth Actions

| **Action** | **Purpose** |
| --- | --- |
| **Signup** | Create a new account |
| **Login** | Authenticate a returning user (this action) |
| **Social Signup** | Authenticate via OAuth provider |
| **Logout** | End the current session |
| **ReloadUser** | Refresh the client-side `user` object after any auth change |

---

## A Note on the Login Form

The login workflow should be triggered by the **form's submit event** or a **button's click event** — whichever the UI uses. If using a button, consider also handling the `committedChange` event on the password input so that pressing Enter submits the form, which is the behaviour users expect.

---

In summary: Login is deliberately simple — two inputs, one action, one ReloadUser, one navigation. Its simplicity is a feature. The complexity in an auth flow lives in error handling, role-based routing, and the post-login experience — not in the login action itself.