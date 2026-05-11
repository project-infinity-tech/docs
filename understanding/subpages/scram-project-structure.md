---
title: "Understanding Scram Project Structure"
---

A Scram project is the top-level container for everything that makes up your app — the frontend, backend, data, users, and configuration. Understanding how a project is structured helps you navigate the editor and know where to find things.

---

## Frontend

### Apps

A Scram App is the thing you're building — a marketing site, a web app, a mobile app, or a browser extension. A project can contain one app or many.

Having multiple apps in a single project means they can share the same database, components, themes, and user base. You could have a customer-facing web app, a stripped-down mobile version, and a separate admin tool — all built from the same project, accessing the same data.

### Theme

Every project has a Theme that controls the visual style of all its apps — typography, colours, spacing, border styles, and icon library. Changing a theme value updates every component across every app that uses it.

See [Understanding Themes](/understanding/understanding-themes) for more detail.

### Components

Components are the building blocks of your app's pages — buttons, inputs, headings, images, containers, and more. Scram provides a library of platform components covering both individual UI elements and higher-level layout components like hero sections, navigation bars, and page templates.

You can also build your own components, either by composing existing ones or starting from scratch.

All apps in a project share the same component library, so a custom component built once is available everywhere.

---

## Backend

### Database

Every Scram project includes a built-in PostgreSQL database. You define your tables and fields, and Scram handles the hosting and infrastructure. All apps in a project share the same database.

See [Understanding the Scram Database](/understanding/understanding-the-scram-database) for more detail.

### File Store

The Scram File Store is S3-backed cloud storage for files your app needs to store or serve — user uploads, images, documents, and so on. Like the database, it is shared across all apps in the project.

See [Understanding the File Store](/understanding/understanding-the-filestore) for more detail.

### Data Sources

A Data Source is anything that brings data into your app or sends it out. At its simplest, that's your internal database. It also covers external APIs — HTTP endpoints you configure to fetch or push data to third-party services.

All apps in a project share the same data sources, so an API integration configured once is available to every app.

See [Understanding Data Sources](/understanding/understanding-data-sources) for more detail.

### Users

Every Scram project has a built-in user management system — authentication, roles, and access control included. You don't need a third-party auth service; it's part of the platform.

All apps in a project share the same user base, which means a user who signs up through one app is automatically available across all apps in the project.

See [Understanding User Management](/understanding/understanding-user-management) for more detail.

### Data Types

Scram has a rich type system covering custom project types, database types, platform types, and style types. Types are used throughout the editor to validate data, define component properties, and power expressions.

See [Understanding Data Types](/understanding/understanding-data-types) for more detail.

### Server Logs

Server Logs records server-side activity for your project. You can write messages to the log from any workflow using the Log Message action, making it useful for debugging and monitoring.

See [Understanding Server Logs](/understanding/understanding-server-logs) for more detail.