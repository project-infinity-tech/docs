# Text

## Overview

**Text** is the standard component for body copy in Scram. It renders as a rich text block — a `<p>`-equivalent element that supports inline formatting (bold, italic, links), markdown, multi-paragraph content, and dynamic expressions. It is the right choice for any running prose: descriptions, instructions, labels, article content, and UI copy.

---

## Default Styles

Text arrives pre-styled for readable body copy:

| **Property** | **Default** |
| --- | --- |
| `fontFamily` | `theme.font.body` |
| `fontSize` | `theme.text.md` |
| `fontWeight` | `400` |
| `fontStyle` | `normal` |
| `lineHeight` | `1.5` — comfortable for reading |
| `textAlign` | `left` |
| `color` | `neutral[950]` |
| `textTransform` | `none` |
| `textOverflow` | `clip` |
| `textWrap` | `wrap` |
| `padding` | `0` |
| `margin` | `auto` |

---

## Style Properties

All of the above defaults can be overridden in the styles panel. Common overrides:

- **`color`** — for muted secondary text (`neutral[500]`), error text (`error[600]`), or inverted white text on dark backgrounds.
- **`fontSize`** — for smaller helper text (`theme.text.sm`) or larger introductory copy (`theme.text.lg`).
- **`fontWeight`** — `600` or `700` to bold a paragraph without switching to a heading.
- **`textAlign`** — `center` for callout text, `right` for metadata.
- **`lineHeight`** — increase to `1.75` or `2` for very small text that needs more breathing room.

---

## Rich Text & Markdown

Text supports **markdown formatting** in its content. Use the text editor in the component panel, or set the content as a markdown expression:

| **Markdown syntax** | **Result** |
| --- | --- |
| `**bold**` | **bold** |
| `*italic*` | *italic* |
| `- item` | Bullet list |
| `1. item` | Numbered list |
| ` ``code ``` | `inline code` |

Dynamic expressions can be embedded inline within markdown content using `{expression}` syntax — for example: `**Hello {user.givenName}!** You have *{count}* messages.`

---

## Multi-Paragraph Behaviour

When a Text component contains more than one paragraph, Scram's CSS adds `0.5rem` vertical spacing between paragraphs automatically. A single-paragraph Text has no top or bottom margin.

---

## Events

| **Event** | **Fires when…** | **Payload** |
| --- | --- | --- |
| `click` | User clicks the text block | Available |
| `doubleClick` | User double-clicks | Available |
| `mouseEnter` | Pointer enters | Available |
| `mouseLeave` | Pointer leaves | Available |
| `contextMenu` | User right-clicks | Available |

---

## Key Points

- **Text cannot contain child components.** It is a text-only element. To place an icon alongside text, use a flex Container with both an Icon and a Text component inside.
- **Text uses the body font by default** (`theme.font.body`), not the heading font. This keeps it distinct from heading components without needing manual font overrides.
- **`flex: none`** is applied internally, so Text never stretches to fill extra space in a flex layout — it only takes the width its content requires.

##