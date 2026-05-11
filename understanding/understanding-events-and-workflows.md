---
title: "Understanding Events and Workflows"
description: "How events and workflows power the logic of your Scram app."
---

Events and workflows are how your app responds to what users do. An event fires when something happens — a button is clicked, a value changes, a page loads. A workflow is the sequence of actions that runs in response.

---

## Events

Every component in Scram exposes a set of built-in events relevant to what it does. A button has an **onClick** event. An input has an **onChange** event. A page has an **onLoad** event. These are the hooks you attach workflows to.

You connect a workflow to an event in the **Logic tab** of the Component Editor — select the component, open Logic, and add a workflow to the event you want to respond to.

### Custom events with Emit Event

Components you build yourself can emit custom events using the **Emit Event** action. This is how a child component tells its parent that something happened — for example, a custom form component emitting an `onSubmit` event when the user completes it.

### How Scram events propagate

Scram events work differently from standard DOM events — they do not bubble up the component tree automatically. A few key things to understand:

**Events are component-to-parent only.** When a component emits an event, only its immediate parent can listen for it. The event does not travel further up the tree.

**Stop Propagation** is an option in the Emit Event action and is on by default. This is more of a safeguard than a true bubble-stop — since events don't bubble in Scram anyway, it reinforces the one-level boundary.

**For communicating further up the tree**, use page variables instead. A child component can set a page variable; a parent component or page workflow can react to that variable changing.

<Note>
  Think of Scram events as a one-level notification system, not a bubbling chain. Child tells parent — that's it.
</Note>

---

## Workflows

A workflow is a sequence of one or more **actions** that runs in response to an event. Workflows execute top to bottom, step by step.

There are two kinds of workflow in Scram:

**Page and component workflows** — attached directly to a page event (like page load) or a component event (like a button click). These are created and edited in the [Workflow Editor](/understanding/subpages/workflow-editor) and are scoped to the page they live on.

**Reusable workflows** — defined once and callable from any other workflow in your project. Useful for logic you want to share across pages — for example, a standard email notification or a common data validation pattern. See [Workflows](/resources/workflows) in the Resource View for more detail.

---

## Actions

Actions are the individual steps inside a workflow — the things that actually happen. Scram provides a full library of built-in actions covering database queries, variable management, navigation, authentication, file handling, and more.

See the [Action Directory](/actions/action-directory) in the Reference section for the full list.

---

## Workflow authorisation

Workflows can be restricted to logged-in users or specific roles. By default, a workflow inherits the authorisation settings of the page it's on. You can override this per workflow.

See [Workflow Auth](/understanding/subpages/workflow-auth) for full details.