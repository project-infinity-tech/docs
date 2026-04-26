# Logout User

**Logout** ends the current user's session. It is the cleanest action in Scram's entire library — no inputs, no configuration, no decisions to make. It just signs the user out.

---

## What is Logout?

Logout is a **built-in authentication action** that terminates the active session on the server and clears the client-side `user` object. After it runs, `user` is `null` and the app treats the visitor as unauthenticated.

It takes no inputs. There is nothing to configure. You add it to a workflow and it does exactly one thing.

---

## Inputs

None.

---

## What Happens on Logout

- The session is invalidated on the server
- The client-side `user` object becomes `null`
- Any page or expression that checks `user !== null` will now evaluate to `false`
- Any protected page the user tries to visit will redirect them away, as configured in the app's error handling settings

---

## The Recommended Pattern

```
1. Logout

2. NavigateToPath → login page / home / landing page
```

That is genuinely the whole pattern. Logout does not need an If/Else. It does not need a ReloadUser. It does not fail in any meaningful way that requires handling. You log the user out and you send them somewhere appropriate.

```
NavigateToPath is not optional.
```

Without it, the user is signed out but still looking at the page they were on. If that page is protected, they will be redirected automatically. If it is not protected, they will see a page that may still visually appear as though they are logged in until the next render cycle. Always navigate explicitly after logout.

---

## Where to Put the Logout Trigger

Logout is almost always triggered from a persistent UI element — something available on every authenticated page:

- A **Sign out** link in a navigation bar
- An option in a user avatar dropdown menu
- A button on an account or settings page

Since it appears in a reusable component (a nav bar, a header), the workflow is typically defined on that component definition. The Logout action runs, followed by NavigateToPath to the login or landing page.

---

## What Logout is Not

- ❌ **Not a data clearer** — Logout does not clear page variables, reset form inputs, or wipe any local state. If your app holds sensitive data in page variables, consider whether that data persists somewhere it should not after logout. In practice, navigating away from the page after logout clears all page state automatically.
- ❌ **Not a confirmation dialog** — Scram does not show a "are you sure?" prompt automatically. If you want one, build it yourself with a boolean variable and a conditional UI element before the Logout step runs.
- ❌ **Not reversible in the workflow** — once Logout runs, the session is gone. There is no undo, no rollback, no second thoughts.

---

## Adding a Confirmation Step

If you want to prompt the user before logging them out:

```
SetVariable vars.showLogoutConfirm = true
```

Then in the UI, show a confirmation modal bound to `vars.showLogoutConfirm`. The confirm button's workflow runs:

```
1. Logout
2. NavigateToPath → login page
```

The cancel button simply sets `vars.showLogoutConfirm = false`. The Logout action itself never needs to know about the confirmation — it just runs when called.

---

## Relationship to Other Auth Actions

| **Action** | **Purpose** |
| --- | --- |
| **Signup** | Create a new account |
| **Login** | Authenticate a returning user |
| **Social Signup** | Authenticate via OAuth provider |
| **Logout** | End the current session (this action) |
| **ReloadUser** | Refresh the client-side `user` object |

Note that ReloadUser is **not needed** after Logout. ReloadUser fetches the current user from the server — but after logout there is no current user to fetch. Navigation away from the page is all that is required.

---

In summary: Logout is the simplest action in the authentication system — no inputs, no error handling, no edge cases worth losing sleep over. Add it to a workflow, follow it with a NavigateToPath, and the user is cleanly and completely signed out. The only way to do it wrong is to forget the navigation step.