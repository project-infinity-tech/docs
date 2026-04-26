# Understanding Data Types

Every piece of data in Scram has a type. Types tell the system what kind of value to expect, how to store it, how to display it, and what operations make sense on it. Understanding types helps you build more reliably — and avoid subtle bugs where a value looks right but behaves unexpectedly.

---

## Primitive Types

These are the basic building blocks. Most values in your app will be one of these.

**Text** — Any string of characters. Names, descriptions, status labels, IDs stored as strings. The most general-purpose type; when in doubt, text works — but be specific when you can.

**Number** — A numeric value that may include decimals. Use for prices, measurements, percentages, scores.

**Integer** — A whole number with no decimal part. Use for counts, quantities, positions, and database row IDs. Choosing integer over number matters when you need to ensure a value is always whole.

**Boolean** — True or false. On or off. Use for flags, toggles, and binary states.

**Date** — A calendar date with no time component. Use for birthdays, deadlines, publication dates — situations where the time of day is irrelevant.

**Time** — A time of day with no date. Use for opening hours, scheduled times within a day.

**Datetime** — A combined date and time. Use for events, timestamps, created/updated records. In Scram, datetimes are represented as **Temporal** objects — not JavaScript Date objects. Use the built-in expression functions (`Now()`, `FormatDateTime()`, `Add()`, `Subtract()`) to work with them.

**File** — A file reference. Used for uploads and file handling workflows.

---

## Structured Types

When a single value isn't enough, structured types let you group related data together.

**Enum** — A value restricted to a fixed set of options. If a field can only ever be "pending", "active", or "archived", an enum enforces that. Enums prevent typos and make your data more predictable. They're stored as text internally but validated against the allowed values.

**Reference (ref)** — A pointer to a defined type. Instead of describing the same shape of data in multiple places, you define a type once and reference it wherever it's needed. This is how you use database table types, API response types, and custom project types in variables and properties.

---

## Arrays

Any type can be made into an **array** — a list of values of that type. An array of text holds multiple strings. An array of integers holds multiple whole numbers. An array of a reference type holds multiple structured objects.

Arrays are what the Repeater consumes. When you load a list of records from the database and pass them to a Repeater, you're passing an array.

---

## Where Types Are Used

Types appear throughout Scram wherever you define something that holds a value:

**Database fields** — Each column in a database table has a type. Choosing the right type determines how values are stored and queried.

**Page variables** — When you create a variable on a page, you declare its type. This tells Scram what kind of data the variable will hold and how to handle expressions that reference it.

**Component properties** — Properties on component definitions have types that control what values are valid inputs and how they appear in the editor.

**Component variables** — Internal state within a component has a type, just like page variables.

**Action inputs and outputs** — Workflow actions accept inputs of specific types and produce outputs of specific types. Matching types correctly is what makes expressions resolve cleanly.

**API response schemas** — When you define what an external API returns, you're describing the type of its response. This lets Scram understand the shape of the data so you can reference it safely in expressions.

---

## Custom Project Types

Beyond the built-in types, you can define your own **project types** — named, reusable shapes that describe structured data specific to your application.

A `CartItem` type might have a `productId` integer, a `quantity` integer, and a `unitPrice` number. An `Address` type might have `line1`, `line2`, `city`, `postcode` — all text.

Once defined, project types can be referenced anywhere a type is expected: page variables, component properties, API schemas. They're the equivalent of defining a data structure once and reusing it throughout the app.

Define project types when the same shape of data appears in multiple places. It keeps your app consistent and means a structural change only needs to happen in one place.

---

## Type Mismatches

Scram will flag type mismatches when it can detect them. If a property expects a number and you pass a text value, or a variable is declared as a boolean but you try to assign an array to it, you'll see a diagnostic error.

The most common mismatch to watch for is **text vs. number**. Data coming from user inputs is almost always text, even if the user typed a number. If you need to do arithmetic on it, you may need to convert it first.

---

## Key Things to Know

**Be as specific as you can.** Use `integer` instead of `number` when the value will always be whole. Use `enum` instead of `text` when the value comes from a fixed set. Specificity catches errors early.

**Datetime is not a JavaScript Date.** Scram uses the Temporal standard. Don't use `new Date()` or `.toISOString()` — use Scram's built-in date/time expression functions instead.

**Arrays are first-class.** Any type can be an array. A variable, property, or field declared as `text[]` holds a list of strings. This is distinct from a single `text` value and they are not interchangeable.

---

## Related

- [Building Your Own Components →](Building%20Your%20Own%20Components%2031a65b4769b5809395ecce627b222e76.md)
- [Working with the Database →](Understanding%20the%20Scram%20Database%2030a65b4769b58030b54afc41839e4a45.md)
- [Working with Expressions →](Understanding%20Expressions%2015965b4769b580aab433dc5ea4a9f19d.md)
- [Custom Project Types →](Custom%20Project%20Types%2031a65b4769b580df99b7fb8a8c1286c4.md)