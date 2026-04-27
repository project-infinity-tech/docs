---
title: "Understanding Variables"
---

# Understanding Variables

**Variables** are containers that store data in your Scram app. They're like your app's short-term memory - holding user inputs, API responses, UI state, and temporary data while users interact with your application.

## 🎯 **What Are Variables?**

Variables store **dynamic data** that changes during your app's lifetime:

- User form inputs (search queries, filter selections)
- Temporary UI state (selected items, active tabs, modal open/closed)
- Results from workflows (API responses before displaying)
- Computed values (cart total, filtered lists)

Unlike database data (which persists), variables **reset when the page reloads**.

## 📍 **Types of Variables**

### **1. Page Variables**

Stored at the **page level** - shared across all components on that page.

**Scope:** Available anywhere on the same page **Lifetime:** Exists while page is open, resets on page reload. **Access:** `vars.variableName`

```
// Example page variables:
vars.searchQuery        // "laptop"
vars.selectedProduct    // {id: 123, name: "MacBook"}
vars.isModalOpen        // true
vars.cartItems          // [{id: 1, qty: 2}, {id: 5, qty: 1}]

```

**Use page variables for:**

- Search/filter inputs shared across the page
- Selected items (clicked product, active tab)
- Modal/drawer open states
- Coordinating state between multiple components

### **2. Component Variables**

Stored **inside a component definition** - private to that component instance.

**Scope:** Only accessible within that specific component **Lifetime:** Exists while component is rendered, resets when unmounted **Access (inside component):** `vars.variableName` **Access (from outside):** `components.componentId.vars.variableName`

```
// Example component variables (inside a "TodoItem" component):
vars.isEditing          // false
vars.editedText         // "Updated todo text"
vars.isHovered          // true

// Access from page:
components.todo123.vars.isEditing  // Check if specific todo is being edited

```

**Use component variables for:**

- Internal component state (hover, focus, expanded)
- Temporary editing buffers
- Component-specific calculations
- Encapsulated behavior (each instance independent)

### **3. Page Data Variables** (Special Type)

**Not regular variables** - these are created automatically by `page-data` workflows.

**Scope:** Page-level, but read-only in expressions **Lifetime:** Loads on page open, can be reloaded **Access:** `pageData.variableName.value` / `pageData.variableName.success`

Page data is discussed in greater detail here [Understanding Page Data](Understanding%20Page%20Data%2011465b4769b58003a439c9df2ab13a9d.md) 

## 📝 **Variable Types**

Variables can hold any data type:

### **Primitive Types**

```
{ type: "text" }        // String: "hello"
{ type: "number" }      // Float: 123.45
{ type: "integer" }     // Integer: 42
{ type: "boolean" }     // Boolean: true/false
{ type: "date" }        // Date: 2024-01-15
{ type: "datetime" }    // DateTime: 2024-01-15 14:30:00

```

### **Complex Types**

```
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
  array: true  // Array of products
}

```

---

## 🎨 **Using Variables**

### **1. In Component Properties**

Bind variable values to component props:

```
{/* Input field bound to variable */}
<pla_textinput
  scram-name="searchInput"
  value={vars.searchQuery}
  onChange="updateSearch"  {/* Workflow updates vars.searchQuery */}
/>

{/* Display variable in text */}
<p scram-name="resultCount">
  Found {vars.filteredProducts.length} results for "{vars.searchQuery}"
</p>

{/* Conditional visibility */}
<div scram-name="modal" scram-visible={vars.isModalOpen}>
  Modal content
</div>

```

### **2. In Workflows**

Read and write variables in workflow actions:

```
<!-- Set variable from user input -->
<step action="SetVariable"
      id="saveSearch"
      variableName="vars.searchQuery"
      value={trigger.payload} />

<!-- Use variable in API call -->
<step action="api-Search Products"
      id="search"
      query={vars.searchQuery}
      limit={20} />

<!-- Store API result in variable -->
<step action="SetVariable"
      id="saveResults"
      variableName="vars.searchResults"
      value={steps.search.output.value} />

```

### **3. In Expressions**

Use variables in computed expressions:

```
// Filter array based on variable
{vars.allProducts.filter(p => p.category === vars.selectedCategory)}

// Compute total from variable
{vars.cartItems.reduce((sum, item) => sum + (item.price * item.qty), 0)}

// Conditional logic
{vars.isLoggedIn ? 'Welcome back!' : 'Please log in'}

// String interpolation
{`Showing ${vars.filteredItems.length} of ${vars.totalItems} items`}
```