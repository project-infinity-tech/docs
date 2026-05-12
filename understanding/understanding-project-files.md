---
title: "Understanding Project Files"
---

Project Files are a place to upload and store static assets that are used directly in your app's design — things like images, logos, hero images, background photos, videos, and audio files.

<Note>
  Project Files are for **design-time assets** that you manage while building your app. If you need to handle files that users upload at runtime — like profile photos, documents, or attachments — that's the [File Store](/understanding/understanding-the-filestore).
</Note>

---

## How They Work

You upload a file once, and it becomes available to use anywhere across your app. When you're editing a component that has an image, video, or audio prop — like an Image component or a Background Image Container — you can pick from your Project Files directly in the editor, without copying URLs or hunting for files.

---

## What They're Not For

Project Files are for design-time assets — files that are part of how the app looks. They're not for files that users upload while using the app. That's handled at runtime by the [File Store](/understanding/understanding-the-filestore).

---

## In Short

Think of Project Files as your app's asset library — a shared folder of images and media that you, the developer, manage and use while building.