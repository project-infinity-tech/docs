# Progress Bar

## Overview

**Progress Bar** is a feature-rich horizontal bar that communicates task completion, upload status, loading state, or any value measured against a maximum. It goes well beyond the simpler [Meter](Meter%2031065b4769b580e39846dd009a44048b.md) component — offering animated transitions, four visual styles, optional percentage labels, a glow effect, and leading/trailing slots for adding custom content alongside the bar.

---

## Structure

```
[Label]

[Leading Slot]  ████████████░░░░░░░░░░░░░░  [Trailing Slot]
                 ↑ bar fills to value/max
```

Inside the bar track, a percentage label can optionally float in the centre. A hidden native `<progress>` element sits beneath for accessibility.

---

## Properties

### Value & Range

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Current Value** (`value`) | Text | `"50"` | How much of the task is complete. Passed as text — use `String(myNumber)` for dynamic values. |
| **Max Value** (`max`) | Number | `100` | The total amount representing 100% completion. |

The rendered fill is always clamped between 0% and 100% — values below 0 or above `max` do not overflow.

### Appearance

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Visual Style** (`variant`) | Enum | `solid` | The fill style of the bar. |
| **Size** (`size`) | Enum | `md` | The height of the bar track. |
| **Color** (`color`) | Colour | `primary[500]` | The fill colour of the bar. |
| **Track Color** (`trackColor`) | Colour | `neutral[50]` | The background track colour (the unfilled portion). |

### Variant Options

| **Value** | **Appearance** |
| --- | --- |
| `solid` | Plain flat fill in `color`. Clean and universal. *(default)* |
| `gradient` | Gradient fill using `color`. (Currently renders as a uniform colour — gradient endpoints use the same value.) |
| `striped` | Diagonal stripe pattern overlaid on `color`. Suggests ongoing activity. |
| `glow` | Flat fill with a coloured outer glow (`box-shadow`) using `color`. |

### Size Options

| **Value** | **Track height** |
| --- | --- |
| `sm` | `theme.spacing.xxxs` — very thin |
| `md` | `theme.spacing.xxs` — standard *(default)* |
| `lg` | `theme.spacing.xs` — prominent |

### Label

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Label** (`inputLabel`) | Text | *(unset)* | Optional text displayed above or beside the bar. |
| **Label Location** (`labelLocation`) | Enum | `top` | `top` places the label above; `left` places it to the left. |
| **Label Size** (`labelSize`) | Enum | `full` | Width of the label when positioned to the left. |

### Percentage Display

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Show Percentage** (`showPercentage`) | Boolean | `false` | Displays the rounded percentage (e.g. `63%`) centred over the bar. Text colour automatically switches from dark to light when the bar passes the 50% mark, to maintain contrast. |

### Animation

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Animated** (`animated`) | Boolean | `true` | When on, the bar width transitions smoothly whenever `value` changes. |
| **Animation Duration** (`animationDuration`) | Number (ms) | `300` | How long the transition takes in milliseconds. |

### Glow Effect

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Show Glow Effect** (`showGlow`) | Boolean | `false` | When on, a coloured glow appears when the bar exceeds 80%. Signals near-completion. |

> *When `variant` is set to `glow`, the glow is always visible at all values. When `showGlow` is `true` on any other variant, the glow only appears above 80%.*
> 

---

## Slots

| **Slot** | **Position** | **Typical Use** |
| --- | --- | --- |
| **Leading Section** | Left of the bar | Icon, step count, start label |
| **Trailing Section** | Right of the bar | Percentage text, remaining count, end label |

---

## Variables

| **Variable** | **Type** | **Exposed** | **Description** |
| --- | --- | --- | --- |
| `percentage` | Number (0–100) | ✅ Yes | The computed fill percentage: `(value / max) * 100`, clamped to 0–100. Read this to display the value elsewhere or trigger conditional logic. |

Access from outside: `components.progressId.vars.percentage`

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks the bar |
| `doubleClick` | User double-clicks |
| `mouseEnter` | Pointer enters |
| `mouseLeave` | Pointer leaves |
| `contextMenu` | User right-clicks |
| `blur` | Bar loses focus |
| `complete` | The value reaches 100% |
| `thresholdReached` | A threshold is crossed *(see note below)* |

> `*complete` and `thresholdReached` are declared events but their exact trigger conditions depend on value changes being driven externally. Wire a workflow to `complete` to trigger a celebration, unlock the next step, or mark a task done.*
> 

---

## Accessibility

A hidden native `<progress max={max} value={value}>` element is always rendered. It contains a text fallback reading `"{percentage}% complete"` for screen readers. No additional ARIA attributes are needed.

---

## Progress Bar vs Meter

|  | **Progress Bar** | **Meter** |
| --- | --- | --- |
| **Purpose** | Task completion, loading, upload progress | Gauge reading within a range |
| **Colour zones** | Single colour (changes via external logic) | Automatic low/mid/high colour switching |
| **Animation** | ✅ Built-in smooth transitions | ❌ None |
| **Percentage label** | ✅ Optional, centred on bar | ❌ Not available |
| **Glow effect** | ✅ Optional | ❌ Not available |
| **Slots** | ✅ Leading and trailing | ❌ None |
| **Visual variants** | Solid, gradient, striped, glow | Single solid bar |
| **Bar height** | sm / md / lg | Fixed thin (`theme.spacing.xxs`) |

Use **Progress Bar** when you are showing task completion or a loading process. Use [**Meter**](Meter%2031065b4769b580e39846dd009a44048b.md) when you are showing a measurement within a range with low/normal/high zones (CPU usage, battery, health score).

---

## Key Points

- **`value` must be a string.** Pass `String(myNumber)` or concatenate with `""` for dynamic values.
- **`percentage` is always 0–100**, regardless of what `value` is. Values outside `min`/`max` are clamped.
- **`animated: true` is the default.** The bar smoothly transitions width on every value change. Disable it with `animated: false` for instantaneous updates.
- **The percentage label colour is automatic.** Below 50% it shows dark (`neutral[700]`); above 50% it shows light (`surface[50]`) to maintain contrast against the filled bar.
- **Leading and trailing slots are flex items** in a row layout alongside the track. Use them for icons, step counts, or custom labels.