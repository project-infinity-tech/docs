# Understanding Events, Triggers and Workflows

## The Core Idea

Every interactive app needs to respond to the user. In Scram, this happens through a two-part system:

- **Events** — something that *happens* (a button is clicked, a form is submitted, a value changes)
    - **Triggers** - the groups of Events on a Component
- **Workflows** — what you *do* in response (save data, navigate, show a message)

Think of it as: **"When [event] fires from Component’s [triggers}, do [workflow]."**

---

## Events

A component fires an ev**ent** when something occurs. You will see these on the “triggers” tab of a Component (along with Properties and Styles).

Every component exposes its own set of events. Common examples:

| **Component** | **Events** |
| --- | --- |
| Button | `click` |
| Text Input | `everyChange`, `committedChange` |
| Checkbox | `committedChange` |
| Button Group | `buttonClick` |
| Custom component | Any events you define  |

> 
> 
> 
> Advanced : Every event must ultimately originate from a **native HTML element** — a `<button>`, `<input>`, `<div onClick>`, etc. These are the only things that can truly "fire" in a browser.
> 
> When you add an event to a **custom component definition**, you're declaring that the component *can* emit that event — but it won't do anything until something inside the component actually triggers it. That means wiring up an **EmitEvent** step in an internal workflow, fired by one of those underlying HTML elements deep inside the component tree.
> 
> As an example : A Scram Button has a very fancy HTML <button> at  
> 
> ***In short:** adding an event to a component is just a declaration. Without an `EmitEvent` step connected to a real interaction inside, nothing will ever fire.*
> 

---

## Workflows

A workflow is a sequence of [Understanding Actions](Understanding%20Actions%2030b65b4769b58036a2d5f773fe4a3f14.md)  run when an event fires. Steps execute top-to-bottom and can:

- **Read and write data** — query the database, call an API
- **Set variables** — update page or component state
- **Navigate** — send the user to another page
- **Branch** — make decisions with `IfElse` or `CaseSwitch`
- **Run code** — execute custom JavaScript for complex transforms

See [Action Directory](Action%20Directory%2031065b4769b58012b096d8ae6374ca05.md) for a list of all Actions

### Workflow Types

Workflows run in 3 main areas of Scram. They work the same across all areas, but some actions may not be available in all.

| **Type** | **When it runs** | **Used for** |
| --- | --- | --- |
| **Frontend** | When a user triggers an event from a Component | Clicks, form submissions, interactions |
| **Page Data** | Automatically on page load | Fetching initial data before the user sees the page |
| **Data Source (API endpoint)** | When an external service calls your app | Webhooks, REST APIs |

---

## Step Output & Error Handling

Every step produces an output you can reference in later steps:

```
steps.myStep.output.value     → the returned data
steps.myStep.output.success   → true or false
steps.myStep.output.errorCode → e.g. "NotFound", "Unauthorized"
```

**Critical rule:** Steps keep running even if a previous step fails. Always follow a step that can fail (API call, database query, login) with an `IfElse` that checks `steps.myStep.output.success` before using its result.

```
[Fetch user] → [IfElse: steps.fetch.output.success]
                  ├── true  → [SetVariable: store result]
                  └── false → [SetVariable: show error message]
```

---

## Control Flow

### IfElse

Two branches: `true` and `false`. Best for binary decisions.

```
IfElse: steps.login.output.success
  ├── true  → NavigateToPath (dashboard)
  └── false → SetVariable (vars.errorMsg = "Invalid credentials")
```

### CaseSwitch

Multiple branches with individual conditions. Best for 3+ outcomes.

```
CaseSwitch
  ├── case: trigger.payload.value === "save"   → [save steps]
  ├── case: trigger.payload.value === "delete" → [delete steps]
  └── default case                             → [fallback steps]
```

> *⚠️ **No steps after control flow.** You cannot add steps after a closing `IfElse` or `CaseSwitch`. All logic must live inside the branches.

In other words, Scram does not have a “Join” workflow action. All branches are independent.*
> 

---

## Variables: Where Workflow Results Live

Workflows don't directly change the UI — they write to **variables**, and the UI reacts to those variables.

| **Scope** | **Reference** | **Use for** |
| --- | --- | --- |
| Page variable | `vars.myVar` | State shared across the whole page |
| Component variable | `components.id.vars.value` | State scoped to a specific component |
| Page data | `page.data.name.value` | Read-only data loaded on page load |

Use a **SetVariable** step to write a value, then bind a component's prop to that variable to display it.

---

## Custom Events (Component Definitions)

When building a **custom component definition**, you can define your own events using `EmitEvent`. This lets a child component communicate upward — for example, a custom card emitting a `select` event when clicked, which a parent workflow can listen for.

---

## Summary

```
User action
    ↓
Event fires on component
    ↓
Workflow triggers
    ↓
Steps execute (fetch, compute, branch)
    ↓
SetVariable updates state
    ↓
UI re-renders reactively
```

Events and Workflows are the backbone of all interactivity in Scram — every button click, form save, page navigation, and data load flows through this system.