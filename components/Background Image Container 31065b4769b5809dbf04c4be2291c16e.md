# Background Image Container

## Overview

**Background Image Container** is a layout container that displays an image as its background while allowing you to place other components on top. It is the standard way to build hero sections, banner panels, image-backed cards, and full-bleed section dividers in Scram.

Unlike the Image component — which renders an image as a content element — the Background Image Container treats the image purely as decoration behind its child content.

---

## Structure

```
┌─────────────────────────────────────────────────┐
│  [background image fills the container]          │
│                                                  │
│     ┌───────────────────────────────┐            │
│     │  default slot                 │            │
│     │  (your content on top)        │            │
│     └───────────────────────────────┘            │
│                                                  │
└─────────────────────────────────────────────────┘
```

---

## Slots

| **Slot** | **Description** |
| --- | --- |
| **default** | Any components placed here render on top of the background image — headings, buttons, overlays, etc. |

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Background Image** (`backgroundImage`) | Text (URL) | *(sample image)* | The URL of the image to display. Accepts any publicly accessible image URL, or a dynamic expression pointing to a stored URL. |
| **Position** (`backgroundPosition`) | Enum | `center` | Where the image is anchored within the container. |
| **Size** (`backgroundSize`) | Enum | `cover` | How the image is scaled to fit the container. |
| **Just a decorative image?** (`decorative`) | Boolean | `false` | Whether the image is purely visual with no informational content. See the Accessibility section below. |

---

### Position Options

| **Value** | **Behaviour** |
| --- | --- |
| `center` | Image is centred horizontally and vertically *(default)* |
| `left` | Image is anchored to the left edge |
| `right` | Image is anchored to the right edge |
| `top` | Image is anchored to the top edge |
| `bottom` | Image is anchored to the bottom edge |

---

### Size Options

| **Value** | **Behaviour** |
| --- | --- |
| `cover` | Scales the image up or down to fill the entire container. The image may be cropped. *(default)* |
| `contain` | Scales the image to fit entirely within the container without cropping. May leave empty space on the sides or top/bottom. |
| `auto` | Displays the image at its original pixel dimensions, without scaling. |

> **`*cover` is almost always the right choice** for hero sections and banners. It guarantees no empty gaps and keeps the container looking full regardless of screen size or image dimensions.*
> 

---

## Style Properties

The container exposes the full set of layout style properties:

| **Property** | **Default** |
| --- | --- |
| `display` | `flex` |
| `flexDirection` | `row` |
| `flexWrap` | `nowrap` |
| `justifyContent` | `start` |
| `alignItems` | `start` |
| `rowGap` / `columnGap` | `0px` |
| `overflow` | `visible` |
| `width` | `auto` |
| `minHeight` | `200px` |
| `height` | `auto` |
| `padding` | `0` |

The `minHeight: 200px` default ensures the container is always visible even when the default slot is empty.

---

## Events

The container responds to the full set of pointer events:

| **Event** | **Fires when…** |
| --- | --- |
| `click` | User clicks the container |
| `doubleClick` | User double-clicks the container |
| `mouseEnter` | Pointer moves into the container |
| `mouseLeave` | Pointer moves out of the container |
| `contextMenu` | User right-clicks the container |
| `blur` | Container loses focus |

---

## Accessibility

The **"Just a decorative image?"** toggle controls how the image is treated by screen readers.

| **Setting** | **Behaviour** |
| --- | --- |
| `false` *(default)* | The image is treated as meaningful content and announced to assistive technology. |
| `true` | The image is hidden from assistive technology (`aria-hidden`). Use this when the image is purely visual — a texture, a photographic backdrop — and the actual information is conveyed by the content in the slot. |

For hero sections where a heading in the slot describes the content, set this to `true`. For a container where the image itself carries meaning (e.g. a product photo used as a background), leave it `false`.

---

## Key Points

- The image is applied via CSS `background-image`, not an `<img>` tag. It scales and crops according to the `backgroundSize` and `backgroundPosition` settings without affecting document flow.
- The default slot is a standard flex container — use `justifyContent`, `alignItems`, and `padding` to position your foreground content precisely over the image.
- For dark images, place a semi-transparent overlay `div` inside the slot before your text to ensure contrast.
- For dynamic images (e.g. a user's chosen banner), set `backgroundImage` to an expression like `current.data.bannerUrl`.