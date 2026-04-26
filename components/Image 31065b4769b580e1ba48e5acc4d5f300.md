# Image

## Overview

**Image** displays a photo or graphic as a content element on the page, with optional rounded corners and a visible caption beneath it. Unlike the [**Background Image Container**](Background%20Image%20Container%2031065b4769b5809dbf04c4be2291c16e.md) — which uses an image as CSS decoration behind other components — Image renders a proper `<img>` element that occupies space in the document flow and is meaningful to browsers, search engines, and screen readers.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Image** (`imgSrc`) | Text (URL) | *(sample photo)* | The URL of the image to display. Accepts any publicly accessible image URL or a dynamic expression such as `current.data.photoUrl`. |
| **Caption** (`imgAlt`) | Text | *(placeholder text)* | Serves two purposes: it is the `alt` attribute on the `<img>` element (read by screen readers and shown if the image fails to load), and it is the visible caption text when **Show Caption** is on. |
| **Show Caption** (`showCaption`) | Boolean | `false` | When on, displays the caption text in a small bar beneath the image. When off, the alt text is still present in the HTML for accessibility — it just isn't visually shown. |

---

## Structure

```
┌─────────────────────────────────┐
│                                 │
│         <img>                   │
│         (fills container)       │
│                                 │
├─────────────────────────────────┤  ← only visible when showCaption: true
│  Caption text                   │
└─────────────────────────────────┘
```

The outer container clips to `theme.roundness.md` by default, applying the theme's standard rounded corners to both the image and the caption bar together.

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `width` | `auto` |
| `height` | `fit-content` |
| `aspectRatio` | `auto` |
| `borderRadius` | `theme.roundness.md` |
| `borderStyle` | `none` |
| `borderWidth` | `medium` |
| `borderColor` | `currentcolor` |
| `boxShadow` | `none` |
| `opacity` | `1` |
| `background` | `transparent` |
| `padding` | `0` |
| `margin` | `auto` |
| `cursor` | `auto` |
| `pointerEvents` | `auto` |

The inner `<img>` element always fills 100% of the width and height of the outer container. Control the image's displayed size by setting `width`, `height`, or `aspectRatio` on the outer container via the style panel.

---

## Caption Styling

When `showCaption` is on, the caption bar renders with:

- **Background:** `neutral[50]`
- **Text colour:** `neutral[700]`
- **Padding:** `theme.spacing.xxxs` on all sides

The caption text is the same value as `imgAlt` — there is a single field that serves both accessibility and display purposes.

---

## Events

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks the image |
| `doubleClick` | User double-clicks the image |
| `mouseEnter` | Pointer enters the image area |
| `mouseLeave` | Pointer leaves the image area |
| `contextMenu` | User right-clicks the image |

---

## Image vs Background Image Container

|  | **Image** | **Background Image Container** |
| --- | --- | --- |
| HTML element | `<img>` | CSS `background-image` |
| In document flow | ✅ Yes — occupies space | ❌ No — purely decorative |
| Content on top | ❌ Not supported | ✅ Via default slot |
| Screen readers | ✅ Read via `alt` | Controlled by `decorative` prop |
| Best for | Photos, illustrations, product images | Hero sections, banner panels, image-backed cards |

---

## Key Points

- **Always fill in the Caption/Alt field.** Even if `showCaption` is off, the `alt` attribute is used by screen readers and displayed by browsers when the image cannot load. An empty alt field leaves the image inaccessible.
- **Size is controlled by the outer container.** Set `width` and/or `aspectRatio` on the Image component to constrain its dimensions. The inner `<img>` always fills whatever space the container provides.
- **Rounded corners are on by default** (`theme.roundness.md`). Set `borderRadius: 0` to show the image with square corners.
- **For images that should link somewhere**, wrap the Image component in a **Link** (`pla_link`) component rather than wiring the `click` event to a NavigateToPath workflow.
- **For images used as decorative backgrounds** behind text or other content, use [**Background Image Container**](Background%20Image%20Container%2031065b4769b5809dbf04c4be2291c16e.md) instead.