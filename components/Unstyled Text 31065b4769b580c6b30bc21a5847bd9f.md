# Unstyled Text

## Overview

**Unstyled Text** is an inline `<span>` element with minimal default formatting. Unlike [Text](Text%2031065b4769b5802c8c85c608bc93f88e.md) — which has full body copy styling baked in — Unstyled Text inherits almost nothing from the theme and starts as a near-blank slate. It is intended for situations where you need precise control over every typographic property, or where you are building a custom component definition and need a text primitive without opinionated defaults.

---

## Default Styles

| **Property** | **Default** |
| --- | --- |
| `fontFamily` | `sans-serif` (browser default, not theme) |
| `fontSize` | `medium` (browser default, not theme) |
| `fontWeight` | `500` |
| `fontStyle` | `normal` |
| `lineHeight` | `1` — tight, no extra leading |
| `textAlign` | `left` |
| `color` | `canvastext` (browser default) |
| `textWrap` | `wrap` |
| `width` | `auto` |
| `display` | `block` |
| `opacity` | `1` |
| `padding` | `0` |
| `margin` | `auto` |

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `fontFamily` | `sans-serif` |
| `fontStyle` | `normal` |
| `fontWeight` | `500` |
| `fontSize` | `medium` |
| `lineHeight` | `1` |
| `textAlign` | `left` |
| `textOverflow` | `clip` |
| `textWrap` | `wrap` |
| `textTransform` | `none` |
| `color` | `canvastext` |
| `userSelect` | `auto` |
| `pointerEvents` | `auto` |
| `cursor` | `auto` |
| `width` | `auto` |
| `padding` | `0` |
| `margin` | `auto` |

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks the text |
| `doubleClick` | User double-clicks |
| `mouseEnter` | Pointer enters |
| `mouseLeave` | Pointer leaves |
| `contextMenu` | User right-clicks |

---

## Text vs Unstyled Text

|  | **Text** | **Unstyled Text** |
| --- | --- | --- |
| HTML element | `<p>`-equivalent (RichText) | `<span>` |
| Theme font | ✅ `theme.font.body` | ❌ Browser `sans-serif` |
| Theme colour | ✅ `neutral[950]` | ❌ `canvastext` |
| Theme text size | ✅ `theme.text.md` | ❌ `medium` |
| Line height | `1.5` (readable) | `1` (tight) |
| Markdown support | ✅ Yes | ❌ No |
| Multi-paragraph | ✅ Yes | ❌ No |
| Use case | Body copy, descriptions, prose | Custom components, precise control |

---

## Key Points

- **Unstyled Text does not inherit theme values.** If you want body-copy styling, use [*Text*](Text%2031065b4769b5802c8c85c608bc93f88e.md). Use Unstyled Text only when you are manually setting every typographic property yourself.
- **It renders as `display: block`** despite being a `<span>`. This means it takes up its own line, not inline within surrounding text.
- **No markdown support.** Content is plain text only — dynamic expressions via `{expression}` syntax are supported, but no bold, italic, or list formatting.
- **`flex: none`** is applied internally, preventing it from stretching in flex layouts.