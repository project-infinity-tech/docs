# HTML Element

### Overview

The HTML Element component renders any native HTML tag directly — `div`, `span`, `section`, `article`, `button`, `input`, `table`, `video`, `canvas`, and anything else the browser supports. It is the lowest-level building block in Scram, sitting beneath all platform components.

In practice, you rarely add an HTML Element explicitly. Scram automatically maps common semantic HTML tags to their appropriate components when you write JSX — for example, a `<div style={{display: 'flex'}}>` becomes a Container, and `<h1>` becomes a Heading. HTML Element is there when you need a tag that has no Scram equivalent.

---

### Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| `asHtmlTag` | text or enum | `div` | The HTML tag to render. Can be any valid HTML tag name (e.g. `section`, `article`, `canvas`, `video`, `table`). |
| `hasTextContent` | boolean | `false` | When `true`, the component renders inline text content rather than child components. |
| `textContent` | InlineText | — | The inline text to render (used when `hasTextContent` is `true`). |
| `nonInlineTextContent` | text | — | Plain text content for elements that cannot contain inline children. |

---

### Events

HTML Element exposes the **full browser event surface** — every standard DOM event is available as a workflow trigger:

**Pointer & Mouse:** `click`, `doubleClick`, `mouseDown`, `mouseUp`, `mouseMove`, `mouseEnter`, `mouseLeave`, `mouseOver`, `mouseOut`, `auxClick`, `contextMenu`

**Pointer (touch/stylus):** `pointerDown`, `pointerUp`, `pointerMove`, `pointerEnter`, `pointerLeave`, `pointerOver`, `pointerOut`, `pointerCancel`, `gotPointerCapture`, `lostPointerCapture`

**Touch:** `touchStart`, `touchEnd`, `touchMove`, `touchCancel`

**Keyboard:** `keyDown`, `keyUp`

**Focus:** `focus`, `blur`

**Drag & Drop:** `drag`, `dragStart`, `dragEnd`, `dragEnter`, `dragLeave`, `dragOver`, `dragExit`, `drop`

**Form:** `change`, `input`, `beforeInput`, `submit`, `reset`, `invalid`, `select`

**Media:** `play`, `pause`, `playing`, `ended`, `canPlay`, `canPlayThrough`, `waiting`, `seeking`, `seeked`, `timeUpdate`, `durationChange`, `volumeChange`, `rateChange`, `emptied`, `stalled`, `suspend`, `loadedData`, `loadedMetadata`, `loadStart`, `progress`, `error`, `encrypted`

**Animation & Transition:** `animationStart`, `animationEnd`, `animationIteration`, `transitionStart`, `transitionEnd`, `transitionRun`, `transitionCancel`

**Scroll:** `scroll`, `scrollEnd`

**Other:** `wheel`, `copy`, `cut`, `paste`, `toggle`, `beforeToggle`, `abort`, `load`, `compositionStart`, `compositionUpdate`, `compositionEnd`

---

### Style Properties

HTML Element has **no default styles** — it inherits nothing from the theme. All styling must be applied explicitly via the style properties panel or JSX.

---

### Automatic Tag Mapping

When writing JSX, Scram maps many semantic tags automatically — you don't need to use HTML Element directly for these:

| **JSX tag** | **Renders as** |
| --- | --- |
| `<div style={{display:'flex'}}>` | Container (`pla_container`) |
| `<h1>`, `<h2>`, `<h3>`, `<h4>` | Heading variants |
| `<p>` | Text (`pla_text`) |
| `<span>` | Unstyled Text (`pla_unstyledtext`) |
| `<section>`, `<article>`, `<header>`, `<footer>`, `<nav>`, `<main>`, `<aside>` with flex | Container |

Tags with **no Scram equivalent** (e.g. `<canvas>`, `<video>`, `<audio>`, `<table>`, `<details>`, `<summary>`) remain as HTML Elements.

---

### Key Points

- HTML Element is an **atomic** component — it has no subcomponents and cannot be broken down further
- It has **no variables** and is not theme-aware — all styling is manual
- The full DOM event list makes it useful when you need events that platform components don't expose (e.g. `scroll`, `keyDown`, `wheel`, `drag`)
- Use `asHtmlTag` to change the rendered tag without removing and re-adding the component
- For semantic HTML, prefer the appropriate Scram platform component where one exists — they carry theme awareness and built-in accessibility behaviour that raw HTML Elements do not