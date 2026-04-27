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

## Related Topics

<CardGroup cols={2}>
  <Card title="Sending Query Parameters" icon="code" href="/understanding/subpages/sending-query-parameters">
    Pass data between pages using URL query parameters.
  </Card>
  <Card title="Page Authorisation" icon="lock" href="/understanding/subpages/page-authorisation">
    Control who can access each page in your app.
  </Card>
</CardGroup>