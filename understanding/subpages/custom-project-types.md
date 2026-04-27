---
title: "Custom Project Types"
description: "A project type is a named, reusable data structure you define yourself. It describes the shape of a piece of data: what fields it has, and what type each field is."
---

# Custom Project Types

As your app grows, you'll find certain shapes of data appearing in multiple places. A delivery address used in orders, customer profiles, and shipping forms. A price structure with an amount and a currency. A set of coordinates used across a mapping feature. Defining these shapes once — and reusing them everywhere — is what custom project types are for.

---

## What is a Project Type?

A **project type** is a named, reusable data structure you define yourself. It describes the shape of a piece of data: what fields it has, and what type each field is.

Once defined, a project type can be used anywhere a type is expected in Scram — as the type of a page variable, a component property, a component variable, or an API schema.

Think of it as defining your own vocabulary for your app's data.

---

## When to Create One

The clearest signal is when the same group of fields appears in more than one place.

If you find yourself defining `line1`, `line2`, `city`, and `postcode` as separate fields in three different places — create an `Address` type and reference it instead.

Other good candidates:

- **Structured values passed between components** — a component property that carries more than one piece of information
- **Complex page variable state** — a variable that holds a structured object rather than a single value, such as a filter configuration or a selected item with metadata
- **Shared response shapes** — when multiple API endpoints return the same structure, define it once and reference it in each

If a structured shape is only used in one place, it may not need to be a named project type — inline definition is fine. It's the reuse that makes project types worthwhile.

---

## Structure

Project types are defined using **JSON Schema**. Each type has a name and a schema that describes its properties.

A simple example — a `MoneyAmount` type:

```
{
  "type": "object",
  "properties": {
    "amount": { "type": "number" },
    "currency": { "type": "string" }
  },
  "required": ["amount", "currency"]
}
```

Fields can be any of Scram's standard types: text, number, integer, boolean, date, datetime, and so on. Fields can also reference *other* project types, which is how you build nested structures.

---

## Referencing Project Types

Once a type is defined, you reference it using:

- **Type:** `ref`
- **Ref:** the type name (e.g. `Address`)
- **Namespace:** `o_project-types`

This tells Scram to look up your custom type by name rather than using a built-in primitive.

You'll use this pattern when declaring:

- A page variable that holds a structured object
- A component property that accepts a complex value
- A component variable that stores internal structured state

---

## Defining in Dependency Order

If one project type references another, define the inner type first.

If `OrderLine` has a `price` field of type `MoneyAmount`, then `MoneyAmount` must be defined before `OrderLine`. Scram resolves references at definition time, so the referenced type needs to exist first.

A useful mental model: work from the smallest, most atomic types outward to the larger ones that compose them.

---

## Arrays of Project Types

Like any type in Scram, project types can be used as arrays. A variable of type `Address[]` holds a list of addresses. A component property of type `OrderLine[]` accepts an array of order line objects.

This is particularly useful for page variables that hold a working set of structured data — a list of items a user is building up before submitting, for example.

---

## Project Types vs. Database Types

It's worth being clear about the distinction:

**Project types** are for application logic — passing structured data between components, holding complex state in variables, describing the shape of API payloads. They live in your app's logic layer.

**Database table types** describe the shape of rows in your ScramDB tables. They're automatically available as types throughout your app once a table is created, without needing to define them manually.

Use project types for transient, in-app data structures. Use database types when the data is being read from or written to the database.

---

## Key Things to Know

**Names are global within the project.** Project type names must be unique. Use clear, descriptive PascalCase names (`CartItem`, `FilterState`, `ContactInfo`) that make it obvious what the type represents.

**Changing a type affects everything that references it.** If you add or rename a field, any expression or component that uses that field needs to be updated. Make structural changes carefully.

**Project types are not validated at runtime.** Scram uses types to help you in the editor — for autocomplete, diagnostics, and expression checking. At runtime, data isn't automatically rejected for not matching a type's shape. Correct data handling is still your responsibility.

---

## Related

- [Understanding Data Types →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Building Custom Component Definitions →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Working with the Database →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)
- [Connecting External APIs →](https://app.projectinfinity.tech/branch/cmmc094nh00q0p72m8f4d8ejn/fe/app/aAA_p111_00001/page/pAA_p111_00001/settings)