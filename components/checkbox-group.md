# Checkbox Group

## Overview

**Checkbox Group** is a container for a set of related checkboxes that allows the user to select multiple options simultaneously. It renders a labelled group of checkboxes from a repeating data source and fires a single `commitedChange` event whenever any checkbox in the group is toggled, reporting the full old and new selection state.

---

## Structure

```
┌─ Checkbox Group ─────────────────┐
│  Group heading (optional)        │
│                                  │
│  ☑  Option A                     │
│  ☐  Option B                     │
│  ☑  Option C                     │
│  ☐  Option D                     │
└──────────────────────────────────┘
```

Checkboxes are stacked vertically with `theme.spacing.xxs` gap between them.

---

## Events

| **Event** | **Fires when…** | **Payload** |
| --- | --- | --- |
| `commitedChange` | Any checkbox in the group is toggled | `newValues`, `oldValues`, `componentId`, `componentName`, `timestamp` |
| `click` | Group area is clicked | Available |
| `doubleClick` | Group area is double-clicked | Available |
| `mouseEnter` | Pointer enters the group | Available |
| `mouseLeave` | Pointer leaves the group | Available |

The `commitedChange` payload includes both `newValues` and `oldValues` as objects, letting you compare before and after states in a workflow.

> ***Note:** The event name is `commitedChange` (one 't') — not `committedChange` as on the individual Checkbox. Use the exact spelling when wiring workflows.*
> 

---

## Key Points

- **Checkbox Group uses a Repeater internally.** Individual checkboxes are not addressable by component ID from outside the group. Respond to selections through the group's `commitedChange` event.
- **There are no exposed variables** on Checkbox Group. Unlike the individual [Checkbox](Checkbox%2031065b4769b58075b53bf9ffb338b3fa.md)'s `isChecked` variable, the group does not expose a readable selected-values state — capture selections in a page variable via the `commitedChange` workflow.
- **The group heading** is an `h3` element built into the structure. Set its text content to label the group for users and screen readers.
- **Spacing is fixed** at `theme.spacing.xxs` between checkboxes. The group itself has no overridable style properties — control its outer dimensions by wrapping it in a Container.
- **For single-select "choose one" scenarios**, use a set of individual Checkbox components with mutual exclusion logic in workflows, or use **Input Select** or **Chip Group** instead.