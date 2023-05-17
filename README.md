# The "missing" Sanity Schema API doc

## schema field properties:

`hidden`: boolean or function 
example:
- hidden: true

- hidden: ({currentUser, value, parent, document}) => {
        return //
    },

`readOnly`: boolean or function 
example:

```javascript
hidden: true
```

```javascript
- hidden: ({currentUser, value, parent, document}) => {
        // option with value
        return value < 5
       // option with parent
        return parent?.externalLink !== undefined
        // option currentUser
        return !currentUser.roles.find(({name}) => name === 'administrator')
      },
    },
```

_function parameter is an object argument with the following  properties:_

name: `document` 
type: `object`

The current state of the document with all its values. Remember that it can return undefined. You can use optional chaining to avoid errors in the console, for example, document?.title.


name: `parent` 
type: `object | undefined`

The values of the field's parent. This is useful when the field is part of an object type. Remember that it can return undefined. You can use optional chaining to avoid errors in the console, for example, parent?.title.
If it's a root field, it will contain the document's values.


name: `value`
type: `any`

The field's current value.


name: `currentUser`
type: `object`

The current user with the following fields:
- email (string)
- id (string)
- name (string)
- profileImage (string)role (string)
- roles (array of objects with name, title, description)

