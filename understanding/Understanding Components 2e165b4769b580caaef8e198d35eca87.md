# Understanding Components

# Scram Components — Overview

A **Component** is the fundamental building block of every page in Scram. Every visible element you see on a page — a button, a text label, an image, a form input, a layout container — is a component.

---

## What is a Component?

A component is a **self-contained piece of UI** that has:

- **Appearance** — controlled by style properties (colours, spacing, typography, borders, etc.)
- **Content** — driven by props (static text, dynamic data from a variable or database, etc.)
- **Behaviour** — defined by events and workflows (what happens when a user clicks, types, hovers, etc.)
- **State** — stored in variables (e.g. an input's current value, whether a dropdown is open)

---

## Types of Components

### Platform Components

Built-in components provided by Scram. They cover the essentials:

- **Layout** — containers, dividers
- **Typography** — headings, text, unformatted text
- **Inputs** — text input, number input, email, password, checkbox, select, switch
- **Display** — image, icon, avatar, chip, badge
- **Navigation** — links, buttons
- **Data** — Repeater (for lists)
- **Overlays** — popovers, modals

### Custom Components (Component Definitions)

You (or the AI) can create **reusable component definitions** — your own design system building blocks. A definition is created once and can be placed on any page, any number of times. Changes to the definition propagate to every instance automatically.

There are two kinds of custom definitions:

- **UI components** — built visually inside Scram, composed from other components
- **React components** — written in code, for cases requiring external libraries (charts, maps, animations, etc.)

---

## Key Concepts

### [Props (or Properties)](Understanding%20Properties%202e165b4769b580e5bf42d53445e0ec69.md)

Props are the **inputs** to a component. They control what it displays or how it behaves. Props can be set to:

- A **literal value** (e.g. `"Submit"` as button text)
- A **dynamic expression** (e.g. `user.givenName` to show the current user's name)

### [Variables](Understanding%20Variables%2015a65b4769b580f49befef25a91812e5.md)

Variables are a component's **local state** — mutable values that can change at runtime. Platform inputs expose their state automatically (e.g. a text input exposes `vars.value`). Custom components can define their own variables.

Variables can be **exposed**, making them readable from outside the component via `components.componentId.vars.variableName`.

### Events & Workflows

Components emit **events** when something happens (a button is clicked, an input value changes, a form is submitted). A **workflow** is attached to an event to define what should happen in response — calling an API, updating a variable, navigating to a page, etc.

### [Slots](Understanding%20Slots%2031065b4769b580c5bdefffda10d2a218.md)

Some components accept **slots** — named regions where you can nest child components. For example, a card component might have a `header` slot and a `content` slot. Slots enable flexible composition without hardcoding a fixed structure.

### Styles

Styles control the visual appearance of a component. Scram uses a **theme system** so colours, spacing, typography, and roundness are consistent across the app. Styles can be overridden per-component, and responsive overrides can be set for **tablet** and **mobile** breakpoints independently.

---

## Component Instances vs. Definitions

|  | **Definition** | **Instance** |
| --- | --- | --- |
| **What it is** | The blueprint | A placed copy on a page |
| **Where it lives** | Component library | Inside a page or another component |
| **Edits affect** | All instances | Only that instance |
| **Customisable via** | Props, slots, events | Prop overrides on the instance |

---

## The Component Tree

Every page is structured as a **tree of nested components**. A container holds other containers or elements inside it. This tree structure determines both the visual layout and the inheritance of context (such as which Repeater a component belongs to).

---

In summary: components are the *what you see*, props and variables are the *what they contain*, and workflows are the *what they do*. Together, these three make a fully interactive, data-driven UI.

[Dynamic Prop setting on Components](Dynamic%20Prop%20setting%20on%20Components%201aa65b4769b580db92cbe119c2c94f19.md)

[Page Templates](Page%20Templates%2030f65b4769b580918cdfccb9dd90b28c.md)

[Component Directory](Component%20Directory%2030f65b4769b580e89859ee6b8b446a4d.md)