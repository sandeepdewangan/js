## VS Code

**Code Editor**: VS Code with Monokai Pro Theme and File icon theme to Seti.

**VS Code Editor Settings:**
1. AutoSave -> onFocusChange
2. Multi cursor modifier -> alt
3. FormatOnSave -> turn on

**VS Code Extensions:**

**Prettier - Code formatter**
set prettier to as a default formatter and format on save is also enabled.
Overriding default values of Prettier:
STEP 01: Create a file named `.prettierrc`
STEP 02: Edit a file
```js
{
  "singleQuote": true
}
```
The above lines convert any double quotes to single quotes.

**User Snippets**
Create a user snippets for repeated function usage.

**Auto Rename Tag**: for auto renaming of tags if changed.

**Image Preview**

NPM Install for Live Server
`npm install live-server -g`
run using cmd: `live-server`
## Best Practices

* Use `const` declaration mostly.
* Declare string not in double quotation rather in back ticks ``.


## Strict Mode

Strict mode makes several changes to normal JavaScript semantics:

1. Eliminates some JavaScript silent errors by changing them to throw errors.
2. Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode.
3. Prohibits some syntax likely to be defined in future versions of ECMAScript.

Activate strict mode

```js
'use strict';
```


