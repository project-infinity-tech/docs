---
title: "repeater"
---

# Repeater

## Overview

The **Repeater** renders a template of components once for every item in an array of data. Give it a list — from a database query, an API response, or a page variable — and it stamps out a copy of its contents for each entry, automatically injecting that entry's data into each copy.

It is the standard way to render any dynamic list in Scram: product cards, search results, table rows, notification feeds, user lists, and so on.

---

## How It Works

1. You provide an **array of data** via the `data` property.
2. You design **one item** inside the `render` slot — this is your template.
3. The Repeater renders that template **once per item**, making each item's fields available inside via the `current` context.
4. Optionally, you design a **fallback** inside the `emptyState` slot that shows when the array is empty.

```text
data = [ {name: "Alice"}, {name: "Bob"}, {name: "Carol"} ]

┌─ render slot (repeated) ──────────┐
│  <p>{current.data.name}</p>       │  → Alice
│                                   │  → Bob
│                                   │  → Carol
└───────────────────────────────────┘
```

---

## Properties

| **Property** | **Type** | **Description** |
| --- | --- | --- |
| **Data** (`data`) | Array | The array to iterate over. Accepts any array expression — database results, API responses, page variables, or inline arrays. |
| **Preview Repetitions** (`previewRepetitions`) | Number | How many times the render slot previews in the editor when no real data is connected yet. Defaults to `1`. Increase this to see how a multi-item layout looks while designing. |
| **Repeating Content** (`render`) | Slot | The template components that repeat for each item. Access the current item's data inside this slot via `current.data`. |
| **Empty State** (`emptyState`) | Slot | Components shown when `data` is empty or `null`. Use this to display a "No results found" message or a prompt to add the first item. |

---

## Accessing Data Inside the Render Slot

Inside the `render` slot, five special context objects are available:

| **Expression** | **Type** | **Description** |
| --- | --- | --- |
| `current.data` | Object | The data item for this particular repetition (e.g. `current.data.name`, `current.data.price`) |
| `current.index` | Number | Zero-based position of this item in the array (0, 1, 2…) |
| `repeater.data` | Array | The full array passed to `data` — useful for showing totals or counts |
| `repeater.prev` | Object | The previous item in the array |
| `repeater.next` | Object | The next item in the array |

---

## Nested Repeaters

Repeaters can be nested inside one another. There is one rule for `current`, and it holds everywhere:

<Info>
  `current` refers to the closest ancestor Repeater, whenever you are inside that Repeater's **Repeating Content** slot.
</Info>

That rule applies to every component equally, including a Repeater nested inside another Repeater. It is worth reading carefully, because nested Repeaters are where people expect it to bend, and it does not.

### Why a Repeater's own properties look like an exception

A Repeater's properties, including its **Data** field, are not inside that Repeater. They sit alongside it, in whatever slot the Repeater itself lives in.

So a nested Repeater's Data field is inside the **outer** Repeater's Repeating Content, exactly like any sibling text element. It resolves `current` the same way they do: to the outer item.

Nothing inside a Repeater component ever points at that Repeater's own `current`. Its items do not exist until its Data has resolved, so there is nothing to point at.

### Worked example

An array of animals, where each animal has a `prey` list of more animals.

```text
animals = [
  { name: "Lion", prey: [{ name: "Antelope" }, { name: "Zebra" }] },
  { name: "Hawk", prey: [{ name: "Mouse" }] }
]
```

**Outer Repeater**, Data property:

```text
vars.animals
```

**Inner Repeater**, Data property. This field lives in the outer Repeater's Repeating Content, so `current.data` is the animal:

```text
current.data.prey
```

**Inner Repeater**, Repeating Content. Now you are inside the inner Repeater, so `current.data` is the prey animal:

```text
{current.data.name}   → "Antelope"
```

To reach the outer animal from inside the inner Repeating Content, use `parentRepeater`:

```text
{parentRepeater.current.data.name}   → "Lion"
```

### Reaching further up

`parentRepeater` is relative to whatever `current` means where you are typing. From inside a Repeating Content slot it reaches the enclosing Repeater's item. From a Repeater's Data property, where `current` is already the outer item, it reaches one level above that.

| **Expression** | **In Repeating Content** | **In a Repeater's Data property** |
| --- | --- | --- |
| `current.data` | This Repeater's item | The enclosing Repeater's item |
| `parentRepeater.current.data` | The enclosing Repeater's item | Two levels up |

For deeper nesting the reference chains: `parentRepeater.parentRepeater.current.data`.

<Note>
  `parentRepeater` is only available where there is an ancestor Repeater to reach. In a nested Repeater's Data property, `current` is already the outer item, so `parentRepeater` there refers to a Repeater outside the outer one.
</Note>

### Typing and casts

If your data comes from a declared project type, the shape carries through and you can access fields directly with no type assertion:

```text
current.data.prey
```

Type assertions such as `(current.data as {prey: any[]}).prey` are only needed where the shape is genuinely unknown. If you find yourself writing one, check whether the source type can be declared properly instead. It is almost always clearer.

### Typing and casts

If your data comes from a declared project type, the shape carries through and you can access fields directly with no type assertion:

```text
current.data.prey
```

Type assertions such as `(current.data as {prey: any[]}).prey` are only needed where the shape is genuinely unknown. If you find yourself writing one, check whether the source type can be declared properly instead. It is almost always clearer.

---

## Layout

The Repeater itself has **no style properties** — it produces no wrapper element of its own. To control how repeated items are laid out (grid, list, horizontal scroll, etc.), wrap the Repeater in a container and style that container:

```text
// A three-column card grid
<div style={{ display: 'flex', flexWrap: 'wrap', columnGap: theme.spacing.md, rowGap: theme.spacing.md }}>
  <Repeater data={page.data.products.value}>
    <ProductCard slot="render" title={current.data.name} />
  </Repeater>
</div>
```

---

## Workflows Inside the Render Slot

Workflows attached to components inside the render slot (e.g. a button click on each card) run in the context of that item's repetition. Use `current.data` to access the item's fields — **do not** try to reference the repeated component by its ID from outside the Repeater, as repeated component instances are not individually addressable.

---

## Key Points

- **Always wrap for layout.** The Repeater emits no container element. Put it inside a flex or grid container to control spacing and flow.
- **Empty state is optional but recommended.** Without it, an empty array renders nothing — which can look like a bug to users.
- **`current` is only available inside the render slot.** It cannot be referenced from outside the Repeater.
- **Components inside a Repeater are not addressable by ID.** Expressions like `components.someChildId.vars.value` will fail. Read values via `current.data` or `trigger.payload` in workflows instead.
- **Repeater does not paginate automatically.** If your data source returns thousands of rows, handle pagination in your query and expose page controls separately.