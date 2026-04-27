---
title: "Understanding Slots"
---

Some components aren't just a single thing — they're a *structure* that holds other components. Slots are how you put content inside them.

---

## What is a Slot?

A **slot** is a named placeholder inside a component where you can place your own content.

Think of a Card component: it has a defined shape — a border, a shadow, rounded corners — but the *content* inside it is up to you. The card exposes slots for its different regions (header, body, footer, image) and you fill those slots with whatever components you need: text, buttons, avatars, data.

Without slots, every component would have to know exactly what content it contains. Slots separate the *structure* of a component from the *content* inside it.

---

## Default and Named Slots

Most components have more than one slot, each with a name that describes its purpose.

A **named slot** targets a specific region of a component. A Card might expose:

- `header` — for a title and actions
- `content` — for the main body
- `footer` — for metadata or buttons
- `image` — for a photo at the top

A **default slot** is the unnamed slot — the one that receives content when you don't specify a slot name. Many simple wrapper components have just one slot and it's the default.

When you drag a component *into* another in the editor, you're placing it into a slot. If the parent has multiple slots, you can choose which one to target.

---

## The Repeater's Slots

The **Repeater** is the most important slot-based component in Scram. It takes an array of data and renders its slot content once for each item.

It has two slots:

- **render** — the template that repeats. Every component you place here is rendered once per item in the data. Inside this slot, you use `current.data` to access the values for the current item.
- **emptyState** — what to show when the data array is empty. Use this to display a friendly "No results found" message rather than a blank space.

The render slot is what makes the Repeater powerful: you design the layout once, and Scram handles repeating it for every row of data.

---

## Slots in Custom Components

When you build your own reusable component definition, you can define your own slots — regions where the person using the component can inject content.

This is how you build truly flexible, composable components. A sidebar layout component might expose a `header` slot and a `content` slot. A modal might expose a `body` and a `footer`. The component defines the structure; the slots define where customisation is allowed.

---

## Key Things to Know

**Slots are structural, not stylistic.** A slot tells you *where* content goes, not what it looks like. Styling is still controlled by the components you place inside.

**Not all regions of a component are slots.** Some components have built-in content controlled by properties (like a button's label text). Slots are specifically for placing *other components* inside.

**Content in a slot belongs to the parent's context** — not the slot itself. Inside a Repeater's render slot, `current.data` is available because the Repeater provides it. Inside a custom component's slot, the page's variables and data are still accessible.

---

## Related

- [Understanding Components →](Understanding%20Components%202e165b4769b580caaef8e198d35eca87.md)
- [Using the Repeater →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Building Custom Component Definitions →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)