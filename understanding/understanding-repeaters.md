---
title: "Understanding Repeaters"
---

# Understanding Repeaters

The Repeater is how you display lists of things. Search results, order history, team members, product cards — any time you need to show the same layout across multiple items of data, use a Repeater.

---

## What it Does

The Repeater takes an **array of data** and renders a template — the content in its `render` slot — once for every item in that array.

You design the layout once. Scram handles the repetition.

If your data has 12 items, you get 12 copies of your template, each populated with its own item's values. If the data changes (because a filter was applied, or new records were loaded), the Repeater updates automatically.

---

## Setting Up the Data

The Repeater's `data` property expects an array. This is usually:

- A page data variable loaded on page open: `page.data.products.value`
- A page variable updated by a workflow: `vars.searchResults`
- A filtered or transformed version of either: `page.data.products.value.filter(p => p.active)`

The array can contain anything — rows from your database, items from an API response, or a simple list you've defined yourself.

---

## Inside the Render Slot

Every component you place inside the `render` slot has access to a special context variable: **`current`**.

- `current.data` — the data for the item currently being rendered
- `current.index` — the position of this item in the array (starting from 0)

So if your array contains products with a `name` and `price` field, inside the render slot you'd display them as `current.data.name` and `current.data.price`.

You design one card, one row, one list item — and `current.data` fills it with the right values for each repetition.

---

## The Empty State Slot

The `emptyState` slot is what renders when the data array is empty or hasn't loaded yet.

Always fill this slot. An empty Repeater with no empty state just shows a blank space — which looks broken to the user. Use it to show a friendly message like "No results found" or "You haven't added anything yet."

---

## Nested Repeaters

You can place a Repeater inside another Repeater's render slot. This is useful for things like a list of orders, each containing a list of line items.

Inside a nested Repeater, `current.data` refers to the *inner* item. To access the *outer* item, use **`parentRepeater.current.data`**.

For a third level of nesting, use `parentRepeater.parentRepeater.current.data`.

---

## Repeaters and Workflows

Components inside a Repeater's render slot can trigger workflows — a button on each card might let the user delete or edit that item.

Inside those workflows, use **`trigger.payload`** or **`current.data`** to identify which item was acted on.

> *⚠️ Components inside a Repeater cannot be addressed by their component ID from outside the Repeater. Don't try to reference `components.someCardId.vars.value` from a page-level workflow — it won't work. Use `current.data` or pass values through the trigger instead.*
> 

---

## Layout and Styling

The Repeater itself doesn't have style properties — it's a pure data mechanism, not a visual container. To control how the repeated items are arranged (as a vertical list, a horizontal row, a grid), **wrap the Repeater in a container** and apply your layout styles there.

This keeps the Repeater's role clean: it handles repetition, the container handles presentation.

---

## A Typical Pattern

1. Load an array of data via a page data workflow or a user-triggered fetch
2. Place a Repeater on the page, set its `data` to that array
3. Design your item layout inside the `render` slot using `current.data` for values
4. Add an empty state to the `emptyState` slot
5. Wrap the Repeater in a styled container to control spacing and layout

---

## Related

- [Understanding Slots →](Understanding%20Slots%2031065b4769b580c5bdefffda10d2a218.md)
- [Understanding Workflows, Triggers and Events →](Understanding%20Events,%20Triggers%20and%20Workflows%2031065b4769b58082ab60db6643f516f1.md)
- [Understanding Page Data →](Understanding%20Page%20Data%2011465b4769b58003a439c9df2ab13a9d.md)
- [Understanding Expressions →](Understanding%20Expressions%2015965b4769b580aab433dc5ea4a9f19d.md)