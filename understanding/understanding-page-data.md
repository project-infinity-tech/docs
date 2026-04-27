---
title: "Understanding Page Data"
---

Every page in a Scram app can have Page Data defined. You'll find it at the bottom of the left-hand panel when a page is selected.

Page Data is data that loads automatically when the page opens — before the user does anything. It's ready and waiting to be displayed as soon as the page appears.

---

## Page Data Variables

You define what data you want available on a page by creating **Page Data Variables**. Each variable holds a particular piece of data that gets loaded when the page opens.

A variable can hold a simple value — like a single piece of text — or a complex structured type, like a Project, which might have multiple fields such as a name, start date, duration, and assigned manager.

Variables can also hold lists. For example, in a Project Management app, your dashboard might load all the projects a user is responsible for. That would be a Page Data Variable typed as a List of Projects.

The data in a variable can come from many places — your internal database, an external API, or even a combination of both. You could fetch project data from an external system and enrich it with additional information from your own database in the same workflow.

<Tip>
  You can also use static data — values you define directly in the workflow itself, like a fixed list of options or a hardcoded configuration value. Static data never changes unless you edit the workflow.
</Tip>

---

## Page Data Workflows

Each Page Data Variable is loaded by a **Workflow** — a series of one or more steps that run in sequence when the page opens.

The simplest workflow is a single step that fetches some data. More complex workflows can chain multiple steps together — for example, calling an API and then querying your database to combine the results.

Each step runs an **Action**. Available actions include:

| Action | Description |
|---|---|
| Execute SQL | Query your internal Scram database directly |
| API call | Fetch data from an external service or data source |
| Scram Filestore | Retrieve stored files |
| Static data | Return a fixed value defined in the workflow itself |

---

## Outputs

At the end of a Page Data workflow, you define what gets stored in the variable. There are two options:

**Inherit** — The variable automatically receives the result of the last step in the workflow. This is the simplest option and is all you need for most cases — for example, fetching a list of rows from your database. If your workflow has multiple steps, Inherit will forward whatever the final step produced.

**Success** — If you need more control — for example, combining results from multiple steps, or shaping the output yourself — you can define exactly what the variable should contain. This gives you full flexibility over the final output.

---

## Page Data is for load-time data only

<Warning>
  Page Data only runs when the page first opens. If you need data to load in response to something the user does — clicking a button, submitting a form, making a selection — that should be handled by a regular workflow, not a Page Data Variable. Using Page Data for user-triggered actions is a common mistake and won't behave as expected.
</Warning>

---

## Reloading Page Data

Page Data can be refreshed during a session using the **Reload Page Data** action inside any workflow. For example, after a user creates a new project, you can trigger a reload so the list on screen updates immediately — without the user having to refresh the page manually.