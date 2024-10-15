## A Brief Intro

JavaScript is a high level, object oriented, multi-paradigm programming language.

**ECMAScript** is **a standard for scripting languages, including JavaScript, JScript, and ActionScript**. It is best known as a JavaScript standard intended to ensure the interoperability of web pages across different web browsers.

Modern JavaScript - from ESMA 2015 and so on. Modern JavaScript Engine has backward compatible. They believe in the principle of **"Don't break the Web"**.

* Old features never removed.
* They provide just incremental updates.
* Website keep working forever.

**Babel** is a free and open-source JavaScript transcompiler that is mainly used to convert ECMAScript 2015+ code into backwards-compatible JavaScript code that can be run by older JavaScript engines. It allows web developers to take advantage of the newest features of the language

**Polyfilling** and **transpiling** are essential strategies in modern web development that provide distinct challenges. **Polyfilling addresses absent features in older browsers while transpiling streamlines code for cross-version harmony**. Both techniques contribute to a seamless and up-to-date web development landscape.

**Webpack and Parcel** is a tool that **lets you bundle your JavaScript applications** (supporting both ESM and CommonJS).

## Linking JS files

`script.js`
```js
let js = "Amazing";
if(js === 'Amazing'){
    alert("JavaScript is Amazing");
}
console.log("Hello");
```
`index.html`
```html
<!DOCTYPE html>
<body>
</body>
<script src="script.js"></script>
</html>
```
## Variables

The only two special case character we can use while declaring variables.

```js
let $firstName = "Sandeep"
let _firstName = "Sandeep"
```

==**NOTE:**== 
The `$` in the variable name is only part of the name, but the convention is to use it to start variable names when the variable represents a jQuery object.

## Data Types

7 Primitive Data types

1. Number - for decimals and integers.
2. Strings
3. Boolean - true or false.
4. Undefined - empty, declared but not assigned.
5. Null - empty value.
6. Symbol (ES 2015) - not so useful now. 
7. BigInt (ES 2020) - large integers.

**Checking the type of variable**

```js
typeof(varName)
```

## let, const, var

* `let` - mutable.
* `var` - mutable.
* `const` - immutable, we need an initial value.

==**NOTE:**== 
* Use `const` frequently.
* Never use `var`

**let vs var**
var and let are both used for variable declaration in javascript but the difference between them is that var is function scoped and let is block scoped.

```js
<script>
    // calling x after definition
    var x = 5;
    document.write(x, "\n"); // prints 5
    
    // calling y after definition
    let y = 10;
    document.write(y, "\n"); // prints 10
    
    // calling var z before definition will return undefined
    document.write(z, "\n"); // prints undefined
    var z = 2;
    
    // calling let a before definition will give error
    document.write(a); // gives an error
    let a = 3;
</script>
```

## Strings

**String Concatenation**

```js
// String concatenation
let firstName = "Sandeep";
let lastName = "Dewangan";

console.log(firstName + ' ' + lastName);
```

**Template Literals**

```js
const firstName = "Sandeep";
const lastName = "Dewangan";
const job = "Programmer";
const organization = "CTE(V)"

console.log(`I am ${firstName} ${lastName} working as ${job} at ${organization}`);
```

**Multi-line text**

```js
const multiLineText = `This is a
multiline
Text`;

console.log(multiLineText);
```

## Type conversion and coercion

**Type Conversion**

```js
const inputYear = '1990'
console.log(Number(inputYear) + 23);
```

**Type Coercion**

Type Coercion refers to the process of automatic or implicit conversion of values from one data type to another.

```js
const firstName = "Sandeep";6
const age = 33;
console.log(firstName + 'and' + age);
```

```js
console.log('10' - '2'); // 8
```

```js
let n = '1' + 1;
n = n - 1;
console.log(n); // 10
```

## Truthy and Falsy Values

There are five falsy values: 
`0, '', undefined, null, NaN`


## Equality Operators

Loose equality operator is `==` which uses type coercion whereas `===` uses does not uses coercion.

```js
18 === 18
true

18 == 18
true

18 == '18' // type coercison
true

18 === '18'  // no type coercison
false

18 !== 18
false
```

## Logical Operators

| AND | &&   |
| --- | ---- |
| OR  | \|\| |
| NOT | !    |

## Switch Statements

```js
const day = 'monday';

switch(day){
    case 'monday':
        console.log("Plan a course");
        break;
    case 'tuesday':
        console.log("Plan a meditation session");
        break;
    default:
        console.log("Do nothing...");
}
```

## Conditional (Ternary) Operator

```js
const age = 16

const res = age >= 18 ? 'Allowed' : 'Not Allowed';
console.log(res);
```


## Functions

Basic Function 

```js
function logger(){
    console.log("In the logger function");
}
// calling
logger();
```

Function with Parameters

```js
function logger(firstName, lastName){
    console.log(`The name of student is: ${firstName} and last name is ${lastName}`);
}
logger('sandeep', 'dewangan');
```

Anonymous Function

```js
const calAge = function (birthYear){
    return 2024 - birthYear;
}
```

Arrow Function

```js
const calAge = birthYear => 2024 - birthYear;
console.log(calAge(1996));
```

```js
const yearsUntilRetirement = birthYear => {
    const age = 2024 - birthYear;
    const retirement = 62 - age;
    return retirement;
}
```

Arrow Function with multiple parameters

```js
const yearsUntilRetirement = (birthYear, firstName) => {
    const age = 2024 - birthYear;
    const retirement = 62 - age;
    return `${firstName} will retire after ${retirement} years.`;
}
console.log(yearsUntilRetirement(1990, "Sandeep"));
```

## Arrays

```js
// creating arrays
const friends = ['Khushbu', 'Darsh', 'Garv'];
const years = new Array(1996, 2021, 2015);

// accessing
friends[0];

// modification
// only primitive values are mutable not an array.
friends[1] = 'Cherry';

// we cannot replace all the array
friends = ['A', 'B']
```

## Objects

```js
// Creating objects
const sandeep = {
    firstName: 'Sandeep',
    lastName: 'Dewangan',
    age: 34,
    job: 'Programmer',
    hobbies: ['Playing Tennis', 'Programming', 'Animation']
}

// accessing object
console.log(sandeep.lastName);
console.log(sandeep['lastName']);

// modified
sandeep.lastName = 'Kosta';

// added dynamically
sandeep.isProf = false;  

console.log(sandeep.lastName); // Kosta
console.log(sandeep.isProf); // false
```

## Object Methods

```js
const sandeep = {
    firstName: 'Sandeep',
    lastName: 'Dewangan',
    age: 34,
    
    calAge: function (birthYear){
        return 2024 - birthYear;
    }
}

sandeep.calAge(1990);
sandeep['calAge'](1990);
```

`this` keyword

```js
const sandeep = {
    firstName: 'Sandeep',
    lastName: 'Dewangan',
    birthYear: 1990,
    
    calAge: function (){
        return 2024 - this.birthYear;
    }
}

sandeep.calAge();
```

Dynamic Property 

```js
const sandeep = {
    firstName: 'Sandeep',
    lastName: 'Dewangan',
    birthYear: 2000,
    
    calAge: function (){
        this.age = 2024 - this.birthYear;
    }
}
// one time call to a function.
sandeep.calAge();
// use as property any time.
console.log(sandeep.age);
```

## Loops

```js
// for loop
for(let i = 0; i <=10; i++){
    console.log(`Index: ${i}`);
}

// while loop
let rep = 1;
while(rep <= 10){
    console.log('While loop called');
    rep++;
}
```


