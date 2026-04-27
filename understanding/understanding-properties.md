---
title: "Understanding Properties"
---

Properties (or "props") are how you configure a component — what it shows, how it behaves, and how it looks. They live on components: both the platform components Scram provides and any custom components you build yourself.

---

## Props vs Variables

The key distinction is direction:

- **Props** are inputs *into* a component — they tell it what to display or how to behave
- **Variables** are state the component holds and can change over time — like whether a menu is open, or what a user has typed

A prop says "show this." A variable remembers "this happened."

---

## Static vs dynamic values

Props can hold two types of value:

**Literal values** — fixed text, numbers, colours. The label on a button, the placeholder above a field. This is the most common starting point when setting things up.

**Expressions** — props can also be wired to live data. A button label that changes based on whether a form is saving. An icon colour that reflects a status. Anything available on the page — variables, logged-in user data, database results — can be used as a prop value. Expressions re-evaluate automatically whenever the underlying data changes.

<Warning>
  Avoid using values that change on every render — like the current timestamp or a random number — directly in a prop expression. Since expressions re-run on every render, using something like `new Date()` in a prop can cause an infinite update loop. Compute those values once in a workflow and store them in a variable instead.
</Warning>

---

## Default values

Most platform components come with sensible defaults already set — a button says "Click Me", an icon picks a theme colour, an input has placeholder text. You don't have to configure anything to get something that works. Setting props is just overriding those defaults when you need something specific.

---

## Props on custom components

When you build your own component, you define its props yourself. This is how you make a component reusable — instead of hardcoding a title or colour inside the component, you expose them as props so each instance can be configured differently.

<Note>
  For more on this, see the component building section.
</Note>

---

## Discovering props on platform components

Different platform components expose different props — a button has different options to a date picker or a data table. The best way to see what's available is to select a component on the canvas and check the **Properties panel**, which lists everything that component supports.