# Signup or Login with Social Provider

**Social Signup** authenticates a user via a third-party OAuth provider — Google, Facebook, Microsoft, or any custom OIDC provider configured for the app. It handles both new and returning users with a single action: if the user has signed in with this provider before, they are logged in; if not, a new account is created automatically.

---

## What is Social Signup?

Social Signup is a **built-in authentication action** that delegates the entire authentication process to an external provider. The user is redirected to that provider's login screen (Google's sign-in page, for example), authenticates there, and is redirected back to the app. Scram handles the OAuth exchange behind the scenes.

Because the provider verifies the user's identity, there is no email or password to collect, validate, or store. The provider's verified email becomes the account's email address.

---

## Inputs

### Provider

The codename of the OAuth provider to use. This must match a provider that has been configured and enabled in the app's authentication settings:

| **Provider** | Name |
| --- | --- |
| Google | `"google"` |
| Facebook | `"facebook"` |
| Microsoft | `"microsoft"` |
| Custom OIDC | The auto-generated name |

This is a string literal — not a reference to a variable or component. You are choosing a specific provider at workflow design time.

---

## What Happens at Runtime

1. The user clicks the social login button
2. Social Signup redirects the browser to the provider's authentication screen
3. The user authenticates with the provider (or is already authenticated and simply confirms)
4. The provider redirects back to Scram with a verified identity token
5. Scram checks whether an account with that provider identity already exists:
    - **Returning user** — the existing account is signed in
    - **New user** — a new account is created with `authType: "social"` and `roles: []`
6. Scram performs its automatic refresh and `/me` call — the `user` object is populated immediately

---

## New Users Have No Roles

Exactly as with email/password Signup, a brand new social user is created with an **empty roles array**. If the app uses role-based access control, the user will be locked out of protected pages immediately after their first sign-in.

You must handle role assignment in the workflow — but only for new users. Returning users already have their roles.

---

## The Recommended Pattern

```
1. Social Signup
   — provider: "google"

2. If/Else (steps.socialSignup.output.success)
   true:
     3. If/Else (is this a new user?)
        condition: steps.socialSignup.output.value.isNewUser
        true (new user):
          4. ExecuteSQL
             — UPDATE "Users" SET roles = ARRAY['defaultRoleId'] WHERE id = user.id
          5. ReloadUser
             — Refreshes user.roles with the newly assigned role
          6. NavigateToPath → onboarding / dashboard
        false (returning user):
          4. NavigateToPath → dashboard
   false:
     3. SetVariable vars.authError = "Sign in failed. Please try again."
```

The `isNewUser` flag on the step output tells you whether Scram just created a new account or signed in an existing one — allowing you to assign roles and route new users differently (to onboarding, for example) without affecting returning users.

---

## Configuring Providers

Social Signup only works if the provider has been set up beforehand. This involves:

1. Creating an OAuth application in the provider's developer console (Google Cloud Console, Facebook Developers, etc.)
2. Configuring the provider in Scram's authentication settings with the **Client ID** and **Client Secret**
3. Registering Scram's **callback URL** in the provider's developer console

The callback URL follows the pattern:

```
{previewBackendUrl}/{provider-codename}/callback
```

Without this configuration, the Social Signup action will fail immediately. A button that says "Sign in with Google" attached to an unconfigured provider will produce an error, not a Google login screen.

---

## One Action for Both Signup and Login

This is worth emphasising. Unlike the email/password flow — which has a separate **Signup** action and a separate **Login** action — social authentication uses a **single action for both**. There is no "social login" and "social signup" to distinguish between. The same workflow, the same action, the same button handles both cases. Scram determines at the point of return from the provider whether to create a new account or sign in an existing one.

This means you do not need separate sign up and log in pages for social providers. One button per provider is sufficient.

---

## What Social Signup is Not

- ❌ **Not a popup** — Social Signup redirects the full browser window to the provider. It does not open in a popup or iframe.
- ❌ **Not instant** — the user leaves the app, authenticates externally, and returns. There is a visible redirect.
- ❌ **Not a role assigner** — new users arrive with empty roles. Assignment is your responsibility in the workflow.
- ❌ **Not available without configuration** — providers must be set up with valid credentials before this action does anything useful.

---

## Relationship to Other Auth Actions

| **Action** | **Purpose** |
| --- | --- |
| [**Signup**](Signup%20New%20User%20with%20Email%20and%20Password%2031065b4769b5805b9666cf200af2a171.md) | Create a new account with email and password |
| [**Login**](Login%20Existing%20User%2031065b4769b580a4bf9ce5561cbddeef.md) | Authenticate a returning user with email and password |
| **Social Signup** | Authenticate via OAuth provider — new or returning (this action) |
| [**Logout**](Logout%20User%2031065b4769b580ccb7f3d223bbc199fe.md) | End the current session |
| [**ReloadUser**](Reload%20User%2031065b4769b5806583a7d9ac54d01abe.md) | Refresh `user` object after a database change to the user's record |

---

In summary: Social Signup is a single action that handles both first-time and returning social users, delegating all credential handling to the external provider. Its workflow is slightly more involved than Login — because new users need role assignment and potentially different routing — but the `isNewUser` flag makes that branching straightforward.