# Reload Page Data

# Reload Page Data — Workflow Action

**Reload Page Data** re-runs a page-data workflow and refreshes the data it provides to the page. It is how you tell the UI that something has changed on the server and it should go and fetch the latest version.

---

## What is Reload Page Data?

When a page loads, its **page-data workflows** run automatically and populate the page with data — a list of records, the current user's profile, a set of configuration values. That data is then held in memory as `page.data.name.value`.

That snapshot does not update itself. If a user submits a form, adds a record, or deletes an item — and a database write happens as a result — the page is still showing the old data. Reload Page Data is the action that fixes this. It re-runs the specified page-data workflow, gets the fresh result from the server, and the UI updates automatically to reflect it.

---

## Inputs

### Target Page Data

The specific page-data workflow to re-run. Referenced as `page.data.variableName`.

A page can have multiple page-data workflows — one for a list of products, another for a summary count, another for user preferences. You target only the one (or ones) that are affected by the change that just happened. There is no need to reload everything if only one dataset has changed.

If you need to refresh all page-data workflows at once, use **Reload All Page Data** instead.

---

## How it Works

When Reload Page Data executes:

1. The targeted page-data workflow runs again from the beginning, exactly as it did on page load
2. While it runs, `page.dataMeta.name.loading` is `true` — useful for showing a loading indicator
3. When it completes, `page.data.name.value` is replaced with the new result
4. Any component on the page that reads from that data **re-renders automatically**

The rest of the page is unaffected. Components reading from other data sources, variables, or unrelated page-data workflows see no change.

---

## When to Use It

Reload Page Data belongs **after a mutation** — any workflow step that changes data on the server:

- After inserting a new database record, to show the updated list
- After updating a record, to reflect the new field values
- After deleting a record, to remove it from the displayed list
- After a form submission that changes server-side state

It should appear in the **true branch** of the If/Else that follows the mutation step — only reload if the write actually succeeded.

---

## Common Pattern

A user clicks "Add Item". The workflow:

```
1. ExecuteSQL — INSERT the new record
2. If/Else (did it succeed?)
   true:
     3. Reload Page Data → page.data.items
     4. SetVariable vars.isModalOpen = false
   false:
     3. SetVariable vars.errorMessage = "Failed to add item. Please try again."
```

The list on the page now shows the newly added item without the user needing to refresh the browser.

---

## Alternatives and When to Choose

| **Approach** | **When to use** |
| --- | --- |
| **Reload Page Data** | After a mutation, to re-fetch the affected dataset from the server |
| **Reload All Page Data** | After a mutation that affects multiple datasets at once |
| **Set Variable** | When you can update local state directly without a round-trip (e.g. appending to a local array) |

The Set Variable approach is faster — no server round-trip — but means the local state can drift from the database if anything else has changed it concurrently. Reload Page Data is slower but always gives you the true current state from the server. For most user-facing apps, Reload Page Data is the safer and simpler choice.

---

## Loading States

While a reload is in progress, the page-data meta flag is available:

```
page.dataMeta.name.loading === true
```

You can bind a spinner's visibility to this expression so the user sees feedback while the data is being refreshed, rather than the list appearing to freeze between the old and new states.

---

In summary: Reload Page Data is the **refresh signal** — the action that closes the loop after a mutation by ensuring the UI reflects what is actually in the database, rather than continuing to display a stale snapshot from when the page first loaded.