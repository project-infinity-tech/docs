# Log Message and Log to Console

# Log Messages — Workflow Actions

Scram provides two logging actions — **Log to Console** and **Logger** — one for frontend workflows and one for backend. Both exist for the same purpose: capturing information about what a workflow is doing at runtime, to help you understand and debug its behaviour.

---

## Log to Console

**Log to Console** writes a message to the browser's developer console. It is a frontend-only action, available in any workflow triggered by a user interaction.

### Inputs

### Message

The text to write to the console. This is a dynamic expression — it can include variable values, step outputs, or any other runtime data:

```
"User clicked submit. Email: " + components.emailInput.vars.value
```

```
steps.fetchUser.output.value
```

You can log a plain string or pass an object/array directly — the console will render it inspectably.

### Level

Controls how the message appears in the console and how it can be filtered. Options:

| **Level** | **Use for** |
| --- | --- |
| `log` | General information (default) |
| `info` | Informational messages, highlighted in some consoles |
| `warn` | Something unexpected that isn't an error |
| `error` | A failure or problem worth investigating |

The level does not affect workflow execution — it is purely a display and filtering aid.

### How to View Output

Open your browser's developer tools (usually F12 or right-click → Inspect) and select the **Console** tab. Messages appear as the workflow executes, in real time.

---

## Log Message

**Logger** is the backend equivalent. It writes a message to the **server logs** rather than the browser console. It is available in server-side workflows — data-source triggers, backend actions, and similar.

### Inputs

### Message

The text or value to log. Same as Log to Console — a dynamic expression that can reference step outputs, trigger payloads, or any workflow context available on the server.

### How to View Output

Server log output is visible in the Scram editor's log viewer, not in the browser console. It persists across requests and is useful for understanding what is happening on the server side of a workflow — what data arrived in a webhook payload, what a query returned, where an unexpected value crept in.

---

## When to Use Logging Actions

Logging actions are **development and debugging tools**. Their primary use cases are:

**Inspecting step outputs mid-workflow** When a later step is receiving unexpected data, place a log step immediately after the step producing the data to see exactly what it returned.

**Confirming a workflow is reaching a certain point** If you are unsure whether the true or false branch of an If/Else is executing, log a distinct message in each branch.

**Tracing a value through transformations** Log the value before and after a Run Code step or complex expression to confirm the transformation is producing what you expect.

**Understanding incoming webhook or trigger data** On the server side, logging `trigger.payload` at the start of a data-source workflow is often the fastest way to confirm what an external service is actually sending.

---

## What Logging Actions Are Not

- ❌ **Not for production monitoring** — these are development tools, not a logging infrastructure for tracking production usage or errors
- ❌ **Not for user-facing output** — nothing logged here is visible to the end user; use Set Variable and display components for that
- ❌ **Not a substitute for If/Else error handling** — logging that something failed does not handle the failure; always use If/Else to respond to errors, not just observe them

---

## A Note on Leaving Logs In

There is no harm in leaving Log to Console or Logger steps in a workflow — they have no side effects and do not slow execution meaningfully. That said, logging sensitive data (passwords, personal information, tokens) to the console or server logs is poor practice regardless of environment. Log the shape and structure of data to confirm it is correct, not the sensitive values themselves.

---

In summary: Log to Console and Logger are **visibility tools** — a way to look inside a running workflow and see what is actually happening, rather than guessing from the outside. Use them freely while building and debugging, and treat unexpectedly missing or malformed log output as a signal worth investigating.