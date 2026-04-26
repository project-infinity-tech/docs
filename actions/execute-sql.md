# Execute SQL

This section should be read on conjunction with [Understanding the Scram Database](Understanding%20the%20Scram%20Database%2030a65b4769b58030b54afc41839e4a45.md).

**Execute SQL** runs a SQL query against the app's built-in ScramDB database. It is the direct, flexible way to read or write data — fetching records, inserting rows, updating fields, deleting entries, or running any query that the app's data model requires.

---

## What is Execute SQL?

Execute SQL is a **database action** that sends a raw PostgreSQL query to ScramDB and returns the result. It gives you full access to the database's capabilities — joins, aggregates, filters, ordering, transactions — without abstracting away the SQL.

It is available in both frontend workflows (triggered by user interaction) and page-data workflows (running on page load).

---

## Inputs

### Query

A PostgreSQL SQL statement. Written as a template literal to safely handle quotes and dynamic content:

```
SELECT * FROM "Users" WHERE "id" = $1
```

Table names and column names in ScramDB use **PascalCase** for tables and **camelCase** for columns, and must always be quoted:

- Tables: `"Users"`, `"Products"`, `"OrderItems"`
- Columns: `"firstName"`, `"createdAt"`, `"userId"`

### Params

An object mapping parameter placeholders to their runtime values:

```
{ $1: user.id, $2: vars.searchQuery }
```

Parameters are how dynamic values — user input, variable values, step outputs — are safely passed into a query. Never interpolate values directly into the query string. Always use `$1`, `$2`, etc. with a corresponding params object.

---

## Output

Execute SQL returns:

- **`output.value`** — an array of result rows for SELECT queries; an empty or summary array for writes
- **`output.success`** — `true` if the query executed without error
- **`output.errorCode`** — the category of failure if something went wrong

Always follow Execute SQL with an **If/Else** checking `output.success` before using the result or assuming a write succeeded.

---

## The Four Core Operations

Execute SQL covers all four fundamental database operations:

**SELECT** — fetch records from the database **INSERT** — add new records **UPDATE** — modify existing records **DELETE** — remove records

Each has its own patterns, conventions, and gotchas. They are covered in detail in the sections below.

---

## A Note on SQL Injection

Scram's parameterised query system (`$1`, `$2`) is the protection against SQL injection. Values passed through `params` are never interpolated into the query string — they are sent separately and handled safely by the database driver.

Never build a query by concatenating user input into the query string directly. Always use params.

---

## Further Sections