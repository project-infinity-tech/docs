# Set Variable

# Set Variable — Workflow Action

The **Set Variable** action is the fundamental way to update state in a Scram app. Whenever something on the page needs to change in response to user interaction — a counter increments, a modal opens, a form resets — Set Variable is almost always involved.

---

## What is Set Variable?

Set Variable is a **workflow step** that writes a new value to a variable. It is the only way to mutate state in Scram. Everything else — what you display, what gets sent to a database, what a component renders — ultimately reads from variables that Set Variable has written.

---

## Inputs

Set Variable takes two inputs:

### Variable

The **target** — the variable you want to update. This must be a reference to an existing variable, not a freeform expression. There are three scopes you can write to:

| **Scope** | **Syntax** | **When to use** |
| --- | --- | --- |
| **Page variable** | `vars.myVariable` | Shared state across the whole page |
| **Component variable** | `components.componentId.vars.myVariable` | State belonging to a specific component |

> *⚠️ A component **cannot set its own variables** using Set Variable — only a sibling or page-level workflow can write to a component's variables. For a component's own internal state, use page variables instead.*
> 

### Value

The **new value** to write into the variable. This can be:

- A **literal** — a fixed string, number, or boolean (e.g. `true`, `0`, `"draft"`)
- A **dynamic expression** — the result of a calculation, another variable, or a previous workflow step's output (e.g. `steps.fetchUser.output.value.name`)
- A **transformation** — any valid JavaScript expression (e.g. `vars.count + 1`, `[...vars.items, newItem]`)

The value must match the **type** of the variable — writing a number into a text variable, for example, will cause a type error.

---

## How it Works at Runtime

When a workflow reaches a Set Variable step, it:

1. Evaluates the **Value** expression
2. Writes the result into the **Variable** reference
3. Any component on the page that reads that variable **re-renders immediately** with the new value

This is synchronous and instant — there is no loading state, no delay. The page reacts the moment the step completes.

---

## Common Patterns

### Toggling a boolean

```
Variable: vars.isMenuOpen
Value:    !vars.isMenuOpen
```

Each time this runs, it flips the menu between open and closed.

### Storing an API result

```
Variable: vars.searchResults
Value:    steps.fetchResults.output.value
```

After a data fetch step, its output is captured into a page variable so the UI can display it.

### Resetting a form

```
Variable: vars.formError
Value:    ""
```

Clearing an error message variable before re-submitting a form.

### Appending to a list

```
Variable: vars.selectedItems
Value:    [...vars.selectedItems, current.data]
```

Adding the currently repeated item to a running list of selections.

---

## Important Constraints

- **Variables must exist before they can be set.** Create them on the page or component definition first.
- **Type safety matters.** The value written must match the variable's declared type.
- **A component cannot write to its own variables.** This is a platform constraint — use a page variable as an intermediary.
- **Set Variable is frontend-only.** It has no effect on the database or any external service. To persist data, follow Set Variable with a database action.

---

## Relationship to Other Actions

Set Variable rarely works alone. It is almost always used in combination with:

- **Data source actions** — to capture the result of an API call or database query into a variable for display
- **IfElse** — to conditionally set different values depending on success or failure
- **ReloadPageData** — when you want to refresh server data after a mutation, rather than manually updating local state
- **RunCode** — for complex transformations before storing the result

---

In summary: Set Variable is the **write** half of Scram's state system. Variables hold the truth of what the page currently knows, and Set Variable is how that truth gets updated.