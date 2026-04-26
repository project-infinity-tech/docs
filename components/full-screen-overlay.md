# Full Screen Overlay

## Overview

**Full Screen Overlay** covers the entire viewport with a semi-transparent backdrop and centres a dialog panel on top of it. It is the standard way to build modals, confirmation dialogs, image lightboxes, and any other content that should demand the user's attention before they continue.

---

## Structure

```
┌─────────────────────────────────────────────────────┐
│                                                     │
│   Semi-transparent backdrop (fixed, full viewport)  │
│                                                     │
│          ┌──────────────────────────┐               │
│          │   Dialog Slot            │               │
│          │   (your modal content)   │               │
│          └──────────────────────────┘               │
│                                                     │
└─────────────────────────────────────────────────────┘
```

Internally the component has two layers:

1. **Overlay Shadow** — a full-viewport `position: fixed` container with a dark semi-transparent background (`#0000003a`). This dims everything behind the overlay.
2. **Overlay Container** — a centred panel with a white card surface, sitting above the shadow at `z-index: 99`. This is where your dialog content lives.

---

## Slots

| **Slot** | **Description** |
| --- | --- |
| **Dialog Slot** | Place your modal content here — headings, body text, form inputs, action buttons, etc. |

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Open** (`overlayOpen`) | Boolean | *(unset)* | Controls whether the overlay is visible. Bind this to a page variable and toggle it from workflows to show and hide the overlay. |
| **Dialog width** (`dialogSize`) | Number | `700` | Maximum width of the dialog panel in pixels. The panel shrinks on smaller screens. |

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `background` | `transparent` |

The overlay wrapper is `position: fixed`, `width: 100vw`, `height: 100vh`, anchored to `top: 0, left: 0`. It always covers the full viewport regardless of scroll position.

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks anywhere on the overlay (including the backdrop) |
| `doubleClick` | User double-clicks |
| `mouseEnter` | Pointer enters the overlay area |
| `mouseLeave` | Pointer leaves the overlay area |
| `contextMenu` | User right-clicks |
| `blur` | Overlay loses focus |
| `ActionClose` | A close action is triggered from within the overlay |

---

## Showing and Hiding the Overlay

The overlay is shown or hidden by setting the `overlayOpen` property. The standard pattern is:

1. **Create a page [variable](Understanding%20Variables%2015a65b4769b580f49befef25a91812e5.md)** (e.g. `showModal`, type: boolean, default: `false`).
2. **Bind `overlayOpen`** to `vars.showModal`.
3. **Open the overlay** by setting `vars.showModal` to `true` in a workflow — typically on a button click.
4. **Close the overlay** by setting `vars.showModal` back to `false` — typically on a "Cancel" button inside the dialog slot, or on a `click` event on the overlay itself (clicking the backdrop to dismiss).

```
Button click → SetVariable vars.showModal = true  → overlay appears
Cancel click → SetVariable vars.showModal = false → overlay disappears
Backdrop click → SetVariable vars.showModal = false → overlay disappears
```

---

## Related Component: Overlay Container

**Component ID:** `pla_overlaycontainer`

The **Overlay Container** is the inner dialog panel used by Full Screen Overlay. It is a card-surfaced, vertically stacking container that sits at `z-index: 5` above the backdrop shadow.

You will rarely need to use it directly — it comes pre-embedded inside Full Screen Overlay. However, it is available as a standalone component if you need a positioned panel that floats above its parent without covering the entire viewport.

| **Style Property** | **Default** |
| --- | --- |
| `width` | `auto` |
| `maxWidth` | `auto` (constrained by `dialogSize` from the parent overlay) |
| `position` | `relative` |

---

## Key Points

- **Always use a page variable for `overlayOpen`**, not a hardcoded `true` or `false`. The overlay is only useful when you can toggle it dynamically from workflows.
- **Clicking the backdrop does not close the overlay automatically.** Wire the overlay's `click` event to a SetVariable step to implement backdrop-dismiss behaviour.
- **The overlay is always in the DOM.** When `overlayOpen` is false, use the component's visibility setting to hide it, rather than relying on `overlayOpen` alone — confirm how your specific setup handles this.
- **`dialogSize` is a maximum width**, not a fixed width. On narrow screens the panel will be narrower than the specified value.
- **Stack order:** The backdrop shadow sits at `z-index: 2`; the dialog panel at `z-index: 99`. If other components on the page use high `z-index` values, ensure they do not exceed `99` or they will appear over the dialog.