---
title: "Understanding The Scram Database"
---

# The Scram Database

Scram's built-in database is a relational database built on PostgreSQL, giving you all the standard relational features:

- Tables with typed columns (text, integer, number, boolean, dates, enums, arrays, and more)
- SQL queries with full `JOIN` support
- Indexes for performance
- Transactions for data consistency

<Note>
  The Scram Database can be accessed from the Resources Menu. Either from the Database option or via the Overview.
</Note>

## Further sections

This page is an overview. The sections below cover working with the Scram Database in depth.

### Querying Data

- **SELECT basics** — fetching rows, filtering with `WHERE`, ordering, limiting
- **Filtering with parameters** — using named parameters (`:paramName`) as the preferred style, e.g. `:userId`, `:status`. Positional parameters (`$1`, `$2`) are also supported for backwards compatibility
- **JOINs** — combining data across related tables
- **Aggregates** — `COUNT`, `SUM`, `AVG`, `GROUP BY`
- **Full-text search** — `LIKE`, `ILIKE`, and PostgreSQL text search
- **Pagination** — `LIMIT` and `OFFSET` patterns for large datasets

### Writing Data

- **INSERT** — adding new rows, returning the created record's ID
- **UPDATE** — modifying existing rows safely with `WHERE` clauses
- **DELETE** — removing rows, and why `WHERE` clauses are non-negotiable
- **RETURNING** — getting data back from write operations without a second query

### Data Modelling

- **ScramDB table conventions** — PascalCase tables, camelCase columns, the automatic `id` primary key
- **Relating tables** — storing ID fields that reference records in other tables
  <Warning>
    Scram does not currently enforce foreign key constraints at the database level. There is no `REFERENCES` or `FOREIGN KEY` enforcement — the database will not prevent you from inserting an invalid ID. Referential integrity must be handled in your app logic. The ID type (`text`/UUID or `integer`) also varies by project — always check before writing queries.
  </Warning>
- **The Users table** — built-in fields, adding custom fields, querying authenticated users
- **Dates and times** — storing, querying, and formatting temporal data in PostgreSQL

### Patterns and Practices

- **Using Execute SQL in page-data workflows** — loading data on page open
- **Using Execute SQL in frontend workflows** — writing data in response to user actions
- **Handling errors** — interpreting error codes, surfacing useful messages to users
- **Dynamic queries** — building flexible queries safely when filters are optional
  <Note>
    Static SQL queries return a typed array — you can use `.length`, `.filter`, and other array methods. Dynamic queries, where the SQL is built conditionally, return untyped JSON, so array methods will not be available.
  </Note>
- **Working with arrays** — PostgreSQL array fields, `ANY`, `@>` operators
- **Transactions** — ensuring multiple writes succeed or fail together