# Signup New User with Email and Password

# Overview

**Signup** creates a new user account using an email address and password. It is the starting point of the email/password authentication flow — the moment a new person goes from visitor to registered user.

---

## What is Signup?

Signup is a **built-in authentication action** that registers a new end user with the app. It takes an email and password, creates a record in the built-in **Users** table, and signs the user in immediately if successful.

It does not send a welcome email, assign roles, or redirect anywhere by itself. Those things are your responsibility in the steps that follow.

---

## Inputs

### Email

The email address for the new account. Must be a valid email — sourced from an email input component:

```
components.emailInput.vars.value
```

### Password

The password to set for the account. Source this from a password input component:

```
components.passwordInput.vars.value
```

Never hardcode passwords. Never log them. Never store them in a variable longer than necessary. They should flow directly from the input component into this action and nowhere else.

---

## What Happens on Success

A new row is created in the **Users** table with:

- The provided email address
- A securely hashed version of the password (never stored in plain text)
- `authType` set to `"userpass"`
- `roles` set to an **empty array** — `[]`

That last point is important enough to have its own section.

---

## ⚠️ New Users Have No Roles

This is the most common source of confusion in signup flows. Signup creates the account, but it does **not** assign any roles. The user's `roles` array is empty.

If your app uses role-based access control — protected pages, restricted workflows, members-only content — a freshly signed-up user will be locked out of all of it immediately after registering.

**You must assign a default role explicitly**, in the workflow, right after Signup succeeds. The pattern is:

```
1. Signup (email, password)
2. If/Else (did Signup succeed?)
   true:
     3. ReloadUser
     4. ExecuteSQL — UPDATE "Users" SET roles = ARRAY['roleId'] WHERE id = user.id
     5. ReloadUser  ← again, so the client sees the new role
     6. NavigateToPath (dashboard or onboarding)
   false:
     3. SetVariable vars.errorMessage = steps.signup.output.message
```

Without step 4, the user lands on a role-protected page and is immediately transferred to the “failed authorisation page” or the home page. They will be confused. Do not skip this step.

See [Page Authorisation](Page%20Authorisation%202e265b4769b580fba17bcc6c514affe3.md) for more information on this.

---

## The Full Recommended Pattern

```
1. Signup
   — email:    components.emailInput.vars.value
   — password: components.passwordInput.vars.value

2. If/Else (steps.signup.output.success)
   true:
     3. ExecuteSQL
        — UPDATE "Users" SET roles = ARRAY['defaultRoleId'] WHERE id = user.id
     4. ReloadUser
        — Refreshes the client-side user object with the new role
     5. NavigateToPath → home / dashboard / onboarding
   false:
     3. SetVariable vars.signupError = steps.signup.output.message
```

---

## Common Failure Cases

| **Scenario** | **`errorCode`** | **What to show** |
| --- | --- | --- |
| Email already registered | `ValidationFailure` | "An account with this email already exists." |
| Password too weak | `ValidationFailure` | "Please choose a stronger password." |
| Invalid email format | `ValidationFailure` | "Please enter a valid email address." |
| Network or server error | `OtherSideCrashed` | "Something went wrong. Please try again." |

Surface these via a Set Variable step in the false branch, displayed in a text component bound to the error variable. Do not show raw error objects to users — use `steps.signup.output.message` as a starting point and adjust the copy to be friendly.

---

## What Signup is Not

- ❌ **Not a login** — it creates the account and signs in, but does not replace the Login action for returning users
- ❌ **Not a role assigner** — you must handle role assignment yourself, in the workflow
- ❌ **Not a welcome emailer** — if you want to send a welcome email, add that as a separate step after a successful signup
- ❌ **Not a validator** — Scram validates the email format, but checking that passwords match (if you have a confirm password field) is your responsibility, ideally with an If/Else *before* this step even runs

---

## Before Signup Runs

Consider validating inputs before the Signup action executes at all:

```
If/Else (components.passwordInput.vars.value === components.confirmInput.vars.value)
  true:
    Signup...
  false:
    SetVariable vars.signupError = "Passwords do not match."
    Terminate.
```

Catching mismatched passwords client-side before hitting the server makes for a faster, smoother experience.

---

## Relationship to Other Auth Actions

| **Action** | **Purpose** |
| --- | --- |
| **Signup** | Create a new account (this action) |
| **Login** | Authenticate a returning user |
| **Social Signup** | Create or sign in via OAuth provider (Google, etc.) |
| **Logout** | End the current session |
| **ReloadUser** | Refresh the client-side `user` object after any auth change |

ReloadUser is essential after Signup. Until it runs, `user.id` is not available — and without `user.id`, you cannot update the user's roles in the database.

---

In summary: Signup creates the account, but it is only the first step. A complete signup flow always includes a success check, a ReloadUser, a role assignment, another ReloadUser, and a navigation step. Skip any of these and someone, somewhere, will register and immediately wonder why the app seems to think they do not exist.