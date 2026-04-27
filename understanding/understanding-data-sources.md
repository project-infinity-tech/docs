# Understanding Data Sources

Data Sources are Scram's way of connecting your app to external systems, APIs, databases, and services. They're the bridges between your frontend apps and the data and functionality your app needs.

---

## Built-in Data Sources

Every Scram project comes with two data sources ready to use out of the box.

<CardGroup cols={2}>
  <Card title="The Scram Database" icon="database" href="/data-sources/database">
    A PostgreSQL database included with every project.

    Use it to store your application data — users, products, orders, and anything else your app needs to persist. Supports full SQL: `SELECT`, `INSERT`, `UPDATE`, and `DELETE`.
  </Card>
  <Card title="The Scram File Store" icon="folder-open" href="/data-sources/file-store">
    A built-in cloud file storage system.

    Use it to upload and manage files — images, PDFs, documents. Supports preparing uploads, uploading files, and listing stored files.
  </Card>
</CardGroup>

---

## External API Calls

In addition to the built-in sources, you can connect to any external service by adding outgoing API calls — or receive data from external systems via incoming API calls.

<CardGroup cols={2}>
  <Card title="Payment APIs" icon="credit-card">
    Stripe, PayPal, Square
  </Card>
  <Card title="Email Services" icon="envelope">
    SendGrid, Mailgun, Postmark
  </Card>
  <Card title="SMS & Notifications" icon="bell">
    Twilio, Slack, Discord
  </Card>
  <Card title="Third-party APIs" icon="plug">
    GitHub, Google Maps, OpenAI, Weather APIs
  </Card>
  <Card title="Your own backend" icon="server">
    If you have a separate API server, you can connect to it as a data source.
  </Card>
</CardGroup>

---

## Learn More

<CardGroup cols={3}>
  <Card title="The Scram Database" href="/data-sources/database" />
  <Card title="The Scram File Store" href="/data-sources/file-store" />
  <Card title="API Calls" href="/data-sources/api-calls" />
</CardGroup>