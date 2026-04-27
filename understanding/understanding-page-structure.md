---
title: "Understanding Page Structure"
description: "How pages work in Scram and how they map to your live app."
---

## The Basics

Scram apps are built around pages — at minimum one Index page — and each page maps directly to a URL in your deployed web app.

## The Index Page

Every app has an Index page created by default when the app is first created. You can rename it any time by double-clicking the name in the editor.

By default, the Index page has a **blank slug**, which means it loads when someone visits your root URL.

<Info>
  If you set another page to have a blank slug, that page will become the new root — the originally created page will no longer load by default.
</Info>

**Example:** If your app is deployed to `mybrandnewsite.com`, any visitor hitting that URL will land on whichever page has the blank slug.

<Note>
  You can change which page acts as the "index" by updating the slug of the old index page to something non-blank, and setting the new page's slug to blank.
</Note>

---

##Adding Pages##

To add a new page, click the **\+** button next to your app name in the pages panel. Give the page a name and a slug — the slug is what appears in the URL when someone visits that page.

Example: A page with the slug `about` would be accessible at `mybrandnewsite.com/about`.

> _Page slugs should be lowercase, with no spaces. Use hyphens to separate words (e.g._ `contact-us`_)._

---

##Child Pages##

Pages can be nested inside other pages, creating a hierarchy. A child page's full URL is made up of its parent's slug followed by its own slug.

Example: If you have a parent page with the slug `blog`, and a child page with the slug `getting-started`, that child page would be accessible at `mybrandnewsite.com/blog/getting-started`.

This is useful for organising related pages together — for example, grouping all settings pages under a `/settings` parent, or all help articles under `/help`.

> _A child page can itself have children, allowing you to build as many levels of nesting as your app requires._

Child pages are created the same way as regular pages — use the **\+** button — and you can drag and drop pages in the panel to rearrange them or change their parent at any time.

## Related Topics

<CardGroup cols={2}>
  <Card title="Sending Query Parameters" icon="circle-question" href="/understanding/subpages/sending-query-parameters">
    Pass data between pages using URL query parameters.
  </Card>

  <Card title="Page Authorisation" icon="lock" href="/understanding/subpages/page-authorisation">
    Control who can access each page in your app.
  </Card>

  <Card title="Page Path Parameters" icon="slash-forward" href="/understanding/subpages/page path parameters">
    Control who can access each page in your app.
  </Card>
</CardGroup>