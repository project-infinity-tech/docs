# Reload User

**Reload User** fetches the current user's data from the server and refreshes the client-side `user` object. It is the action that bridges the gap between something changing about the user on the server and the app knowing about it.

---

## What is Reload User?

The `user` object available in expressions throughout Scram — `user.id`, `user.roles`, `user.givenName`, and so on — is a **snapshot**. It does not update itself automatically when the underlying data changes.

Reload User says: *go back to the server, get the current state of this user, and replace the snapshot with what you find.*

It takes no inputs. It simply re-fetches and refreshes.

---

## Inputs

None.

---

## After Login and Signup — You Don't Need It

This is the key distinction. When **Login** or **Signup** succeed, Scram automatically performs a token refresh and a `/me` request behind the scenes. By the time those actions complete, the `user` object is already populated — `user.id`, `user.roles`, and all other properties are available immediately in the next workflow step.

**You do not need to call Reload User after Login or Signup.**

---

## When You DO Need Reload User

Reload User is needed when user data changes **after** the initial login or signup — that is, when a subsequent operation modifies the user's record in the database and you need the client-side snapshot to reflect that change.

The most common case is **role assignment** during a signup flow:

```
1. Signup
2. If/Else (success?)
   true:
     3. ExecuteSQL — UPDATE "Users" SET roles = ARRAY['roleId'] WHERE id = user.id
        ← user.id is already available, no ReloadUser needed first
     4. ReloadUser
        ← refreshes user.roles so the newly assigned role is visible
     5. NavigateToPath
```

Other cases where Reload User is appropriate:

| **Event** | **Why Reload User is needed** |
| --- | --- |
| After assigning or changing roles | `user.roles` still reflects the old value until refreshed |
| After updating profile fields | Name, photo URL, or custom fields changed in the database but not yet reflected client-side |
| After any direct `UPDATE "Users"` query | The database has changed; the snapshot has not |

---

## What Reload User is Not

- ❌ **Not needed after Login** — Scram's built-in refresh/me calls handle this automatically
- ❌ **Not needed after Signup** — same reason
- ❌ **Not needed after Logout** — there is no user to reload. Navigate away instead.
- ❌ **Not a session check** — it does not tell you whether a user is logged in. Check `user !== null` for that.
- ❌ **Not automatic after database writes** — if you update the Users table directly and do not call Reload User, the app will continue showing stale data until the page is refreshed.

---

## Does it Ever Fail?

Reload User is a straightforward fetch of the current session's user data. There is no meaningful failure case to handle in the way there is for API calls or database writes. You do not need to follow it with an If/Else.

---

## Relationship to Other Auth Actions

| **Action** | **Reload User needed after?** |
| --- | --- |
| **Signup** | ❌ No — Scram handles this automatically |
| **Login** | ❌ No — Scram handles this automatically |
| **Social Signup** | ❌ No — Scram handles this automatically |
| **Logout** | ❌ No |
| **Updating user data in the database** | ✅ Yes — if the change should be reflected in the `user` object |

---

In summary: Reload User is **not** the routine step after every auth action that it might appear to be. Scram handles the post-login and post-signup refresh automatically. Reload User exists specifically for the cases where you have directly modified the user's data in the database afterwards — most commonly, assigning a default role during signup — and need the client-side snapshot to catch up.