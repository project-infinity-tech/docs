---
title: "Understanding Variables"
---


Variables are containers that store data in your Scram app. They're like your app's short-term memory — holding user inputs, API responses, UI state, and temporary data while users interact with your application.

🎯 What Are Variables?
Variables store dynamic data that changes during your app's lifetime:

* User form inputs (search queries, filter selections)
* Temporary UI state (selected items, active tabs, modal open/closed)
* Results from workflows (API responses before displaying)
* Computed values (cart total, filtered lists)
Unlike database data (which persists), variables reset when the page reloads.

📍 Types of Variables
1. Page Variables
Stored at the page level — shared across all components on that page.

* Scope: Available anywhere on the same page Lifetime: Exists while page is open, resets on page reload Access: vars.variableName

```javascript
vars.searchQuery        // "laptop"
vars.selectedProduct    // {id: 123, name: "MacBook"}
vars.isModalOpen        // true
vars.cartItems          // [{id: 1, qty: 2}, {id: 5, qty: 1}]
```
Use page variables for:

* Search/filter inputs shared across the page
* Selected items (clicked product, active tab)
* Modal/drawer open states
* Coordinating state between multiple components
2. Component Variables
Stored inside a component definition — private to that component instance.

* Scope: Only accessible within that specific component Lifetime: Exists while component is rendered, resets when unmounted Access (inside component): vars.variableName Access (from outside): components.componentId.vars.variableName

```javascript
vars.isEditing          // false
vars.editedText         // "Updated todo text"
vars.isHovered          // true

// Access from page:
components.todo123.vars.isEditing
```
Use component variables for:

* Internal component state (hover, focus, expanded)
* Temporary editing buffers
* Component-specific calculations
* Encapsulated behaviour (each instance independent)
⚠️ Repeater limitation: Components inside a Repeater cannot be addressed by component ID from outside. components.childId.vars.x will fail because rows are dynamically rendered. Inside a Repeater's own workflow, use current.data.fieldName to access row data instead.

⚠️ SetVariable limitation: A workflow triggered by a component cannot use SetVariable to write to that same trigger component's own variables. Use a page variable or another component's variable as the target instead.

⚠️ No optional: true on workflow-set variables: Variables that will be written to by workflows must not be marked optional — doing so causes validation errors when the workflow runs.

3. Page Data Variables (Special Type)
Not regular variables — these are created automatically by page-data workflows.

* Scope: Page-level, read-only in expressions Lifetime: Loads on page open, can be reloaded on demand Access: page.data.variableName.value / page.data.variableName.success Loading state: page.dataMeta.variableName.loading (true while fetching)

Page data is discussed in greater detail in [Understanding Page Data].

📝 Variable Types
Primitive Types
```json
{ type: "text" }        // String: "hello"
{ type: "number" }      // Float: 123.45
{ type: "integer" }     // Integer: 42
{ type: "boolean" }     // Boolean: true/false
{ type: "date" }        // Date: 2024-01-15
{ type: "datetime" }    // DateTime: 2024-01-15 14:30:00
{ type: "time" }        // Time: 14:30:00
{ type: "File" }        // A file object (e.g. from a file picker)
{ type: "enum",
  values: ["a","b"] }   // One of a fixed set of values
```
Complex Types
```json
// Database record
{
  type: "ref",
  ref: "Users",
  namespace: "o_scramdb",
  validators: {}
}

// Custom type
{
  type: "ref",
  ref: "CartItem",
  namespace: "o_project-types",
  validators: {}
}

// Array of items
{
  type: "ref",
  ref: "Products",
  namespace: "o_scramdb",
  validators: {},
  array: true
}
```
🎨 Using Variables
1. In Component Properties
Bind variable values to component props:

```html
{/* Display variable in text */}
<p scram-name="resultCount">
  Found {vars.filteredProducts.length} results for "{vars.searchQuery}"
</p>

{/* Conditional visibility */}
<div scram-name="modal" scram-visible={vars.isModalOpen}>
  Modal content
</div>
```
Reading input values directly Platform input components (text fields, dropdowns, etc.) expose their current value as a built-in component variable. You can read components.inputId.vars.value directly in expressions — you don't need a workflow to copy the value into a page variable first.

A note on expressions in props Prop expressions re-run on every render. Avoid putting heavy computations directly in a prop (e.g. filtering a large array inline) — it will run continuously as the page updates. Instead, compute the result once in a workflow, store it in a variable, and bind that variable to the prop.

2. In Workflows
Read and write variables in workflow actions:

```xml
<!-- Set a variable -->
<step action="SetVariable"
      id="saveSearch"
      variable="vars.searchQuery"
      value={trigger.payload} />

<!-- Use variable in an action -->
<step action="api-SearchProducts"
      id="search"
      query={vars.searchQuery}
      limit={20} />

<!-- Store result in variable -->
<step action="SetVariable"
      id="saveResults"
      variable="vars.searchResults"
      value={steps.search.output.value} />
```
3. In Expressions
```javascript
// Conditional logic
{vars.isLoggedIn ? 'Welcome back!' : 'Please log in'}

// String interpolation
{`Showing ${vars.filteredItems.length} of ${vars.totalItems} items`}

// Accessing a nested value
{vars.selectedProduct.name}
```