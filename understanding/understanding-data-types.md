---
title: "Understanding Data Types"
---

Every piece of data in Scram has a type. Types tell the system what kind of value to expect, how to store it, how to display it, and what operations make sense on it. Understanding types helps you build more reliably — and avoid subtle bugs where a value looks right but behaves unexpectedly.

---

## Primitive Types

These are the basic building blocks. Most values in your app will be one of these.

<CardGroup cols={2}>
  <Card title="Text">
    Any string of characters. Names, descriptions, status labels, IDs stored as strings.

    The most general-purpose type — when in doubt, text works. But be specific when you can.
  </Card>
  <Card title="Number">
    A numeric value that may include decimals.

    Use for prices, measurements, percentages, and scores.
  </Card>
  <Card title="Integer">
    A whole number with no decimal part.

    Use for counts, quantities, positions, and database row IDs. Choose integer over number when you need to ensure a value is always whole.
  </Card>
  <Card title="Boolean">
    True or false. On or off.

    Use for flags, toggles, and binary states.
  </Card>
  <Card title="Date">
    A calendar date with no time component.

    Use for birthdays, deadlines, and publication dates — situations where the time of day is irrelevant.
  </Card>
  <Card title="Time">
    A time of day with no date.

    Use for opening hours and scheduled times within a day.
  </Card>
  <Card title="Datetime">
    A combined date and time.

    Use for events, timestamps, and created/updated records. In Scram, datetimes are represented as **Temporal objects** — not JavaScript Date objects. Use the built-in expression functions (`Now()`, `FormatDateTime()`, `Add()`, `Subtract()`) to work with them.
  </Card>
  <Card title="File">
    A file reference.

    Used for uploads and file handling workflows.
  </Card>
</CardGroup>

---

## Structured Types

When a single value isn't enough, structured types let you group related data together.

<CardGroup cols={2}>
  <Card title="Enum">
    A value restricted to a fixed set of options.

    If a field can only ever be `"pending"`, `"active"`, or `"archived"`, an enum enforces that. Enums prevent typos and make your data more predictable. They're stored as text internally but validated against the allowed values.
  </Card>
  <Card title="Reference (ref)">
    A pointer to a defined type.

    Instead of describing the same shape of data in multiple places, you define a type once and reference it wherever it's needed. This is how you use database table types, API response types, and custom project types in variables and properties.
  </Card>
</CardGroup>

---

## Arrays

Any type can be made into an array — a list of values of that type. An array of `text` holds multiple strings. An array of `integer` holds multiple whole numbers. An array of a reference type holds multiple structured objects.

Arrays are what the **Repeater** consumes. When you load a list of records from the database and pass them to a Repeater, you're passing an array.

<Note>
  A variable declared as `text[]` holds a list of strings and is distinct from a single `text` value. They are not interchangeable.
</Note>

---

## Where Types Are Used

Types appear throughout Scram wherever you define something that holds a value.

| Context | How types are used |
|---|---|
| **Database fields** | Each column has a type that determines how values are stored and queried |
| **Page variables** | Declaring a type tells Scram what kind of data the variable holds and how to handle expressions that reference it |
| **Component properties** | Types control what values are valid inputs and how they appear in the editor |
| **Component variables** | Internal component state has a type, just like page variables |
| **Action inputs and outputs** | Matching types correctly is what makes expressions resolve cleanly |
| **API response schemas** | Describing the type of an API response lets Scram understand its shape so you can reference it safely in expressions |

---

## Custom Project Types

Beyond the built-in types, you can define your own **project types** — named, reusable shapes that describe structured data specific to your application.

A `CartItem` type might have a `productId` integer, a `quantity` integer, and a `unitPrice` number. An `Address` type might have `line1`, `line2`, `city`, `postcode` — all text.

Once defined, project types can be referenced anywhere a type is expected: page variables, component properties, API schemas. They're the equivalent of defining a data structure once and reusing it throughout your app.

<Tip>
  Define project types when the same shape of data appears in multiple places. It keeps your app consistent and means a structural change only needs to happen in one place.
</Tip>

---

## Type Mismatches

Scram will flag type mismatches when it can detect them. If a property expects a number and you pass a text value, or a variable is declared as a boolean but you try to assign an array to it, you'll see a diagnostic error.

<Warning>
  The most common mismatch to watch for is **text vs. number**. Data coming from user inputs is almost always text, even if the user typed a number. If you need to do arithmetic on it, you may need to convert it first.
</Warning>

---

## Key Things to Know

<AccordionGroup>
  <Accordion title="Be as specific as you can">
    Use `integer` instead of `number` when the value will always be whole. Use `enum` instead of `text` when the value comes from a fixed set. Specificity catches errors early.
  </Accordion>
  <Accordion title="Datetime is not a JavaScript Date">
    Scram uses the Temporal standard. Don't use `new Date()` or `.toISOString()` — use Scram's built-in date/time expression functions instead.
  </Accordion>
  <Accordion title="Arrays are first-class">
    Any type can be an array. A variable, property, or field declared as `text[]` holds a list of strings. This is distinct from a single `text` value and they are not interchangeable.
  </Accordion>
</AccordionGroup>

---

## Related

<CardGroup cols={3}>
  <Card title="Working with the Database" href="/database" />
  <Card title="Working with Expressions" href="/expressions" />
  <Card title="Custom Project Types" href="/project-types" />
</CardGroup>