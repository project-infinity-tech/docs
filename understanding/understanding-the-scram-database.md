# Understanding the Scram Database

Scram’s built-in data is a **relational database** — it's built on PostgreSQL, so you get all the standard relational features like:

- **Tables with typed columns** (text, integer, number, boolean, dates, enums, arrays, etc.)
- **SQL queries** with full JOIN support
- **Indexes** for performance
- **Transactions** for data consistency

The Scram Database can be accessed either from the Side Bar menu ☁️ \+ 💽 or from the Backend Overview ☁️ and clicking Database

## Further Sections

This entry is an overview. The following sections cover Execute SQL in depth:

### Querying Data

- **SELECT basics** — fetching rows, filtering with WHERE, ordering, limiting
- **Filtering with parameters** — safe use of `$1`, `$2` placeholders
- **JOINs** — combining data across related tables
- **Aggregates** — COUNT, SUM, AVG, GROUP BY
- **Full-text search** — LIKE, ILIKE, and PostgreSQL text search
- **Pagination** — LIMIT and OFFSET patterns for large datasets

### Writing Data

- **INSERT** — adding new rows, returning the created record's ID
- **UPDATE** — modifying existing rows safely with WHERE clauses
- **DELETE** — removing rows, and why WHERE clauses are non-negotiable
- **RETURNING** — getting data back from write operations without a second query

### Data Modelling

- **ScramDB table conventions** — PascalCase tables, camelCase columns, the automatic `id` primary key
- **Relating tables** — using integer foreign key fields to link records across tables
- **The Users table** — built-in fields, adding custom fields, querying authenticated users
- **Dates and times** — storing, querying, and formatting temporal data in PostgreSQL

### Patterns and Practices

- **Using Execute SQL in page-data workflows** — loading data on page open
- **Using Execute SQL in frontend workflows** — writing data in response to user actions
- **Handling errors** — interpreting error codes, surfacing useful messages to users
- **Dynamic queries** — building flexible queries safely when filters are optional
- **Working with arrays** — PostgreSQL array fields, `ANY`, `@>` operators
- **Transactions** — ensuring multiple writes succeed or fail together