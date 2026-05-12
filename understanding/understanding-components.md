---
title: "Understanding Components"
---

A **Component** is the fundamental building block of every page in Scram. Every visible element you see on a page — a button, a text label, an image, a form input, a layout container — is a component.

---

## What is a Component?

A component is a self-contained piece of UI that has:

- **Appearance** — controlled by style properties (colours, spacing, typography, borders)
- **Content** — driven by props (static text, dynamic data from a variable or database)
- **Behaviour** — defined by events and workflows (what happens when a user clicks, types, hovers)
- **State** — stored in variables (e.g. an input's current value, whether a dropdown is open)

---

## Types of Components

### Platform Components

Built-in components provided by Scram. They cover the essentials:

- **Layout** — containers, dividers
- **Typography** — headings, text, unstyled text
- **Inputs** — text input, number input, email, password, checkbox, select, switch
- **Display** — image, icon, avatar, chip, badge
- **Navigation** — links, buttons
- **Data** — Repeater (for lists)
- **Overlays** — popovers, modals

See the [Component Directory](/components/component-directory) for the full reference.

### Custom Components

You can create reusable component definitions — your own design system building blocks. A definition is created once and can be placed on any page, any number of times. Changes to the definition propagate to every instance automatically.

There are two kinds of custom definitions:

- **UI components** — built visually inside Scram, composed from other components
- **React components** — written in code, for cases requiring external libraries (charts, maps, animations)

---

## Key Concepts

**[Props](/understanding/understanding-properties)** — the inputs to a component. They control what it displays or how it behaves. Props can be set to a literal value or a dynamic expression.

**[Variables](/understanding/understanding-variables)** — a component's local state. Platform inputs expose their state automatically (e.g. a text input exposes `vars.value`). Custom components can define their own variables, and these can be exposed so they're readable from outside the component.

**Events and Workflows** — components emit events when something happens (a click, a value change). A workflow attached to an event defines what should happen in response. See [Understanding Events and Workflows](/understanding/understanding-events-and-workflows).

**[Slots](/understanding/understanding-slots)** — named regions where you can nest child components. A card might have a `header` slot and a `content` slot. Slots enable flexible composition without hardcoding a fixed structure.

**Styles** — control the visual appearance of a component. Scram uses a theme system so colours, spacing, typography, and roundness are consistent across the app. Styles can be overridden per component, with separate responsive overrides for tablet and mobile breakpoints.

---

## Component Instances vs. Definitions

| | Definition | Instance |
|---|---|---|
| What it is | The blueprint | A placed copy on a page |
| Where it lives | Component library | Inside a page or another component |
| Edits affect | All instances | Only that instance |
| Customisable via | Props, slots, events | Prop overrides on the instance |

---

## The Component Tree

Every page is structured as a tree of nested components. A container holds other containers or elements inside it. This tree structure determines both the visual layout and the inheritance of context — such as which Repeater a component belongs to.

---

Components are the *what you see*, props and variables are the *what they contain*, and workflows are the *what they do*. Together, these three make a fully interactive, data-driven UI.

---

## Related

<CardGroup cols={3}>
  <Card title="Component Directory" href="/components/component-directory" />
  <Card title="Dynamic Prop Setting" href="/understanding/subpages/dynamic-prop-setting-on-components" />
  <Card title="Building Your Own Components" href="/understanding/subpages/building-your-own-components" />
</CardGroup>