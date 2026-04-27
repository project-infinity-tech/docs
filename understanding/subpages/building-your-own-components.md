---
title: "Building Your Own Components"
---

# Building Your Own Components

A **component definition** is a reusable UI blueprint. You build it once, then place instances of it anywhere in your app — on any page, inside other components, inside Repeaters.

Every instance shares the same structure and behaviour. When you update the definition, every instance updates with it.

Think of it like designing your own platform component. Once defined, it sits in your component palette alongside the built-in ones.

---

## When to Build One

The clearest signal is repetition. If you'd like to reuse the same layout in two or more places, make it a component definition instead.

Good candidates include:

- **List items and cards** — anything used inside a Repeater
- **Page headers and section titles** — consistent structure across pages
- **Navigation bars and footers** — shared across every page
- **Status indicators** — a badge or chip with consistent logic
- **Form field groups** — a label, input, and error message packaged together

If you find yourself copying and pasting a group of components, that's the moment to extract them into a definition.

---

## Properties

Properties are how a component definition accepts input from the outside. They make each instance configurable without changing the underlying definition.

A user card definition might have properties for `name`, `role`, `avatarUrl`, and `isOnline`. Whoever places the card sets those values — either as literals or as expressions like `current.data.name` when used inside a Repeater.

Inside the definition, you reference properties as `props.name`, `props.role`, and so on.

Properties have types (text, number, boolean, date, enum, and more) and can have default values so instances work sensibly out of the box.

---

## Variables

Component definitions can also have their own internal **variables** — mutable state that lives within each instance.

An accordion item might have an `isOpen` boolean variable. A rating widget might track the `selectedRating`. This state is private to each instance by default.

Variables can optionally be **exposed**, which makes them readable from outside the component — from page-level expressions or workflows using `components.componentId.vars.variableName`. Use this when the rest of the page needs to know something about the component's state (for example, reading the current value of a custom input).

---

## Events

Events are how a component definition communicates back to the page.

A custom button component might emit a `click` event. A custom input might emit a `committedChange` event with the entered value as the payload. A data card might emit a `select` event when clicked.

Whoever uses the component can attach a workflow to those events, just like they would with a platform component. The event carries a payload — whatever data the component passes out — which the workflow can access via `trigger.payload`.

This is the clean separation between what a component *does internally* and what the *page does in response*.

---

## Slots

Component definitions can expose **slots** — regions where the person using the component can inject their own content.

A layout component might expose a `header` slot and a `content` slot. A modal wrapper might expose a `body` and a `footer`. The definition controls the overall structure; the slots let each instance customise the parts that vary.

Inside the definition, you mark where a slot's content should appear using a `Slot` placeholder with a name. When someone uses the component, they fill that slot with whatever components they need.

---

## The Two Types of Definition

**UI components** are the default. You build them visually, the same way you build a page — placing and arranging components, wiring up interactions. This covers the vast majority of use cases.

**React components** are for advanced cases where you need to write custom code or use external libraries — a specialised chart, a third-party integration, something that can't be achieved with the standard building blocks. These are written as React component code directly.

Start with UI unless you have a specific reason to use React.

---

## Instances vs. the Definition

When you place a component definition on a page, you're creating an **instance**. The instance inherits everything from the definition — its structure, its default styles, its behaviour.

You can override individual properties on each instance to customise it, but the underlying layout and logic come from the definition.

This means: edit the definition to change behaviour everywhere. Edit an instance's properties to customise just that one.

---

## Key Things to Know

**Definitions are app-wide.** A component defined in your app is available on every page of that app.

**Instances inside Repeaters are not individually addressable.** You can't reference a specific card inside a Repeater by its component ID. Design your components to be self-contained, using `current.data` and events to communicate rather than relying on external references.

**Keep definitions focused.** A component that does one thing well is easier to reuse and maintain than one that tries to handle every case. Use properties and slots to handle variation rather than building every variant into the definition itself.

---

## Related

- [Understanding Slots →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Understanding the Repeater →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Component Variables →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Working with Events →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)