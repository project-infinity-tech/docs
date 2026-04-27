---
title: "Understanding Actions"
---

# Understanding Actions

Actions are the individual steps that make up a workflow. If a workflow is the script, actions are the lines.

---

## What is an Action?

When something happens in your app — a button is clicked, a page loads, a form is submitted — a workflow runs. That workflow consists of one or more **actions**: discrete, named operations that do exactly one thing.

An action might:

- Read or write data to the database
- Call an external API
- Set a variable to a new value
- Navigate the user to a different page
- Send an email
- Show or hide something
- Run a piece of custom code

Each action runs in sequence, one after another, unless you use control flow actions (like **If/Else** or **Case Switch**) to branch the logic.

---

## Built-in vs. Data Source Actions

Actions come from two places:

**Built-in actions** are always available, regardless of how your app is configured. They cover core operations like setting variables, navigating between pages, logging in a user, or uploading a file.

**Data source actions** are added when you connect a data source — your database, an external API, or a service integration. Each connection brings its own set of actions specific to that source (e.g. *Insert Row*, *Send Email*, *Call Endpoint*).

---

## Inputs and Outputs

Every action accepts **inputs** — the information it needs to do its job. These can be literal values ("active") or dynamic expressions that reference variables, other steps, or user data.

Most actions produce an **output** — the result of what they did. You can reference a previous step's output in any later step using `steps.stepId.output.value`.

Actions also report **success or failure**. After any action that can fail (a database query, an API call, a login attempt), you should use an **If/Else** step to check `steps.stepId.output.success` before proceeding. This is how you handle errors gracefully — showing the user a message, retrying, or taking a different path.

---

## Control Flow Actions

Two actions change the *shape* of a workflow rather than doing work themselves:

- **If/Else** — splits the workflow into two paths based on a condition. Only one path runs.
- **Case Switch** — splits into multiple paths, each with its own condition. The first matching case runs; the last case (with no condition) acts as a default.

> *⚠️ Once a workflow enters a branch, it cannot rejoin. Any logic you need on both paths must be duplicated in each branch.*
> 

---

## Finding Actions

For the full list of available built-in actions and what each one does, see the [**Actions Directory →**](Action%20Directory%2031065b4769b58012b096d8ae6374ca05.md).

Data source actions are listed within each connected data source in the editor.

---

## Related

- [Understanding Workflows, Triggers and Events →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Actions Directory →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Connecting Data Sources →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)

[Action Directory](Action%20Directory%2031065b4769b58012b096d8ae6374ca05.md)