---
title: "Understanding Variables"
---

Variables are containers that store data in your Scram app — holding user inputs, UI state, workflow results, and temporary values while users interact with your application. Unlike database data, variables reset when the page reloads.

---

## Types of Variables

### Page Variables

Page variables are stored at the page level and are available to every component on that page.

- **Scope** — anywhere on the same page
- **Lifetime** — exists while the page is open, resets on reload
- **Access** — `vars.variableName`

Use page variables for search and filter inputs shared across the page, selected items, modal open/closed states, and coordinating state between multiple components.

### Component Variables

Component variables are stored inside a component definition and are private to that component.

- **Scope** — within that specific component instance
- **Lifetime** — exists while the component is rendered
- **Access from inside** — `vars.variableName`
- **Access from outside** — `components.componentId.vars.variableName`

Use component variables for internal component state (hover, focus, expanded), temporary editing buffers, and component-specific calculations where each instance should behave independently.

### Page Data Variables

Page data variables are a special type — created automatically by page-data workflows and available as read-only values in expressions.

- **Access** — `page.data.variableName.value`
- **Success state** — `page.data.variableName.success`
- **Loading state** — `page.dataMeta.variableName.loading`

See [Understanding Page Data](/understanding/understanding-page-data) for full details.

---

## Variable Types

Variables can hold any of Scram's standard data types — text, number, integer, boolean, date, datetime, time, file, or enum. They can also hold structured types — a reference to a database table type, a custom project type, or an array of any of these.

See [Understanding Data Types](/understanding/understanding-data-types) for the full type reference.

---

## Reading Input Values

Platform input components expose their current value as a built-in component variable. You can read `components.inputId.vars.value` directly in expressions — you don't need a workflow to copy the value into a page variable first.

---

## Using Variables in Expressions

Access variable values directly in component properties and expressions:

```js
vars.searchQuery              // a page variable
vars.selectedProduct.name     // accessing a field on a structured variable
components.myInput.vars.value // reading an input component's current value
```

<Tip>
  Prop expressions re-run on every render. Avoid heavy computations directly in a prop — filter a large array in a workflow instead, store the result in a variable, and bind that variable to the prop.
</Tip>

---

## Gotchas

<Warning>
  **Repeater limitation** — components inside a Repeater cannot be addressed by component ID from outside. `components.childId.vars.x` will fail because rows are dynamically rendered. Inside a Repeater's workflow, use `current.data.fieldName` to access row data instead.
</Warning>

<Warning>
  **SetVariable limitation** — a workflow triggered by a component cannot use SetVariable to write to that same trigger component's own variables. Use a page variable or another component's variable as the target instead.
</Warning>

<Warning>
  **No `optional: true` on workflow-set variables** — variables that will be written to by workflows must not be marked optional. Doing so causes validation errors when the workflow runs.
</Warning>