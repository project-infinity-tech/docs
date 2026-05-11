---
title: "Understanding Reactive Programming"
---

Scram builds React apps under the hood, which means the frontend is **reactive** — components automatically update when the data they depend on changes. You don't need to manually tell the page to refresh or re-render anything.

---

## How It Works

When you bind a component property to a variable, the component watches that variable. If the variable changes, the component re-renders automatically — and so does any expression that references it.

A simple example: you have a page variable holding a user's first name, and you pass it into a text component as a prop. When the variable updates, the component instantly displays the new name. If you have three components all bound to the same variable, all three update at once.

---

## A More Complex Example

Say you're building an invoice management screen. You have a list of invoices in one component and a detail panel in another. Both are bound to a `currentInvoice` page variable.

When the user clicks an invoice in the list, a workflow sets `currentInvoice` to the selected item. The detail panel immediately updates to show that invoice's data, and the list highlights the selected row — without you writing any update logic. The reactivity handles it.

---

## What This Means in Practice

- **Variables drive the UI** — store the right data in variables and your components stay in sync automatically
- **Expressions recalculate** — any expression referencing a variable re-evaluates when that variable changes. A greeting that shows "Hello" when a name is empty and "Hello, Sarah" when it's set will switch automatically
- **Props are the link** — binding a component prop to a variable is what makes the component reactive to that data

<Tip>
  If a component isn't updating when you expect it to, check that its prop is actually bound to a variable — not set to a static value.
</Tip>

---

## Related

- [Understanding Variables](/understanding/understanding-variables)
- [Understanding Properties](/understanding/understanding-properties)
- [Understanding Expressions](/understanding/understanding-expressions)