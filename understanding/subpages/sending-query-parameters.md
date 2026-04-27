---
title: "Sending Query Parameters"
---

# Sending Query Parameters

**Query Parameters**

Query parameters are extra pieces of information you can attach to a URL — they appear after a `?` at the end of the address, and let you pass data into a page without it being part of the page's main path.

Example: `mybrandnewsite.com/search?query=shoes` — here, `query` is the parameter name and `shoes` is its value.

You can have multiple query parameters in one URL by separating them with `&`:

`mybrandnewsite.com/search?query=shoes&sort=price`

---

**When to use them**

Query parameters are best suited for things that are optional or changeable — like search terms, filters, sort orders, or the currently active tab. Unlike path parameters, they don't define _which_ page is being shown, just _how_ it should behave or what it should display.

> _Use path parameters when the value identifies a specific resource (e.g. a particular product). Use query parameters when the value influences what's shown on a page but doesn't change which page you're on (e.g. a search term or a filter)._

---

**Defining query parameters on a page**

To make a query parameter available on a page, you declare it in the page's settings. This tells Scram to expect that parameter in the URL and make its value available for use on the page — for example, to pre-fill a search box, apply a filter, or restore a previous state.

Once defined, the parameter's value can be read anywhere on that page and used in workflows or to drive what content is displayed.

---

**Sharing and bookmarking state**

Because query parameters live in the URL, any state stored in them is automatically shareable and bookmarkable. If a user filters a product list and copies the URL, anyone they send it to will land on the same filtered view.

\