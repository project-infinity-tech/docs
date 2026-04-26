# Run Code

# Run Code — Workflow Action

**Run Code** executes a custom JavaScript function as a workflow step. It is the escape hatch for logic that cannot be expressed as a simple expression or covered by Scram's built-in actions — complex data transformations, multi-step calculations, string manipulations, or anything that genuinely requires procedural code to express clearly.

---

## What is Run Code?

Run Code is a **frontend workflow step** that runs an async JavaScript function in a sandboxed environment. Whatever the function returns becomes the step's output, accessible to subsequent steps as `steps.stepId.output.value`.

It is intentionally limited in scope. Run Code is not a general-purpose scripting environment — it cannot interact with the browser, make network requests, or produce side effects. Its job is to **transform data and return a result**.

---

## Inputs

### Code

The body of an async JavaScript function. You provide only the body — Scram wraps it automatically as:

```
async function stepName() {
  // your code here
}
```

Whatever you `return` from the body becomes the step's output value.

---

## What is Available Inside Run Code

The following context objects are accessible within the function body:

| **Context** | **What it provides** |
| --- | --- |
| `steps` | Outputs of all preceding workflow steps |
| `vars` | Current page variable values |
| `component` | The ID of the component that triggered the workflow |
| `trigger` | The event payload that started the workflow |
| `page.data` | Current page-data values |
| `user` | The currently authenticated user object |
| `current` | The current repeater item (if triggered from inside a Repeater) |
| `config` | App configuration values |

---

## What is NOT Available

Run Code runs in a **sandboxed environment** with no access to browser APIs:

- ❌ `document` — no DOM access
- ❌ `window` — no browser globals
- ❌ `querySelector` and all DOM methods
- ❌ `fetch`, `XMLHttpRequest` — no network calls
- ❌ `setTimeout`, `setInterval` — no timers
- ❌ `localStorage`, `sessionStorage` — no browser storage
- ❌ External libraries — no imports

If you need to make an API call, use a data source action. If you need to interact with the DOM, reconsider — Scram components handle rendering and you should not need to touch the DOM directly.

---

## Timeout

Run Code has a **5-second execution limit**. If the function has not returned within 5 seconds, it is terminated and the step returns an error. Functions that take longer than this indicate either an infinite loop or logic that belongs in a backend action rather than a frontend code step.

---

## Return Value

Whatever the function returns becomes `steps.stepId.output.value` for subsequent steps. You can return:

- A primitive — a string, number, or boolean
- An array — a transformed or filtered list
- An object — a restructured or merged data shape
- `undefined` — if the function doesn't explicitly return, the output value will be undefined

If the function throws an error, `steps.stepId.output.success` will be `false`. Always check this with an If/Else if the subsequent logic depends on the result.

---

## When to Use It

Run Code is the right choice when:

**The transformation is too complex for an inline expression** Filtering and reshaping a nested array, computing a derived value across multiple conditions, or building a structured object from disparate inputs.

**The logic requires multiple statements** If you need to declare intermediate values, loop over items, or use conditionals to build a result, an expression is not the right tool.

**You need a reusable calculation** A calculation that combines several step outputs into one clean result before passing it to a database action or Set Variable step.

---

## When NOT to Use It

| **Instead of Run Code, use...** | **When...** |
| --- | --- |
| A simple expression | The transformation is a single statement |
| **If/Else** | You need to branch based on a condition |
| **Set Variable** | You just need to store a value |
| A data source action | You need to call an API or query the database |
| **Create Variable** | You need to name an intermediate value in a server workflow |

Run Code adds friction — it is harder to read at a glance than a named action with clear inputs. Reach for it only when the alternatives genuinely cannot express what you need.

---

## Common Patterns

### Filtering and reshaping an array

```
const orders = steps.fetchOrders.output.value;
return orders
  .filter(o => o.status === "pending")
  .map(o => ({ id: o.id, label: `#${o.reference} — ${o.customerName}` }));
```

### Computing a summary value

```
const items = steps.fetchItems.output.value;
const total = items.reduce((sum, item) => sum + item.price * item.quantity, 0);
return { total, itemCount: items.length, hasItems: items.length > 0 };
```

### Building a structured payload from multiple steps

```
return {
  userId: user.id,
  productId: trigger.payload.id,
  quantity: vars.selectedQuantity,
  addedAt: new Date().toISOString()
};
```

### Deduplicating a list

```
const seen = new Set();
return steps.fetchResults.output.value.filter(item => {
  if (seen.has(item.id)) return false;
  seen.add(item.id);
  return true;
});
```

---

## Error Handling

Because Run Code can fail (a thrown error, a timeout, an operation on undefined data), treat it like any other fallible step. Follow it with an **If/Else** checking `steps.stepId.output.success` before using the result in subsequent steps:

```
true:   SetVariable vars.processedData = steps.runCode.output.value
false:  SetVariable vars.errorMessage = "Failed to process data."
```

---

In summary: Run Code is the **custom logic escape hatch** — a place to express procedural JavaScript transformations that are too complex or multi-step for inline expressions, while remaining firmly scoped to data transformation rather than side effects. Use it deliberately, not as a default.