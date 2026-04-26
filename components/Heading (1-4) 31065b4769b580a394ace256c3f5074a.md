# Heading (1-4)

Scram provides four heading components, mapping directly to the HTML heading hierarchy (`h1`–`h4`). Each renders as the correct semantic HTML element and arrives pre-styled with theme-aware typography — the right size, weight, colour, and font for its level in the hierarchy.

---

## The Heading Hierarchy

| **Component** | **ID** | **HTML element** | **Font size** | **Font weight** | **Colour** |
| --- | --- | --- | --- | --- | --- |
| **Heading 1** | `pla_heading` | `<h1>` | `theme.text.xxxxxl` | 700 | `neutral[950]` |
| **Heading 2** | `pla_heading2` | `<h2>` | `theme.text.xxxxl` | 700 | `neutral[950]` |
| **Heading 3** | `pla_heading3` | `<h3>` | `theme.text.xxl` | 700 | `neutral[900]` |
| **Heading 4** | `pla_heading4` | `<h4>` | `theme.text.xl` | 600 | `neutral[800]` |

All four share the same foundational defaults:

- **Font family:** `theme.font.heading`
- **Line height:** `1.2`
- **Text align:** `left`
- **Margin / padding:** `0` (no browser default spacing)

Colour steps down subtly from Heading 1 (`neutral[950]`, near black) to Heading 4 (`neutral[800]`, slightly softer), creating a gentle visual hierarchy without changing the font family or switching to a different colour entirely.

---

## Shared Style Properties

All four heading components expose the same set of overridable styles:

| **Property** | **Description** |
| --- | --- |
| `color` | Text colour. Defaults to a shade of `neutral` appropriate to the heading level. |
| `fontFamily` | Defaults to `theme.font.heading`. Override to use the body font or a custom stack. |
| `fontWeight` | `700` for H1–H3, `600` for H4. |
| `fontStyle` | `normal` by default. Set to `italic` for emphasis. |
| `fontSize` | Defaults to the theme text scale size for each level. |
| `lineHeight` | `1.2` — tight, appropriate for large display text. |
| `textAlign` | `left` by default. |
| `textTransform` | `none` by default. Set to `uppercase`, `lowercase`, or `capitalize`. |
| `textOverflow` | `clip` by default. |
| `textWrap` | `wrap` by default. |
| `opacity` | `1` by default. |
| `margin` / `padding` | Both `0` by default. |

---

## Shared Events

All four heading components respond to the same events:

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks the heading |
| `doubleClick` | User double-clicks the heading |
| `mouseEnter` | Pointer enters the heading |
| `mouseLeave` | Pointer leaves the heading |

---

## Setting the Text

Heading text is set directly as the component's text content — type it into the component in the editor, or bind it to a dynamic expression such as `current.data.title` or `page.data.article.value.headline`.

> ***Text components cannot have child components.** You cannot place an icon or another component inside a heading. To show an icon alongside a heading, place both inside a flex Container.*
> 

---

## Choosing the Right Level

Heading levels communicate document structure to browsers, search engines, and screen readers — not just visual size.

| **Level** | **When to use** |
| --- | --- |
| **H1** | The single main title of the page. Use only once per page. |
| **H2** | Major sections of the page. |
| **H3** | Sub-sections within an H2 section. |
| **H4** | Minor sub-sections, card titles, sidebar headings. |

Don't skip levels (e.g. jumping from H1 directly to H4) for visual effect — adjust `fontSize` in the style panel instead.

---

## Semantic HTML Note

The Scram editor also allows you to drop a plain `h1`–`h6` HTML tag, which maps automatically to the corresponding Heading component. `h4`, `h5`, and `h6` all map to `pla_heading4` — use `pla_heading4` directly when you need any of those levels, and adjust the font size as needed for H5 and H6.