---
title: "Understanding Server Logs"
---

The Server Log is a live feed of everything happening on the backend of your app. It's where you go when something isn't working the way you expect — and increasingly, as you build more complex apps, it becomes an indispensable part of your development workflow.

---

## What it Shows

Every time a backend operation runs, it leaves a trace in the Server Log. This includes:

- **Workflow executions** — when a workflow runs, each step is logged with its inputs, outputs, and whether it succeeded or failed
- **Database queries** — the SQL that was executed, the parameters passed, and the result
- **API calls** — outgoing requests to external services, including the request details and the response received
- **Errors and exceptions** — anything that went wrong, with as much detail as the system can provide
- **Logger action output** — messages you've explicitly logged using the **Logger** action in your workflows

The log is chronological, with the most recent entries at the top.

---

## The Logger Action

The Logger action exists specifically to help you understand what's happening inside a workflow. You place it as a step and give it a message — usually an expression that outputs the value of something you want to inspect.

For example, if you're unsure what data a step is producing, add a Logger step immediately after it and log `steps.myStep.output.value`. The result appears in the Server Log the next time that workflow runs.

This is the backend equivalent of a `console.log`. Use it freely while building, then remove it when you're done.

> *Logger is a backend-only action. It runs in the context of server-side workflow execution, not in the browser.*
> 

---

## Reading an Entry

Each log entry shows:

- **Timestamp** — when the operation occurred
- **Type** — what kind of operation it was (workflow step, query, error, log message)
- **Detail** — the specifics: the message, query, response, or error

Errors are visually distinct from informational entries, making it quick to spot what went wrong in a sequence of steps.

---

## When to Use It

**Something isn't saving to the database.** Check whether the query ran, what parameters were passed, and whether a SQL error was returned.

**An API call isn't working.** See the exact request that was sent and the exact response that came back — including error codes and response bodies that don't surface in the UI.

**A workflow seems to run but nothing happens.** Check whether it reached the step you expected, or whether it branched somewhere unexpected.

**You're not sure what a step is returning.** Add a Logger action, run the workflow, and inspect the output directly.

---

## Key Things to Know

**The Server Log shows backend activity only.** Things that happen purely in the browser — a variable being set, a component showing or hiding — don't appear here. For frontend debugging, use your browser's developer console.

**Logs are live but not persistent indefinitely.** The log reflects recent activity. It's a diagnostic tool for active development, not a permanent audit trail.

**Sensitive data can appear in logs.** Query parameters, API responses, and logged values may contain real data. Be mindful of this when working with production environments.

---

## Related

- [Understanding Actions →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Understanding Workflows, Triggers and Events →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Working with the Database →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Connecting External APIs →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)