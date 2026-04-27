---
title: "Understanding Expressions"
---

# Understanding Expressions

When writing an expression, you can access a range of local data depending on where the expression is used. The Expression Builder will eventually abstract this away, but until then this page serves as a reference.

---

## On a Page

| Expression | Description |
|---|---|
| `pageData.<pageDataName>.value` | The value returned by the Page Data request. Traverse the returned structure to access fields and arrays. |
| `pageData.<pageDataName>.success` | Whether the Page Data request was successful. |
| `queryParams.<queryParam>` | The value of a page query parameter. |
| `pathParams.<pathParam>` | The value of a URI path parameter. |
| `component.vars.<varname>` | A variable on the current component only — not page-level variables. |
| `components.<componentId>.vars.<varname>` | A variable on any accessible component. Subject to composite access rules. |

---

## In a Repeater

| Expression | Description |
|---|---|
| `current.data.<name>` | The data for the current slot. |
| `current.index` | The index of the current slot (starts at 0). |
| `repeater.data` | The full dataset being repeated over. |
| `repeater.data.length` | The number of entries the repeater will iterate over. |
| `repeater.next` | The next value in the list. |
| `repeater.prev` | The previous value in the list. |
| `parentRepeater` | Refers to the repeater that contains this repeater. Chain with `parentRepeater.parentRepeater` for deeper nesting. |

### Striped Rows

To alternate background colours on repeater rows:

```js
current.index % 2 === 0 ? theme.colors.secondary["100"] : theme.colors.primary["100"]
```

---

## In Composite Components

### Accessing Data

| Expression | Description |
|---|---|
| `props.<varName>` | Any property exposed by this composite. |
| `vars.<varname>` | A variable on the current component (from within the component). |
| `components.<componentId>.vars.<varname>` | A variable on any component within the composite, or on the parent page. |

### Custom Event Payloads

When emitting an event, you define the payload as a JavaScript object. For example, if your event has two fields — `payA` (a string) and `payB` (an integer):

```js
{ payA: "some value", payB: 42 }
```

To include expressions in payload fields, wrap the value in backticks and use `${}` for the expression:

```js
{ "firstName": `${components.cAI_001JM.vars.firstName}`, "familyName": `${components.cAI_001JM.vars.familyName}` }
```

To pass a query param as a payload field:

```js
`${queryParams.email}`
```

In the workflow that receives the event, access payload fields via `trigger.payload.<fieldName>`.

---

## In Workflows

| Expression | Description |
|---|---|
| `steps.<stepId>.output.success` | `true` if the step succeeded, `false` if there was an error. |
| `trigger.payload.<fieldName>` | A variable from a triggered component event. |
| `trigger.payload.newValue` | The new value from an `onChange` trigger. |
| `trigger.payload.oldValue` | The previous value from an `onChange` trigger. |

<Note>
  Autocomplete only shows step IDs for steps that produce output. Steps that only log or perform side effects won't appear.
</Note>

### HTTP API Steps

For steps that call an HTTP API, the following are available on the step output:

| Expression | Description |
|---|---|
| `steps.<stepId>.output.additional.requestUrl` | The full URL contacted, including query parameters. |
| `steps.<stepId>.output.additional.status` | The HTTP status code received (e.g. `200`, `404`). |
| `steps.<stepId>.output.additional.statusMessage` | The server's status message string. |
| `steps.<stepId>.output.additional.headers['content-type']` | A specific response header. All header keys are lowercase. |

---

## Visibility & Style Expressions

Visibility conditions do not need `{{}}` — just write the boolean expression directly.

For style expressions, use the ternary pattern:

```js
{{ something-to-evaluate ? value-if-true : value-if-false }}
```

For example, toggling a background colour:

```js
{{ something-to-evaluate ? theme.colors.primary["200"] : theme.colors.secondary["200"] }}
```

<Warning>
  Always use straight quotes (`"200"`) not smart/curly quotes (`"200"`) inside expressions. Copying from some editors or documents can silently introduce smart quotes that will break your expression.
</Warning>

Use `==` for loose equality or `===` for strict equality in conditions.

---

## Theme Values

You can reference your app's theme defaults inside any expression:

```js
theme.text.md
theme.colors.primary["200"]
```

---

## The User Object

When a user is logged in, their data is available via the `user` context:

| Expression | Description |
|---|---|
| `user.id` | The user's ID (sequentially generated integer starting at 1). |
| `user.email` | The user's email address. |
| `user.firstname` / `user.givenname` | The user's first name. |

To safely check whether a user is logged in:

```js
user?.id !== undefined
```

---

## Arrays in Expressions

To define an inline array within an expression:

```js
{{ [ { ...user1_stuff }, { ...user2_stuff } ] }}
```

---

## Useful Functions

| Function | Description |
|---|---|
| `.toString()` | Converts an integer to a string for display. |
| `JSON.stringify()` | Serialises an object to a JSON string. |