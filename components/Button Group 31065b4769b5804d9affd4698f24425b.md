# Button Group

### Overview

Button Group renders a set of related buttons as a single cohesive unit. All buttons in the group share the same `size`, `variant`, and `buttonTheme` — it is not possible to mix styles within one group. Use it for segmented controls, view toggles, media player controls, filter sets, and grouped form actions.

---

### Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| `buttons` | array of button objects | `[]` | Defines the buttons to render. See button object structure below. |
| `orientation` | enum | `horizontal` | `horizontal` (row) or `vertical` (column). |
| `size` | enum | `md` | `sm` / `md` / `lg` — applied to all buttons uniformly. |
| `variant` | enum | `solid` | `solid`, `outline`, `subtle`, `ghost` — applied to all buttons. |
| `buttonTheme` | enum | `neutral` | `primary`, `secondary`, `neutral`, `success`, `alert`, `error`. |
| `fullWidth` | boolean | `false` | Expands the group to 100% of parent width, distributing buttons evenly. |
| `disabled` | boolean | `false` | Disables all buttons simultaneously. |

---

### Button Object Structure

Each item in the `buttons` array is an object with these fields:

| **Field** | **Type** | **Required** | **Description** |
| --- | --- | --- | --- |
| `value` | text | ✅ | Unique identifier — this is what appears in `trigger.payload.value` when clicked. |
| `content` | text | ✅ (for `button` type) | The button label text. |
| `type` | enum | — | `button` (default) or `iconButton`. |
| `iconName` | IconName | ✅ (for `iconButton`) | Icon for icon-button type items. |
| `leadingIcon` | IconName | — | Icon before the label text. |
| `trailingIcon` | IconName | — | Icon after the label text. |
| `ariaLabel` | text | — | Accessible label (required when using `iconButton` type). |
| `disabled` | boolean | — | Disables this individual button only. |

```
[
  { content: "List",  value: "list",  leadingIcon: "List" },
  { content: "Grid",  value: "grid",  leadingIcon: "Grid" },
  { content: "Table", value: "table", leadingIcon: "Table" }
]
```

---

### Events

| **Event** | **Payload** | **Description** |
| --- | --- | --- |
| `buttonClick` | `{ value: string }` | Fires when any button in the group is clicked. |

The `value` in the payload matches the `value` field of the clicked button object. Access it in a workflow via `trigger.payload.value`.

---

### Handling Clicks in Workflows

**For 2 buttons (toggle):** use IfElse

```
<IfElse condition={trigger.payload.value === "list"}>
  <true>
    <step action="SetVariable" variable="vars.viewMode" value="list" />
  </true>
  <false>
    <step action="SetVariable" variable="vars.viewMode" value="grid" />
  </false>
</IfElse>
```

**For 3+ buttons:** use CaseSwitch

```
<CaseSwitch>
  <case condition={trigger.payload.value === "play"}>
    <step action="SetVariable" variable="vars.state" value="playing" />
  </case>
  <case condition={trigger.payload.value === "pause"}>
    <step action="SetVariable" variable="vars.state" value="paused" />
  </case>
  <case>
    <step action="SetVariable" variable="vars.state" value="stopped" />
  </case>
</CaseSwitch>
```

---

### Style Properties

| **Property** | **Default** |
| --- | --- |
| `borderRadius` | `theme.roundness.md` |
| `borderStyle` | `solid` |

Most visual styling is driven by `variant` and `buttonTheme` — override sparingly.

---

### Common Configurations

| **Use Case** | **`orientation`** | **`variant`** | **`buttonTheme`** | **`fullWidth`** |
| --- | --- | --- | --- | --- |
| View toggle (list/grid) | `horizontal` | `subtle` | `primary` | `false` |
| Media controls | `horizontal` | `outline` | `neutral` | `false` |
| Mobile bottom nav | `horizontal` | `ghost` | `neutral` | `true` |
| Filter bar | `horizontal` | `outline` | `secondary` | `false` |
| Form actions | `vertical` | `solid` | `primary` | `true` |

---

### Key Points

- **All buttons share the same theme, variant, and size** — you cannot mix styles within one group. Use separate Button components or multiple Button Groups for mixed styling.
- `value` fields must be **unique** within the array — they are the only way to identify which button was clicked.
- Individual buttons can be disabled via their object's `disabled` field, without disabling the whole group.
- `iconButton` type items require `iconName` and should always have `ariaLabel` for accessibility.
- Variables: **none** — there is no exposed selected/active state. Track selection yourself with a page variable updated in the `buttonClick` workflow.
- Aim for **3–7 buttons** per group for usability; beyond that, consider a different UI pattern.