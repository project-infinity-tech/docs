# Understanding Data Sources

**Data Sources** are Scram's way of connecting your app to external systems, APIs, databases, and services. They're the bridges between your frontend apps and the data/functionality your app needs.

The pre-built Data Sources are :

- The Scram Database
    - **What:** PostgreSQL database included with every app
    - **Purpose:** Store your application data (users, products, orders, etc.)
    - **Actions:** Execute SQL queries (SELECT, INSERT, UPDATE, DELETE)
    - **Usage:** Internal data storage, user records, app state
- The Scram File Store
    - **What:** Cloud file storage system
    - **Purpose:** Upload and manage files (images, PDFs, documents)
    - **Actions:** Prepare upload, upload files, list files
    - **Usage:** User avatars, document uploads, media libraries

In addition to the database and file store you can add incoming and outgoing API calls

- Common Examples
    - **Payment APIs:** Stripe, PayPal, Square
    - **Email Services:** SendGrid, Mailgun, Postmark
    - **SMS/Notifications:** Twilio, Slack, Discord
    - **Third-party APIs:** GitHub, Google Maps, OpenAI, Weather APIs
    - **Your own backend:** If you have a separate API server

[Data Sources - The Scram Database](Data%20Sources%20-%20The%20Scram%20Database%202e165b4769b5807b9b88c80d8a0e6a38.md)

[The Scram File Store](The%20Scram%20File%20Store%202e165b4769b580788f5ccf1810c4fb90.md)

[Data Sources - API Calls](Data%20Sources%20-%20API%20Calls%2014965b4769b58082bd85f86052bc4a7f.md)