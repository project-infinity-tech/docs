---
title: "Understanding Page Structure"
description: "How pages work in Scram and how they map to your live app."
---

Scram apps are built around pages. Each page maps directly to a URL in your deployed app, and every app starts with at least one — the Index page.

---

## The Index page

Every app has an Index page created by default. It has a **blank slug**, which means it loads when someone visits your root URL.

**Example:** If your app is deployed to `mybrandnewsite.com`, visitors hitting that URL will land on whichever page has the blank slug.

<Note>
  You can change which page acts as the index by setting its slug to blank and giving the previous index page a non-blank slug.
</Note>

---

## Adding pages

Pages are added from the **App Manager** in the Top Navigation. Give each page a name and a slug — the slug is what appears in the URL when someone visits that page.

**Example:** A page with the slug `about` would be accessible at `mybrandnewsite.com/about`.

<Tip>
  Page slugs should be lowercase with no spaces. Use hyphens to separate words — e.g. `contact-us`.
</Tip>

---

## Child pages

Pages can be nested inside other pages, creating a URL hierarchy. A child page's full URL is made up of its parent's slug followed by its own slug.

**Example:** A parent page with the slug `blog` and a child page with the slug `getting-started` would be accessible at `mybrandnewsite.com/blog/getting-started`.

This is useful for organising related pages together — for example, grouping all settings pages under `/settings`, or all help articles under `/help`.

<Note>
  A child page can itself have children, allowing as many levels of nesting as your app requires.
</Note>

---

## Path parameters

Page slugs can include dynamic path parameters — placeholders that capture a variable value from the URL. For example, a page with the slug `:itemId` nested under an `items` parent would be accessible at `mybrandnewsite.com/items/42`, and the page would know that `itemId` is `42`.

See [Page Path Parameters](/understanding/subpages/page-path-parameters) for full details.

---

## Related topics

<CardGroup cols={2}>
  <Card title="Page Path Parameters" icon="slash-forward" href="/understanding/subpages/page-path-parameters">
    Use dynamic URL segments to display different content on the same page.
  </Card>
  <Card title="Sending Query Parameters" icon="circle-question" href="/understanding/subpages/sending-query-parameters">
    Pass data between pages using URL query parameters.
  </Card>
  <Card title="Page Authorisation" icon="lock" href="/understanding/subpages/page-authorisation">
    Control who can access each page in your app.
  </Card>
  <Card title="App Manager" icon="grid" href="/understanding/subpages/the-app-manager">
    Where you add and manage pages in your app.
  </Card>
</CardGroup>