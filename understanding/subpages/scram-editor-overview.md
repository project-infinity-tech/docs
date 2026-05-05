---
title: "The Scram Editor"
description: "An overview of the Scram editor and its three main views."
---

The Scram editor is where you build your app. It has three distinct views, each with a different purpose — the **Canvas**, the **Workflow Editor**, and **Resource View**. You switch between them depending on what you're working on.

---

## The three views

**The Canvas** is where you design your app's pages. You place and arrange components, configure their properties, and define how the page looks and behaves. It's the view you'll spend most of your time in when building UI.

**The Workflow Editor** is where you define the logic of your app — what happens when a user clicks a button, submits a form, or triggers any other event. Workflows are sequences of actions that run in response to those events.

**Resources** is the backend view. It gives you access to everything that lives outside of individual pages — your database, file storage, API integrations, user management, data types, deployments, and server logs.

---

## Always-visible elements

Regardless of which view you're in, two areas are always present:

**The Top Navigation** runs across the top of the editor. It gives you access to project-level settings and lets you switch between your apps.

**The Side Navigation** runs down the left edge. It contains the AI chat assistant, the page structure tree, and the component editor — the tools you reach for most often while building.

---

## Editor areas

<CardGroup cols={2}>
  <Card title="Canvas" href="/understanding/subpages/canvas">
    Design your pages — place components, configure layouts, and set properties.
  </Card>
  <Card title="Workflow Editor" href="/understanding/subpages/workflow-editor">
    Build the logic of your app — actions, events, and conditional flows.
  </Card>
  <Card title="Top Navigation" href="/understanding/subpages/top-navigation">
    Project-level controls — manage apps and configure frontend settings.
  </Card>
  <Card title="Side Navigation" href="/understanding/subpages/side-navigation">
    AI chat, page structure, and the component editor.
  </Card>
</CardGroup>

---

## Resource View

<CardGroup cols={2}>
  <Card title="Component Gallery" href="/understanding/subpages/component-gallery">
    Browse and manage the components available in your project.
  </Card>
  <Card title="Project Files" href="/understanding/subpages/project-files">
    Static assets and files attached to your project.
  </Card>
  <Card title="Database" href="/understanding/subpages/database">
    Create and manage your app's database tables and fields.
  </Card>
  <Card title="Storage" href="/understanding/subpages/storage">
    File storage powered by the Scram File Store.
  </Card>
  <Card title="HTTP API" href="/understanding/subpages/http-api">
    Configure external API integrations.
  </Card>
  <Card title="Users" href="/understanding/subpages/users">
    Manage user accounts, roles, and authentication settings.
  </Card>
  <Card title="Workflows" href="/understanding/subpages/workflows">
    Server-side workflows that run independently of page events.
  </Card>
  <Card title="Data Types" href="/understanding/subpages/data-types">
    Define and manage the custom types used across your project.
  </Card>
  <Card title="Deployments" href="/understanding/subpages/deployments">
    Manage your Dev and Live environments.
  </Card>
  <Card title="Server Logs" href="/understanding/subpages/server-logs">
    Monitor and debug server-side activity.
  </Card>
</CardGroup>