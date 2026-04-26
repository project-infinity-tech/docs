# Understanding Expressions

When writing an Expression, you can access a range of local data if you know where to find them. In future the Expression Builder will abstract this all away so you don’t need to remember the right paths, but until then this page provides a reference:

# On a Page

- `pageData.*<pageDataName>*`
    - `.value` - the value returned by the Page Data request.
        - You can then just traverse the returned structure, accessing fields and arrays.
    - `.success` - check if the Page Data request was successful.
    - *etc - see Workflow step output for other relevant properties.*
- `queryParams*.<queryParam>*` - access the value of a page parameter.
- `pathParams.*<pathParam>*` - access the value of a URI path parameter.
- `component.vars.*<varname>` -* access variables on the current component.
    - NOTE - this is now the **component’s variable only, not one added by the app (as they are on the page only now)**
- `components.*<componentId>*.vars.*<varname>*` - access a component’s variable.
    - Note that there are access rules controlling exactly what is visible from any particular place on the Page: [Composite Rules](https://www.notion.so/Composite-Rules-baa5dee5da5645ee86fff9848f9b8d91?pvs=21).

# Repeater

- `current.data.*<name>`* - access “this” data
- `current.index` - access the index of “this” slot (starts from 0)
- `repeater`
    - `.data` - the data being repeated over
        - `.length` - the number of entries the repeater will repeating over
    - `.next` - the next value in the list
    - `.prev` - the previous value in the list
    - `parentRepeater` allows you to refer to the repeater that a repeater is within (and then `parentRepeater.parentRepeater` etc)
- Make it stripey with background colour
    - `current.index % 2 === 0 ? theme.colors.secondary["100"] : theme.colors.primary["100"]`

# Composite Components

## Properties

- `props.*<varName>*` - access any property exposed by this composite.
- `vars.*<varname>` -* access variables on the current component (from within the component)
- `components.*<componentId>*.vars.*<varname>*` - access external variables on any component within the composite or on the component on the page.

## Custom Events

To specify an event payload when Emitting an Event you create a Javascript object where each payload field is assigned a value, ie. if you have two fields `payA` (a string) and `payB` (an integer) then you specify the payload input as `{ *payA*: "some value", *payB*: 42 }`.

Within the Workflow, you then pull these back out with `trigger.payload.payA` (see below). 

### Sending Event Payload

If you are emitting events that have payload fields that need an expression, you will need to wrap the value in back ticks ` and then use ${} to add in the expression. Nope, not a clue either.

Example of sending firstname and familyname as two payload fields.

```jsx
{ "firstName": `${components.cAI_001JM.vars.firstName}`, "familyName": `${components.cAI_001JM.vars.familyName}` }
```

 

```jsx
`${queryParams.email}`
```

# Workflows

- `steps.*<stepId>*.output`  *- **note: you will only get autocomplete of stepIds for steps that have some form of output; you won’t ever see IDs for events that log, etc.***
- Rewriting as at April 2025 as below has changed considerably.
    - `.success` - true if it succeeded, false if there was an error.
    
- Deprecated from here
    - `.value` - the output of a previous step, if it was successful and returns something (else undefined).
    - `.errorCode` - a Scram error code, always present if an error occurred.
    - `.error` - the error response of the previous step, if it failed and returns something when an error occurs (else undefined).
    - `.additional` - optional additional info about the step, which will be Action specific
        - `.requestUrl` (for HTTP APIs) - the URL that was contacted, including any query parameters.
        - `.status` (for HTTP APIs) - the integer HTTP status code that was received, eg. 200 or 404 (always present if the server responded, or undefined if we couldn’t connect).
        - `.statusMessage` (for HTTP APIs) - the server’s string status message.
        - `.headers` (for HTTP APIs) - a map of all headers sent by the server where key is in lower case, eg. to get the Content-Type header use `.headers['content-type']`. (think this should be ‘content-type’)
- `trigger.payload.<payloadvarname>` - reference a variable on a Triggered event from a Component.
- For “On - Change” actions on an input`trigger.payload.newValue`  - the new value in the input (also oldValue if needed)
- Boolean Expression in Visibility
    - Visibility does not need {{}}
    - Expressions to control styles
    - Method 1
        - {{ something-to-evaluate-to-true ? value-if-true : value-if-false }}
        - `{{ something to evaluate to true ? theme.colors.primary["200"] : theme.colors.secondary["200"] }}`
    - If / Else
        - You need to use == as equals or === as really really equals
- If a variable / prop is Boolean you get `valueOf`  - what is this?
- In Expressions, you can refer to the theme defaults with `theme.xxxxxx.xx`
    - For example `theme.text.md`  or `theme.colour.primary["200"]`
        - Note you MUST use straight quotes `"200"` not smart one like this > “200” so copying out of here can be dangerous!

An array inside an expression 

 `{{ [ { ...user1_stuff }, { ......user2_stuff } ] }}`

# User

You can access a logged-on User’s data via the User Context in expressions `user.xxxx`

- `User.id` - id of the user, an integer. You would usually use this to update the user details. Sequentially generated starting at 1.
- `User.email` - id of the user, and integer. You would usually use this to update the user details
- `User.firstname User.givenname` - name !
- 

Checking if the user is logged on or not … `user?.id !== undefined` is safest 

# Useful Functions

- `.toString()` turns an integer into a string so you can display it nicely
- JSONSTringify

# Links

The link type is an object as follows

# Examples

current.index === 0 ? theme.colors.primary[’200’] : theme.colors.secondary[’200’] 

current.index === components.cAC_00004.vars.currentStep ? theme.colors.primary[”200”]  : theme.colors.secondary[”200”] 

```json
{
"id": 1,
"created_at": "2024-08-09T08:25:14.540034+00:00",
"code": "ABCF",
"phoneType": "Phoney"
}
```

```json
steps.sAB_0009S.output.value.id = 1
```

If the prop leftisPrimary is true then set the colour to primary (200

`{{ props.leftIsPrimary ? theme.colors.primary["200"] : theme.colors.secondary["200"] }}`

`{{ !props.leftIsPrimary ? theme.colors.primary["200"] : theme.colors.secondary["200"] }}`

```json
[
{
"id": 1,
"created_at": "2024-08-09T08:25:14.540034+00:00",
"code": "ABCF",
"phoneType": "Phoney"
},
{
"id": 2,
"created_at": "2024-08-09T08:25:14.540034+00:00",
"code": "SNVV",
"phoneType": "Sammy"
}
]
```

```json
steps.sAB_0009S.output.value[1].id = 2
```

`const a = 1;const b = 2;const together = `${a} + ${b}``

`together = “1 + 2”`

`const together = ‘${a}+ ${b}’;`

`together = ‘${a}+ ${b}’`