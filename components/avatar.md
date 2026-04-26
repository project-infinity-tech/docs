# Avatar

## Overview

**Avatar** displays a circular profile photo, typically representing a user or contact. It supports three standard sizes and an optional presence indicator dot — a small coloured badge in the top-right corner that signals whether the person is online or offline.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Avatar Image** (`image`) | Text (URL) | *(sample image)* | URL of the photo to display. Accepts any publicly accessible image URL or a dynamic expression such as `user.profilePhotoUrl`. |
| **Alt text** (`alt`) | Text | *(unset)* | Descriptive text for the image, read by screen readers. Should describe the person, e.g. `"Profile photo of Jane Smith"`. |
| **Avatar Size** (`size`) | Enum | `md` | Controls the diameter of the avatar. |
| **Presence Indicator** (`presence`) | Enum | `none` | Whether to show a status dot and what colour it should be. |

---

### Size Options

| **Value** | **Diameter** |
| --- | --- |
| `sm` | 3rem (~48px) |
| `md` | 4rem (~64px) |
| `lg` | 6rem (~96px) |

---

### Presence Indicator Options

| **Value** | **Dot colour** | **Meaning** |
| --- | --- | --- |
| `none` | No dot | No status shown |
| `online` | `success[500]` (green) | Person is active |
| `offline` | `neutral[200]` (light grey) | Person is inactive |

The presence dot appears in the top-right corner of the avatar, outlined with a thin `surface[500]` ring to separate it from the photo underneath.

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `width` | Determined by `size` prop |
| `borderRadius` | `0` *(outer wrapper; the inner circle uses `99rem`)* |
| `borderStyle` | `none` |
| `borderWidth` | `medium` |
| `borderColor` | `currentcolor` |
| `margin` | `auto` |

The circular clipping is applied to the inner image container (`border-radius: 99rem`, `overflow: hidden`), not the outer wrapper. The outer wrapper is square and sized by the `size` prop — this is what holds the presence dot in position.

---

## Key Points

- **The image fills the circle completely.** It uses `width: 100%, height: 100%` inside an `overflow: hidden` circular container, so images are cropped to a square and then rounded. Portrait and landscape images will be cropped at the edges.
- **For logged-in users**, set `image` to `user.profilePhotoUrl` and `alt` to `user.givenName + " " + user.familyName`.
- **The presence dot is absolutely positioned** at `top: 7%, right: 7%` relative to the outer wrapper. It scales proportionally with the avatar size (15% of the container width).

##