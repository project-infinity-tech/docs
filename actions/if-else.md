# If/Else

# If/Else — Workflow Action

**If/Else** is the decision-making action in a Scram workflow. It evaluates a condition and routes execution down one of two paths — the **true** branch or the **false** branch — based on the result. Without it, every workflow would run the same steps every time, regardless of what actually happened.

---

## What is If/Else?

If/Else is a **control flow step** that splits a workflow into two branches. Only one branch executes on any given run. Once a branch finishes, the workflow ends — the two branches never rejoin.

This last point is critical and worth stating plainly:

> *⚠️ **No steps can be placed after an If/Else.** Any logic that needs to run must be duplicated into each branch that requires it.*
> 

---

## Inputs

If/Else takes a single input:

### Condition

A **boolean expression** that resolves to either `true` or `false` at runtime. If it is truthy, the `true` branch runs. If it is falsy, the `false` branch runs.

Common condition patterns:

| **Purpose** | **Example** |
| --- | --- |
| Check a step succeeded | `steps.saveRecord.output.success` |
| Check a step failed | `!steps.login.output.success` |
| Compare a value | `vars.count > 0` |
| Check for a specific error | `steps.fetch.output.errorCode === "NotFound"` |
| Check user is logged in | `user !== null` |
| Check a variable state | `vars.isEditing === true` |

---

## Branches

### True Branch

Runs when the condition is **truthy**. Typically the "happy path" — the thing you wanted to happen, happened.

### False Branch

Runs when the condition is **falsy**. Typically the error or alternative path — something went wrong, or the user took a different route.

Both branches are optional — you can leave one empty if nothing needs to happen in that case. But for any step that can fail, you should always handle the false branch.

---

## The No-Rejoin Rule

This is the most important structural constraint in Scram workflows, and the one most likely to catch you out.

**Wrong mental model:**

```
Fetch data
  ↓
If/Else (did it succeed?)
  ↓ true        ↓ false
Set variable   Show error
  ↓                ↓
Navigate ←————————         ← THIS DOES NOT EXIST
```

**Correct mental model:**

```
Fetch data
  ↓
If/Else (did it succeed?)
  ↓ true              ↓ false
Set variable        Set error variable
Navigate            (workflow ends)
```

If navigation (or any other step) needs to happen in both branches, it must appear in **both branches separately**.

---

## Common Patterns

### Handling a failed API call

```
true:   SetVariable vars.result = steps.fetch.output.value
false:  SetVariable vars.errorMessage = "Something went wrong. Please try again."
```

### Redirecting after login

```
true:   ReloadUser → NavigateToPath (dashboard)
false:  SetVariable vars.loginError = "Invalid email or password."
```

### Showing different content based on user role

```
condition: user !== null && user.roles.some(r => r.id === 'admin')
true:   NavigateToPath (admin panel)
false:  NavigateToPath (home page)
```

### Handling a specific error type

```
condition: steps.fetch.output.errorCode === "NotFound"
true:   SetVariable vars.message = "That record no longer exists."
false:  SetVariable vars.message = "An unexpected error occurred."
```

---

## Nesting If/Else

If/Else steps can be **nested inside each other's branches** to handle more complex logic. A true branch can itself contain another If/Else with its own condition. There is no formal limit on nesting depth, but deeply nested workflows become hard to read — consider whether a CaseSwitch action (for multiple discrete values) would be cleaner.

---

## Relationship to Other Actions

If/Else is almost always the step **immediately after** anything that can fail:

- **Data source actions** (API calls, database queries) — check `.output.success` before using the result
- **Login / Signup** — check success before calling ReloadUser or navigating
- **File uploads** — check success before storing the resulting URL
- **RunCode** — check success before using the return value

A workflow that calls an API without an If/Else afterwards will blindly continue even if the call failed — often causing confusing behaviour or silent errors in the UI.

---

## Relationship to CaseSwitch

If/Else handles **binary decisions** — yes or no, success or failure, on or off. When you need to branch on **more than two possible values** (e.g. a status field that could be `"pending"`, `"active"`, or `"cancelled"`), use **CaseSwitch** instead. It works on the same principle but supports multiple named branches and a default fallback.

---

In summary: If/Else is how a Scram workflow **responds to reality**. It is what separates a workflow that assumes everything works from one that actually handles what happens when it doesn't.