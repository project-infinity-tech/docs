# Icon Button

### Overview

A compact square button that displays only an icon — no text label. Designed for toolbars, actions within cards, close buttons, and anywhere a full button would be too large.

---

### Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| `iconName` | IconName | `XMark` | The icon to display. |
| `size` | enum | `sm` | `sm` / `md` / `lg` — controls the button's square dimensions. |
| `variant` | enum | `ghost` | `solid`, `outline`, `subtle`, `ghost` — same visual weight system as Button. |
| `buttonTheme` | enum | `neutral` | `neutral`, `primary`, `secondary`, `error`, `success`, `alert`. |
| `ariaLabel` | text | *(icon name)* | Screen reader label — **always set this** since there is no visible text. |

---

### Events

| **Event** | **Description** |
| --- | --- |
| `click` | User clicks the icon button |
| `blur` | Button loses focus |
| `doubleclick` | User double-clicks *(note: lowercase `c`, unlike Button's `doubleClick`)* |
| `mouseenter` | Cursor enters *(lowercase)* |
| `mouseleave` | Cursor leaves *(lowercase)* |

---

### Key Points

- The Icon Button is **always square** — width and height are equal, derived from `size`
- Default `variant` is `ghost` (unlike Button which defaults to `solid`) — appropriate for compact toolbar use
- Always provide a meaningful `ariaLabel` — without visible text, screen readers rely entirely on this
- Event names use **all-lowercase** (`doubleclick`, `mouseenter`, `mouseleave`) — different from Button's camelCase variants
- Variables: **none**

---

### Button vs Icon Button

|  | **Button (`pla_buttonv2`)** | **Icon Button (`pla_iconbutton`)** |
| --- | --- | --- |
| Label text | ✅ `content` prop | ❌ None |
| Icon | Optional (leading/trailing) | Required (`iconName`) |
| Shape | Pill/rectangle | Square |
| Default variant | `solid` | `ghost` |
| Default size | `md` | `sm` |
| Event casing | camelCase | all-lowercase |