---
title: "Understanding Data Sources"
---

Data Sources are Scram's way of connecting your app to external systems, APIs, databases, and services. They're the bridges between your frontend apps and the data and functionality your app needs.

---

## Built-in Data Sources

Every Scram project comes with two data sources ready to use out of the box.

<CardGroup cols={2}>
  <Card title="The Scram Database" icon="database" href="/understanding/understanding-the-scram-database">
    A PostgreSQL database included with every project.

    Use it to store your application data — users, products, orders, and anything else your app needs to persist. Supports full SQL: `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.
  </Card>
  <Card title="The Scram File Store" icon="folder-open" href="/understanding/understanding-the-filestore">
    A built-in cloud file storage system.

    Use it to upload and manage files — images, PDFs, documents. Supports preparing uploads, uploading files, and listing stored files.
  </Card>
</CardGroup>

---

## External API Calls

In addition to the built-in sources, you can connect to any external service by configuring outgoing API calls — or receive data from external systems via incoming API calls (webhooks).

Common examples include:

- **Payment APIs** — Stripe, PayPal, Square
- **Email services** — SendGrid, Mailgun, Postmark
- **SMS and notifications** — Twilio, Slack, Discord
- **Third-party APIs** — GitHub, Google Maps, OpenAI, weather services
- **Your own backend** — if you have a separate API server, you can connect to it as a data source

API integrations are configured in the [HTTP API](/resources/http-api) section of the Resource View. For details on securing API calls with tokens, API keys, and other auth methods, see [Authenticating API Calls](/understanding/subpages/authenticating-api-calls). For AI and other APIs that support incremental responses, see [Streaming API Responses](/understanding/subpages/streaming-api-responses).

---

## Learn More

<CardGroup cols={3}>
  <Card title="The Scram Database" href="/understanding/understanding-the-scram-database" />
  <Card title="The Scram File Store" href="/understanding/understanding-the-filestore" />
  <Card title="API Calls" href="/understanding/subpages/data-sources---api-calls" />
</CardGroup>