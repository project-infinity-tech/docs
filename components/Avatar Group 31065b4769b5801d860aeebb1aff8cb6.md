# Avatar Group

# Overview

**Avatar Group** displays a horizontal stack of overlapping [avatars](Avatar%2031065b4769b580f9b3b1c69def5f6c9b.md) from an array of data. It is used to represent a collection of people compactly — team members on a project, participants in a conversation, contributors to a document.

---

## Properties

| **Property** | **Type** | **Default** | **Description** |
| --- | --- | --- | --- |
| **Avatar List** (`avatarList`) | Array of objects | `[{}]` | The list of people to display. Each item can have an image URL, an optional status, and an optional link. |
| **Avatar Size** (`avatarSize`) | Enum | `sm` | Size of every avatar in the group. All avatars share the same size. |

### Avatar List Item Fields

Each object in `avatarList` supports:

| **Field** | **Type** | **Required** | **Description** |
| --- | --- | --- | --- |
| `avatarImage` | Text (URL) | Optional | Profile photo URL. Falls back to a placeholder image if omitted. |
| `status` | `online` | `offline` | Optional | Presence indicator. Omit for no dot. |
| `link` | Text (URL) | Optional | A URL associated with this person. |

---

### Size Options

| **Value** | **Diameter** | **Overlap offset** |
| --- | --- | --- |
| `sm` | 3rem | −1rem |
| `md` | 4rem | −1.25rem |
| `lg` | 6rem | −1.5rem |

The negative left margin on each avatar after the first creates the overlapping stack effect. The overlap is proportional to the avatar size.

---

## Style Properties

| **Property** | **Default** |
| --- | --- |
| `width` | `fit-content` |

---

## Example Data

```
[
  { "avatarImage": "https://example.com/alice.jpg", "status": "online" },
  { "avatarImage": "https://example.com/bob.jpg",   "status": "offline" },
  { "avatarImage": "https://example.com/carol.jpg"  }
]
```

Bind `avatarList` to this array and the group renders three overlapping circles, the first two with presence dots.

---

## Key Points

- **All avatars in a group share the same size.** Use `avatarSize` to set it. You cannot mix sizes within one group.
- **The group width is `fit-content`** — it shrinks to exactly the width of its stacked avatars. Place it inside a flex container to control its position within a larger layout.
- **The group uses a [Repeater](Repeater%2030f65b4769b5809b99e3de6e9112e82f.md) internally.** You cannot target individual avatars within the group by component ID. Presence dots and images are driven entirely by the `avatarList` data.
- **To show a count overflow** (e.g. "+5 more"), add a custom element after the [Avatar Group](Avatar%20Group%2031065b4769b5801d860aeebb1aff8cb6.md) component rather than trying to modify the group itself.