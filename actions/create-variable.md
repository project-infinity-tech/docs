# Create Variable

# Create Variable — Workflow Action

**Create Variable** is a server-side workflow action that declares a temporary, named value scoped to a single workflow run. It lets you capture an intermediate result — a calculation, a transformed value, a piece of data extracted from a previous step — and give it a name so later steps in the same workflow can reference it cleanly.

---

## What is Create Variable?

Create Variable is a **local scratchpad step**. It does not write to the database, does not update any UI state, and disappears the moment the workflow finishes. Its only purpose is to make complex workflows easier to reason about by naming intermediate values rather than repeating long expressions throughout the workflow.

Think of it as the server-side equivalent of declaring a named constant mid-workflow.

---

## Inputs

### Name

The identifier you will use to reference this variable in subsequent steps. Once created, it is accessible in later steps as part of the workflow's step output context.

### Value

The expression that produces the value to store. This is evaluated once, at the moment the step runs, using the outputs of all preceding steps. It can be:

- A **literal** — a fixed string, number, or boolean
- A **transformation** — a JavaScript expression derived from earlier step outputs (e.g. filtering an array, extracting a nested field, formatting a string)
- A **computation** — combining multiple step results into a single value

---

## How it Works

Create Variable runs like any other step in the workflow sequence. When it executes:

1. The **Value** expression is evaluated using the current workflow context
2. The result is stored under the given **Name**
3. All subsequent steps can reference it via the step's output

It does not branch, it does not fail, and it does not produce side effects. It simply gives a name to a value and moves on.

---

## When to Use It

Create Variable is most useful when:

**You need the same derived value in multiple places** Rather than repeating `steps.fetchOrder.output.value.items.filter(i => i.status === "pending")` across three different steps, compute it once, name it `pendingItems`, and reference that instead.

**An expression is too complex to read inline** Breaking a deeply nested or multi-part expression into a named intermediate step makes the workflow legible to anyone reading it later.

**You want to combine data from multiple preceding steps** If you have results from two separate database queries and need to merge them before passing to the next step, Create Variable is the natural place to do that transformation.

---

## Relationship to Page Variables

Create Variable and page variables (`vars.name`) solve different problems and should not be confused:

|  | **Create Variable** | **Page Variable** |
| --- | --- | --- |
| **Scope** | This workflow run only | Persists for the lifetime of the page |
| **Accessible from** | Later steps in the same workflow | Any component, workflow, or expression on the page |
| **Written by** | The Create Variable step, automatically | Set Variable action, explicitly |
| **Purpose** | Intermediate computation | UI state |
| **Survives workflow end** | ❌ No | ✅ Yes |

If you need the result to be visible in the UI or usable by other workflows, you still need a **Set Variable** step to write it into a page variable. Create Variable alone will not update the page.

---

## Common Patterns

### Extracting a nested field for reuse

```
Name:  customerId
Value: steps.fetchOrder.output.value.customer.id
```

Later steps reference `steps.createVar.output.value` rather than drilling into the nested path each time.

### Filtering a list before further processing

```
Name:  activeUsers
Value: steps.fetchUsers.output.value.filter(u => u.status === "active")
```

The filtered list is then passed to a subsequent step that sends notifications or generates a report.

### Building a combined payload

```
Name:  emailPayload
Value: { to: steps.fetchUser.output.value.email, subject: "Your order", orderId: steps.fetchOrder.output.value.id }
```

The constructed object is passed cleanly to a following Send Email step.

---

In summary: Create Variable is a **clarity tool**. It does not change what a workflow does — it changes how readable and maintainable that workflow is, by giving meaningful names to intermediate values that would otherwise be long, repeated, or opaque expressions buried inside later steps.