# Reload All Page Data

# Reload All Page Data — Workflow Action

**Reload All Page Data** re-runs every page-data workflow on the current page simultaneously and refreshes all of their results at once. It is the broad equivalent of **Reload Page Data** — use it when a single action on the page has affected multiple datasets at once.

---

## What is Reload All Page Data?

It behaves identically to Reload Page Data, except it targets **every page-data workflow on the page** rather than a single named one. All datasets re-fetch in parallel, and the UI updates as each one completes.

It takes no inputs. There is nothing to configure — it simply fires and reloads everything.

---

## When to Use It

Use Reload All Page Data when a mutation is broad enough that you cannot easily predict which datasets have been affected, or when it is simply more practical than chaining multiple Reload Page Data steps:

- A bulk action that touches many records across different datasets
- An admin operation that affects both a list and its associated summary or aggregate counts
- A setting change that influences multiple independent parts of the page
- Any situation where the affected data spans more than two or three page-data workflows

---

## Reload Page Data vs. Reload All Page Data

|  | **Reload Page Data** | **Reload All Page Data** |
| --- | --- | --- |
| **Targets** | One named dataset | Every dataset on the page |
| **Inputs** | `page.data.variableName` | None |
| **Server calls** | One | One per page-data workflow |
| **Use when** | The mutation affects a known, specific dataset | The mutation is broad, or multiple datasets are affected |
| **Performance** | More efficient | More network activity |

Prefer **Reload Page Data** when you know exactly what changed — it is faster and more precise. Reach for **Reload All Page Data** when the scope of a change is wide or ambiguous, and the cost of a few extra server calls is worth the simplicity.

---

## Loading States

As with Reload Page Data, each individual dataset exposes its own loading flag while it refreshes:

```
page.dataMeta.name.loading === true
```

Since datasets re-fetch in parallel, different parts of the page may finish loading at slightly different times. Each section can independently show or hide a loading indicator based on its own `dataMeta` flag.

---

In summary: Reload All Page Data is the **full refresh signal** — a single no-configuration step that ensures the entire page is back in sync with the server. Reach for it when the scope of a mutation is broad, and reach for the targeted Reload Page Data when precision and efficiency matter.