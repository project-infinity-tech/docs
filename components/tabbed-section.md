# Tabbed Section

## Overview

**Tabbed Section** is a segmented tab bar control — a row of labelled tabs where one is active at a time. It renders the tab strip itself; you are responsible for showing and hiding the content panels beneath it based on the selected tab.

It is suited to switching between views, filtering content, or organising settings into named sections within a page.

---

## Structure

```
┌─────────────────────────────────────────────┐
│  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │  Tab 1   │  │  Tab 2   │  │  Tab 3   │   │  ← tab strip (this component)
│  └──────────┘  └──────────┘  └──────────┘   │
└─────────────────────────────────────────────┘

 ┌─────────────────────────────────────────────┐
 │  Content for the active tab                 │  ← you build this separately
 └─────────────────────────────────────────────┘
```

The active tab has a white (`surface[50]`) background with a subtle border. Inactive tabs are transparent. The strip sits on a `neutral[50]` pill background.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Tab Items** (`tabItems`) | Array of objects | 3 default tabs | The list of tabs to display. Each item has a `label` (display text) and a `value` (number identifier). |
| **Default Tab** (`defaultTab`) | Number | `1` | Which tab is active when the component first loads. Matches the `value` field of the desired tab. |

### Tab Items Structure

Each object in `tabItems`:

| **Field** | **Type** | **Description** |
| --- | --- | --- |
| `label` | Text | The text shown on the tab button |
| `value` | Number | A unique numeric identifier for this tab |

**Default value:**

```
[
  { "label": "Tab 1", "value": 1 },
  { "label": "Tab 2", "value": 2 },
  { "label": "Tab 3", "value": 3 }
]
```

---

## Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `currentTab` | Number | ❌ No | The `value` of the currently active tab. Initialised from `defaultTab`. Updated automatically when a tab is clicked. |

> **`*currentTab` is not exposed.** It cannot be read from outside the component via `components.id.vars.currentTab`. To drive content panels from the selected tab, you must use an alternative approach — see the Usage Pattern section below.*
> 

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `display` | `flex` |
| `aspectRatio` | `auto` |

The outer container is `width: fit-content` — the strip only occupies the width of its tabs. Place it inside a full-width container if you need it to span the page.

---

## Events

Tabbed Section has **no events** at the component level. Individual Tab Items fire a `click` event.

---

## Usage Pattern: Showing Tab Content

Because `currentTab` is not exposed, the standard approach is to use a **page variable** to track the active tab, updated via a workflow on each Tab Item's `click` event.

### Setup

1. **Create a page variable** (e.g. `activeTab`, type: number, default: `1`).
2. **Wire each Tab Item's `click` event** to a SetVariable step:
    
    ```
    Tab 1 click → SetVariable vars.activeTab = 1
    Tab 2 click → SetVariable vars.activeTab = 2
    Tab 3 click → SetVariable vars.activeTab = 3
    ```
    
    > *Tab Items are inside a Repeater internally, so they are not individually addressable by component ID from outside. Add the Tabbed Section to the page, then select each Tab Item directly in the component tree to wire its click event.*
    > 
3. **Show/hide content panels** using the `scram-visible` attribute bound to the page variable:
    
    ```
    Panel A: scram-visible = { vars.activeTab === 1 }
    Panel B: scram-visible = { vars.activeTab === 2 }
    Panel C: scram-visible = { vars.activeTab === 3 }
    ```
    

### Result

```
vars.activeTab = 2

Tab 1  [Tab 2]  Tab 3     ← Tab 2 highlighted

░░░░░░░░░░░░░░░░░         ← Panel A (hidden)
██████████████████        ← Panel B (visible)
░░░░░░░░░░░░░░░░░         ← Panel C (hidden)
```

---

## Tab Item (standalone)

**Component ID:** `pla_tabitem`

Tab Item is the individual button within a Tabbed Section. It renders as a `<label>` wrapping a hidden `<input type="radio">`, giving it native radio group semantics for accessibility.

It is used automatically inside Tabbed Section and rarely needs to be placed manually. Its key property is `isActive` — a boolean that controls whether it shows the active (white background) or inactive (transparent) style.

| **Property** | **Type** | **Description** |
| --- | --- | --- |
| `tabData` | Object `{label, value}` | The tab's label and identifier |
| `isActive` | Boolean | Whether this tab is the currently selected one |

**Event:** `click` — fires when the tab is clicked.

---

## Key Points

- **Tabbed Section only renders the strip.** Content panels are separate components that you show and hide using page variables and `scram-visible`.
- **`currentTab` is internal and not readable from outside.** Always track the active tab in a page variable via click workflows on the Tab Items.
- **Tab values are numbers**, not text. Use numeric comparisons (`vars.activeTab === 1`, not `=== "1"`).
- **The strip is `width: fit-content`** by default — it does not stretch full width automatically. Wrap it in a container with `width: 100%` if you need it to span the full page width.
- **Tabs use native radio input semantics** internally, which means keyboard navigation between tabs (arrow keys) works out of the box for accessibility.