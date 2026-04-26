# Emit Event

# Emit Event — Workflow Action

**Emit Event** is how a component communicates outward to the rest of the app. It is the action that makes custom components truly reusable — instead of hardcoding what should happen when a user interacts with a component, the component announces that something happened and lets the page (or parent component) decide what to do about it.

---

## What is Emit Event?

Emit Event is a **workflow step** that fires a named event from a component, optionally carrying a payload of data with it. Any workflow on the page that is listening for that event will then execute.

It is the outbound half of Scram's event system:

- The component **emits** — it says *"something happened, here's the data"*
- The page or parent **listens** — it decides *"when that happens, do this"*

This separation is what makes component definitions reusable. A `ProductCard` component does not need to know whether clicking it should open a modal, navigate to a page, or add something to a basket. It just emits a `select` event with the product data, and whatever is using it decides the rest.

---

## Inputs

### Target Event

The **named event** to fire. This must be an event that has been defined on the component definition — you cannot emit an arbitrary string. Events are declared on the component definition itself, each with a name and an expected payload type.

Referenced as: `events.eventName`

### Payload

The **data to send with the event**. The payload type is defined when the event is created on the component definition — it might be a text value, a number, a structured object, or nothing at all.

The payload becomes available to any workflow that handles the event via `trigger.payload`.

### Should Stop Propagation

A boolean that controls whether the event continues bubbling up through the component tree after being emitted. Defaults to `true`.

- `true` — the event stops here; only direct listeners on this component will receive it
- `false` — the event continues propagating upward to parent components

In most cases the default of `true` is correct. Set it to `false` only if you intentionally want parent components to also react to the same event.

---

## How it Works

1. A user interacts with a component (clicks a button, submits a form, selects an item)
2. An internal workflow inside the component definition runs, leading to an Emit Event step
3. Emit Event fires the named event, attaching any payload data
4. On the page (or parent component), a workflow triggered by that event executes
5. That workflow can read `trigger.payload` to access the data that was sent

---

## Defining Events on a Component

Before Emit Event can be used, the event must be **declared on the component definition**. Each event has:

- A **name** — what it's called (e.g. `select`, `submit`, `delete`, `close`)
- A **payload type** — the shape of data it carries (text, number, boolean, a structured object type, or nothing)

Once declared, the event appears as a trigger option on any instance of that component placed on a page, just like built-in events (click, change, etc.) on platform components.

---

## Common Patterns

### Passing a selected item to the page

A `ProductCard` component emits a `select` event when clicked:

```
Target Event: events.select
Payload:      current.data
```

On the page, a workflow triggered by `select` runs:

```
SetVariable vars.selectedProduct = trigger.payload
```

### Signalling that a form was submitted

A `ContactForm` component emits a `submit` event with the form values:

```
Target Event: events.submit
Payload:      { name: components.nameInput.vars.value, email: components.emailInput.vars.value }
```

The page workflow then calls an API with `trigger.payload.name` and `trigger.payload.email`.

### Closing a modal from within it

A `Modal` component emits a `close` event when the user clicks the dismiss button:

```
Target Event: events.close
Payload:      (none)
```

The page workflow sets `vars.isModalOpen = false`.

---

## Emit Event vs. Direct Variable Access

You might wonder: why emit an event when a component could just write to a page variable directly?

|  | **Emit Event** | **Direct variable write** |
| --- | --- | --- |
| **Reusability** | ✅ Component stays generic | ❌ Component is coupled to a specific page's variables |
| **Flexibility** | ✅ Page decides what to do | ❌ Behaviour is baked into the component |
| **Clarity** | ✅ Explicit contract between component and page | ❌ Hidden side-effects inside the component |

For one-off components that will only ever live on a single page, writing to a page variable directly is pragmatic and fine. For any component definition intended to be reused, Emit Event is always the right pattern.

---

## Relationship to Other Actions

Emit Event sits at the **boundary** between a component's internal logic and the outside world. Inside a component definition workflow it is typically the **final step** — the component has done its internal work (validated a form, processed a selection, handled a toggle) and now signals the result outward.

On the receiving side, the page workflow triggered by that event will typically use:

- **Set Variable** — to store the payload in page state
- **If/Else** — to branch based on what the payload contains
- **Data source actions** — to persist or fetch data using the payload

---

In summary: Emit Event is the **voice** of a component. It lets a component say *"something meaningful just happened"* without needing to know or care what the rest of the app will do about it. That separation of concerns is what makes well-designed components genuinely reusable.