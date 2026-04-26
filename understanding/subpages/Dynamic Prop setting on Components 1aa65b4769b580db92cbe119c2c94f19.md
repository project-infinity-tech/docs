# Dynamic Prop setting on Components

Note this is current as at March 2025 and may well change.

Parameters that are passed into a composite do so via “props” (properties) that are defined on the composite.

You cannot set a prop directly from an action. To set a prop from a dynamic value you need to :

- Create a variable in the app to store the dynamic value
- Set the Prop to take the value of the variable
- Set the Variable in an action