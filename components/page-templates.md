# Page Templates

# Page Templates

A **page template** is a pre-built layout component that wraps an entire page. Instead of building your navigation bar and footer from scratch on every page, you place a template once, and it provides the surrounding structure automatically — you only need to fill in the content that changes from page to page.

---

## The Problem They Solve

Without a template, you'd have to add a navigation bar, a footer, and all the layout scaffolding to every single page in your app. If you later wanted to change the nav bar, you'd have to update every page individually.

With a template, that shared structure lives in one place. Change it once, and every page using that template updates automatically.

---

## How They Work

A page template is a component that contains **slots** — placeholder areas where you drop your page-specific content. The template itself manages everything outside those slots.

```
┌──────────────────────────────┐
│   Navigation (template)      │
├──────────────────────────────┤
│                              │
│   ← your content goes here → │  (the slot)
│                              │
├──────────────────────────────┤
│   Footer (template)          │
└──────────────────────────────┘
```

The navigation and footer are part of the template. The middle section is the slot — you own it entirely.

---

## Using a Template

1. Add the template component as the **outermost component** on your page — it should wrap everything else.
2. Place your page-specific components **inside its default slot**. They appear in the content area between the header and footer.
3. Configure the template's properties (such as container width) to match your design.

---

## Scram's Built-in Template

Scram ships with one page template out of the box:

| **Template** | **What it provides** | Details |
| --- | --- | --- |
| **Page Template Full** (`pla_pagetemplatefull`) | A top navigation bar, a centred content area, and a footer | [Page Template Full](Page%20Template%20Full%2030f65b4769b5804c9499c5ab6b28a154.md)  |

This covers the most common app layout: a persistent header and footer with changing content in between.

---

## Key Points

- **One template, many pages.** Apply the same template across your whole app for visual consistency.
- **Only content changes.** Each page fills the slot differently; the chrome around it stays the same.
- **Customise the sub-components.** The navigation bar and footer inside the template are themselves editable components — add your logo, links, and branding there.
- **Templates are just components.** Under the hood, a page template is a regular Scram component. You can inspect and edit its internals like any other component.