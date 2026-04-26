# Button

### Overview

The Button is the primary interactive element for triggering actions. It is theme-aware, supports multiple visual weights, and can carry leading and trailing icons alongside its label text.

> *There is also a dedicated [**Icon Button**](Icon%20Button%2031065b4769b5803c848cfce590399575.md) (`pla_iconbutton`) for icon-only actions — documented separately below.*
> 

---

### Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| `content` | text | `"Click Me"` | The button label. Keep concise and action-oriented. |
| `type` | enum | `button` | HTML button type: `button`, `submit`, `reset`. Use `submit` inside forms. |
| `size` | enum | `md` | `sm` / `md` / `lg` — scales height, padding, and font size together. |
| `buttonTheme` | enum | `neutral` | Semantic colour: `primary`, `secondary`, `neutral`, `error`, `success`, `alert`. |
| `variant` | enum | `solid` | Visual weight: `solid`, `outline`, `subtle`, `ghost`. |
| `width` | enum | `fit` | `fit` = wraps content. `full` = 100% of parent. |
| `leadingIcon` | IconName | — | Icon displayed before the label text. |
| `trailingIcon` | IconName | — | Icon displayed after the label text. |
| `iconSize` | enum | `sm` | Size of leading/trailing icons. Usually matches or is one step smaller than button size. |

---

### Variants

The `variant` prop controls visual weight — use it to signal the relative importance of actions:

| **Variant** | **Appearance** | **Use when** |
| --- | --- | --- |
| `solid` | Filled background | Primary CTA, the most important action |
| `outline` | Transparent bg, coloured border | Secondary action alongside a solid button |
| `subtle` | Lightly tinted background | Tertiary action, low emphasis |
| `ghost` | Text only, no border or background | Inline or toolbar actions |

---

### Themes

The `buttonTheme` prop maps to semantic colour roles:

| **Theme** | **When to use** |
| --- | --- |
| `primary` | Main call-to-action |
| `secondary` | Supporting action |
| `neutral` | Default, general-purpose |
| `error` | Destructive actions (delete, remove) |
| `success` | Confirmation, completion |
| `alert` | Caution or warning actions |

---

### Events

| **Event** | **Description** |
| --- | --- |
| `click` | User clicks the button — the most common trigger for workflows |
| `doubleClick` | User double-clicks |
| `mouseEnter` | Cursor enters the button |
| `mouseLeave` | Cursor leaves the button |
| `blur` | Button loses focus |

---

### Style Properties

Key overridable styles (all size-aware defaults apply automatically):

| **Property** | **Default** |
| --- | --- |
| `width` | `fit-content` (or `100%` when `width="full"`) |
| `height` | Derived from `size` + theme spacing |
| `padding` | Derived from `size`; reduced if icons are present |
| `borderRadius` | `theme.roundness.md` |
| `fontFamily` | `theme.font.body` |
| `fontSize` | Derived from `size` |
| `background` | Derived from `variant` + `buttonTheme` |
| `color` | Derived from `variant` + `buttonTheme` |
| `borderWidth` | `theme.border.sm` (transparent unless `outline`) |

---

### Navigation

**The Button does not have a `link` prop.** To navigate on click, attach a frontend workflow to the `click` event with a **NavigateToPath** step. To wrap content as a navigation link, use the **Link** component (`pla_link`) instead.

---

### Key Points

- `type="submit"` makes the button submit the nearest HTML `<form>` — use this inside form layouts
- `type="reset"` clears all inputs inside the nearest `<form>`
- When `leadingIcon` or `trailingIcon` is set, padding automatically tightens on the icon side to maintain visual balance
- `width="full"` is useful for mobile layouts or full-width form submit buttons
- Variables: **none** — the Button has no exposed `vars`

---