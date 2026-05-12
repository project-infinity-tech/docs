---
title: "Understanding Repeaters"
---

The Repeater is how you display lists of things. Search results, order history, team members, product cards — any time you need to show the same layout across multiple items of data, use a Repeater.

---

## What it Does

The Repeater takes an **array of data** and renders a template — the content in its `render` slot — once for every item in that array.

You design the layout once. Scram handles the repetition.

If your data has 12 items, you get 12 copies of your template, each populated with its own item's values. If the data changes — because a filter was applied or new records were loaded — the Repeater updates automatically.

---

## Setting Up the Data

The Repeater's `data` property expects an array. This is usually:

- A page data variable loaded on page open: `page.data.products.value`
- A page variable updated by a workflow: `vars.searchResults`
- A filtered or transformed version of either: `page.data.products.value.filter(p => p.active)`

The array can contain anything — rows from your database, items from an API response, or a simple list you've defined yourself.

---

## Inside the Render Slot

Every component you place inside the `render` slot has access to a special context variable: **`current`**.

- `current.data` — the data for the item currently being rendered
- `current.index` — the position of this item in the array (starting from 0)

So if your array contains products with a `name` and `price` field, inside the render slot you'd display them as `current.data.name` and `current.data.price`.

You design one card, one row, one list item — and `current.data` fills it with the right values for each repetition.

---

## The Empty State Slot

The `emptyState` slot is what renders when the data array is empty or hasn't loaded yet.

Always fill this slot. An empty Repeater with no empty state just shows a blank space — which looks broken to the user. Use it to show a friendly message like "No results found" or "You haven't added anything yet."

---

## Nested Repeaters

You can place a Repeater inside another Repeater's render slot. This is useful for things like a list of orders, each containing a list of line items.

Inside a nested Repeater, `current.data` refers to the inner item. To access the outer item, use `parentRepeater.current.data`. For a third level of nesting, use `parentRepeater.parentRepeater.current.data`.

---

## Repeaters and Workflows

Components inside a Repeater's render slot can trigger workflows — a button on each card might let the user delete or edit that item. Inside those workflows, use `trigger.payload` or `current.data` to identify which item was acted on.

<Warning>
  Components inside a Repeater cannot be addressed by their component ID from outside the Repeater. Don't try to reference `components.someCardId.vars.value` from a page-level workflow — it won't work. Use `current.data` or pass values through the trigger instead.
</Warning>

---

## Layout and Styling

The Repeater itself doesn't have style properties — it's a pure data mechanism, not a visual container. To control how the repeated items are arranged (as a vertical list, a horizontal row, a grid), **wrap the Repeater in a container** and apply your layout styles there.

This keeps the Repeater's role clean: it handles repetition, the container handles presentation.

---

## A Typical Pattern

<Steps>
  <Step title="Load your data">
    Fetch an array via a page data workflow or a user-triggered workflow and store it in a variable.
  </Step>
  <Step title="Place a Repeater">
    Add a Repeater to the page and set its `data` property to the array.
  </Step>
  <Step title="Design the item layout">
    Build your item template inside the `render` slot using `current.data` to reference each item's fields.
  </Step>
  <Step title="Add an empty state">
    Add a friendly message to the `emptyState` slot for when there's nothing to show.
  </Step>
  <Step title="Wrap in a container">
    Place the Repeater inside a styled container to control spacing, direction, and layout.
  </Step>
</Steps>

---

## Related

<CardGroup cols={2}>
  <Card title="Understanding Slots" href="/understanding/understanding-slots" />
  <Card title="Understanding Events and Workflows" href="/understanding/understanding-events-and-workflows" />
  <Card title="Understanding Page Data" href="/understanding/understanding-page-data" />
  <Card title="Understanding Expressions" href="/understanding/understanding-expressions" />
</CardGroup>