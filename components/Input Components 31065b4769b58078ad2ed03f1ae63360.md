# Input Components

# Input Components

Scram provides seven purpose-built input components. All share a common set of conventions covered first, followed by individual reference entries for each.

---

## Common Conventions

All input components follow the same patterns:

### Labels

Every input supports an optional label with two placement options:

| **`labelLocation`** | **Behaviour** |
| --- | --- |
| `top` | Label sits above the field, full width of the input |
| `left` | Label sits to the left of the field, width controlled by `labelSize` |

`labelSize` controls the label's font size when `labelLocation` is `left`: `fit` · `sm` · `md` · `lg` · `full`.

### Reading Values

Every input exposes a `value` variable. **Read it directly** — do not create a page variable to mirror it.

```
components.inputId.vars.value
```

### Validation Errors

Every input exposes an `error` variable (type: text). Set it from a workflow to display a validation error message below the field:

```
SetVariable  →  components.inputId.vars.error  →  "This field is required"
```

Clear the error by setting it to an empty string.

### Description / Helper Text

Every input has a `description` property. Text set here appears as small helper copy below the field — instructions, format hints, character limits.

### Leading & Trailing Sections

Text Input, Email Input, Number Input, Password Input, and Textarea Input all support optional decorative sections on either side of the field:

| **Property** | **Description** |
| --- | --- |
| `showLeadingSection` | Must be `true` for the leading section to appear |
| `leadingIcon` | Icon shown on the left |
| `leadingBackground` | Adds a tinted background to visually separate the leading section |
| `showTrailingSection` | Must be `true` for the trailing section to appear |
| `trailingIcon` | Icon shown on the right |
| `trailingBackground` | Adds a tinted background to visually separate the trailing section |

> ***Both `showLeadingSection` / `showTrailingSection` must be enabled** before any icon or background appears, even if an icon is set.*
> 

### Two Change Events

Most inputs fire two events:

| **Event** | **Fires when…** | **Use for…** |
| --- | --- | --- |
| `everyChange` | Every keystroke as the user types | Live search, character count, real-time feedback |
| `committedChange` | When the user leaves the field (blur) or presses Enter | Form submission, validation, saving |

> *Password Input only has `committedChange` — for security, the value is never emitted on every keystroke.*
> 

## --

## Text Input

**Component ID:** `pla_textinput`

A single-line field for short free-form text — names, titles, search queries, URLs, and any other plain string.

### Properties

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `inputLabel` | *(unset)* | Field label |
| `inputPlaceholder` | `"Placeholder text"` | Hint shown when empty |
| `defaultValue` | *(unset)* | Initial value |
| `labelLocation` | `top` | Label placement |
| `labelSize` | `fit` | Label width (left placement) |
| `showClearButton` | `false` | Shows an ✕ button to clear the field. Best for search/filter inputs. |
| `iconSize` | `md` | Size of leading/trailing icons |
| Leading/trailing sections | — | See common conventions |

### Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `value` | Text | ✅ | Current text value |
| `error` | Text | ✅ | Validation error message |

### Events

`everyChange` · `committedChange` · `click` · `dblClick` · `mouseEnter` · `mouseLeave`

---

## Email Input

**Component ID:** `pla_emailinput`

A single-line field validated for email address format. Behaves like Text Input but its `value` variable is typed as `Email` rather than plain text, and it sets `type="email"` on the underlying input for mobile keyboard optimisation.

### Properties

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `inputLabel` | *(unset)* | Field label |
| `inputPlaceholder` | `"Enter your email"` | Hint shown when empty |
| `defaultValue` | *(unset)* | Initial value |
| `autocomplete` | `username` | Tells password managers how to treat this field. Use `username` for login email fields, `email` for other email fields. |
| `showClearButton` | `false` | Shows an ✕ clear button |
| `labelLocation` | `top` | Label placement |
| `labelSize` | `fit` | Label width |
| Leading/trailing sections | — | See common conventions |

### Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `value` | Email | ✅ | Current email value |
| `error` | Text | ✅ | Validation error message |

### Events

`everyChange` · `committedChange` · `click` · `doubleClick` · `mouseEnter` · `mouseLeave`

---

## Number Input

**Component ID:** `pla_numberinput`

A single-line field for numeric entry, with built-in increment/decrement spinner buttons and optional range constraints.

### Properties

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `inputLabel` | *(unset)* | Field label |
| `inputPlaceholder` | `"Placeholder Text"` | Hint shown when empty |
| `defaultValue` | *(unset)* | Initial numeric value |
| `range` | `any` | Constrains allowed values |
| `minimumValue` | *(unset)* | Hard minimum (overrides `range`) |
| `maximumValue` | *(unset)* | Hard maximum |
| `showClearButton` | `false` | Shows an ✕ clear button |
| `labelLocation` | `top` | Label placement |
| `labelSize` | `fit` | Label width |
| Leading/trailing sections | — | See common conventions |

### Range Options

| **Value** | **Allowed input** |
| --- | --- |
| `any` | Negative, zero, and positive numbers |
| `nonnegative` | Zero and above |
| `positive` | 1 and above |

### Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `value` | Number | ✅ | Current numeric value |
| `error` | Text | ✅ | Validation error message |

### Events

`everyChange` · `committedChange` · `click` · `mouseEnter` · `mouseLeave`

---

## Password Input

**Component ID:** `pla_passwordinput`

A field for entering passwords. The value is masked by default, with a show/hide toggle built in. Includes an optional strength meter. For security, the value is **never emitted on every keystroke** — only on `committedChange`.

### Properties

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `inputLabel` | *(unset)* | Field label |
| `placeholder` | `"Enter password"` | Hint shown when empty |
| `showStrengthMeter` | `false` | Displays a colour-coded strength bar at the bottom of the field |
| `autocomplete` | `current` | Tells password managers how to treat the field |
| `labelLocation` | `top` | Label placement |
| `labelSize` | `fit` | Label width |
| Leading/trailing sections | — | See common conventions. The trailing section is shown by default (`showTrailingSection: true`) to accommodate the show/hide eye icon. |

### Autocomplete Options

| **Value** | **Meaning** |
| --- | --- |
| `current` | This is an existing password (login form) |
| `new` | This is a new password (signup / change password form) |
| `off` | Disable autocomplete entirely |

### Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `value` | Text | ✅ | Current password value |
| `passwordStrength` | Number (0–100) | ✅ | Computed strength score. Based on length, uppercase, lowercase, digits, and special characters. |
| `passwordLength` | Number | ✅ | Character count of the current password |
| `error` | Text | ✅ | Validation error message |

### Strength Score Calculation

| **Score** | **Indicates** |
| --- | --- |
| 0–30 | Weak |
| 31–60 | Moderate |
| 61–90 | Strong |
| 91–100 | Very strong |

The score adds up to 60 points for length (4 points per character, up to 15 chars) and 10 points each for: lowercase letters, uppercase letters, digits, and special characters.

### Events

`committedChange` · `click` · `doubleClick` · `mouseEnter` · `mouseLeave`

> ***No `everyChange` event.** Read the live state from `components.passwordId.vars.value` if you need real-time access.*
> 

---

## Textarea Input

**Component ID:** `pla_textareainput`

A multi-line text field for longer content — comments, descriptions, bio text, notes. Resizable by the user by default.

### Properties

| **Property** | **Default** | **Description** |
| --- | --- | --- |
| `label` | *(unset)* | Field label |
| `placeholder` | `"Placeholder text"` | Hint shown when empty |
| `defaultValue` | *(unset)* | Initial value |
| `labelLocation` | `top` | Label placement |
| `labelSize` | `fit` | Label width |
| `size` | `md` | Overall size |
| Leading/trailing sections | — | See common conventions |

The textarea has a fixed `min-height: 120px` and is user-resizable. Font family inherits from the parent context; font size is `theme.text.md`.

### Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `value` | Text | ✅ | Current text value |
| `error` | Text | ✅ | Validation error message |

### Events

`everyChange` · `committedChange` · `click` · `doubleClick` · `mouseEnter` · `mouseLeave`

---

---

## Quick Reference

| **Component** | **Value type** | **Has `everyChange`?** | **Key variable** |
| --- | --- | --- | --- |
| Text Input | `text` | ✅ | `vars.value` |
| Email Input | `Email` | ✅ | `vars.value` |
| Number Input | `number` | ✅ | `vars.value` |
| Password Input | `text` | ❌ | `vars.value`, `vars.passwordStrength` |
| Textarea Input | `text` | ✅ | `vars.value` |
| Input Select | Array of objects | ❌ | `vars.selectedItems` |
| Date Picker | `datetime` | ❌ | `vars.selectedDate` |