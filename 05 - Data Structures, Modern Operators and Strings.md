
## De-structuring Arrays

Breaking of arrays

```js
const restaurant = {
  name: 'Indian Coffee House',
  location: 'Ghadi Chowk, Raipur',
  categories: ['Vegeterian', 'Non Vegeterian', 'Chineese', 'Italian'],
  menu: ['Dosa', 'Idly', 'Pav Bhaji', 'Chicken'],
};

// de-structuring
const [cat1, cat2] = restaurant.categories;
// skip second element
const [cat_1, , cat_3] = restaurant.categories;
// default values
const [p = 1, q = 1, r = 1] = [8, 9];
console.log(p, q, r); // 8 9 1
```

## De-structuring Objects

```js
// breaking of arrays
const restaurant = {
  restName: 'Indian Coffee House',
  location: 'Ghadi Chowk, Raipur',
  categories: ['Vegeterian', 'Non Vegeterian', 'Chineese', 'Italian'],
  menu: ['Dosa', 'Idly', 'Pav Bhaji', 'Chicken'],
};

// De-structuring
const { restName, menu } = restaurant;
console.log(restName, menu);

// custom variable name
const { restName: name, menu: tags } = restaurant;
console.log(name, tags);

// default values if not exist and custom variable name
const { restName: rname = [] } = restaurant;
console.log(rname);

// Mutating variables
let a = 'Indian Chilly';
const obj = { a: 1, b: 2, c: 3 };
// { a } = obj; // Uncaught SyntaxError, Unexpected token '='
({ a } = obj);
console.log(a); // 1

// Named parameter with default values
function order({ menuIndex = 0, time = '20:00', address }) {}
order({ menuIndex: 1, time: '07:00', address: 'Raipur' });

```

## Spread Operator - Expand

Unpacking all the array elements at once.

**Shallow copy:** When a reference variable is copied into a new reference variable using the assignment operator, a shallow copy of the referenced object is created. If the state of the object changes through any of the reference variables it is reflected for both.

**Deep copy:** Unlike the shallow copy, deep copy makes a copy of all the members of the old object, allocates a separate memory location for the new object, and then assigns the copied members to the new object.

```js
const arr = [1, 2, 3];
const spreadOp = [...arr, 4, 5, 6];
console.log(spreadOp); // [1, 2, 3, 4, 5, 6]

console.log(...arr); // 1 2 3

// copy of an array
const arrCopy = [...arr];
console.log(arrCopy);

//  calling methods
function orderPizza(ing1, ing2, ing3) {
  console.log(
    `The order is confirmed with ingredients: ${ing1}, ${ing2}, ${ing3}`
  );
}

const indigredients = ['Pizza', 'Fresh Pan', 'Paneer'];
orderPizza(...indigredients);

// Objects
const sandeep = {
  name: 'Sandeep',
  position: 'Programmer',
  age: 34,
};

const newSandeep = { ...sandeep, DOB: 1990, isResigned: false };
console.log(newSandeep);
// {name: 'Sandeep', position: 'Programmer', age: 34, DOB: 1990, isResigned: false}

```


==Side Notes:====
* Maps, arrays, strings, sets are iterables.
* Object is not iterables.

## Rest Operator - Compress

Packing of elements into an array.

```js
// SPREAD, Right hand side of = operator
const arr1 = [1, 2, 3, ...[4, 5]];

// REST, Left hand side of = operator
const [ar1, ar2, ...others] = arr1;
console.log(ar1, ar2, others); // 1 2 [3, 4, 5]

// function
const add = function (...numbers) {
  console.log(numbers);
};
add(2, 3); // [2, 3]
add(2, 3, 4, 5); // [2, 3, 4, 5]
```

### Short Circuiting (&&, ||)

OR operator

```js
// returns 3, first encounter the truth value.
console.log(3 || 'Sandy'); // 3
console.log('' || 'Sandy'); // Sandy
console.log(undefined || null); // null, here both are falsy value.

// With ternarary operator
let numGuests = 0;
const guestsDemo1 = numGuests ? numGuests : 10;
console.log(guestsDemo1); // 10 bez numGuests is 0 which is falsy value.

// With short circuiting
const guestsDemo2 = numGuests || 10;
console.log(guestsDemo2); // 10
```

AND Operator
```js
console.log(0 && 'Sandy'); // 0, bez of falsy value
console.log(3 && 'Sandy'); // Sandy
console.log(undefined && null); // undefined
```

## Nullish Coalescing Operator (??)

Coalescing operator works with only null and undefined.

```js
let numGuests = null;
const guests1 = numGuests ?? 10;
console.log(guests1); // 10

let numGuests = 5;
const guests1 = numGuests ?? 10;
console.log(guests1); // 5
```

## Logical Assignment Operator

```js
const hotel1 = {
  name: 'ABC',
  rooms: 10,
};

const hotel2 = {
  name: 'XYZ',
};
hotel1.rooms = hotel1.rooms || 5;
hotel2.rooms = hotel2.rooms || 5;

console.log(hotel1, hotel2);
//  {name: 'ABC', rooms: 10}
//  {name: 'XYZ', rooms: 5}

// above code using logical assignment operator
hotel1.rooms ||= 5;
hotel2.rooms ||= 5;
console.log(hotel1, hotel2);

// OR with nullish coalescing assignment operator
hotel1.rooms ??= 5;
hotel2.rooms ??= 5;
console.log(hotel1, hotel2);
```

## Looping Arrays

For-of Loop:

```js
const hotel = {
  name: 'Abc',
  estbYear: 2021,
  owner: 'Sandeep',
};

const hotelItem = [hotel.name, hotel.estbYear, hotel.owner];

for (const item of hotelItem) {
  console.log(item);
}
```

## Enhanced Object Literals

Advanced usage of properties and methods.

```js
const locations = {
  Raipur: {
    name: 'Aquaplast Infracon',
    address: 'Magneto Mall, Raipur',
  },
  Bhilai: {
    name: 'Aquaplast IT Services',
    address: 'Bhilai, Supela',
  },
};

const company = {
  name: 'Aquaplast Groups',
  locations,    // <---- THIS
  estbYear: 2021,
  getCompanyDetails(){    // <---- THIS
    return ...
  }
};
```

## Optional Chaining (?.)

Optional chaining checks if value from the left exists.

```js
const company = {
  name: 'Company Groups',
  estbYear: 2021,
  location: {
    Raipur: {
      name: 'ABC',
      address: 'abc',
    },
    Bhilai: {
      name: 'XYZ',
      address: 'xyz',
    },
  },
  callMe() {
    return 'Hello from Company';
  },
};

console.log(company.location.Bilaspur); // undefined

// we got error if we call on something which is undefined
//console.log(company.location.Bilaspur.name); // Uncaught TypeError.

// To solve this issue use if stmt.
if (company.location.Bilaspur) {
  console.log(company.location.Bilaspur.name);
}

// Alternative use optional chaining
// if Bilaspur location is present then only name variable is read.
console.log(company.location.Bilaspur?.name); // undefined
console.log(company.location?.Bilaspur?.name); // we can do this also

// works for methods also
console.log(company.callMeee?.()); // undefined
console.log(company.callMe?.()); // Hello from Company
```

## Looping through objects

```js
const company = {
  name: 'Company Groups',
  estbYear: 2021,
  location: {
    Raipur: {
      name: 'ABC',
      address: 'abc',
    },
    Bhilai: {
      name: 'XYZ',
      address: 'xyz',
    },
  },
};

// Object.keys
// Returns all the keys of the object
const keys = Object.keys(company.location); // ['Raipur', 'Bhilai']

// Object.values
// Returns all the values of the object
const values = Object.values(company.location);
// 0: {name: 'ABC', address: 'abc'}
// 1: {name: 'XYZ', address: 'xyz'}

// Object.entries
// Returns all the entries of the object
const entries = Object.entries(company.location);
// 0: (2) ['Raipur', {…}]
// 1: (2) ['Bhilai', {…}]

// looping
for (const [key, value] of entries) {
  console.log(key); // Raipur
  console.log(value); // {name: 'ABC', address: 'abc'}
}

for (const [key, { name, address }] of entries) {
  console.log(key); // Raipur
  console.log(name, address); // {name: 'ABC', address: 'abc'}
}
```

## Sets

Collection of unique values.

```js
const myset = new Set(['Pizza', 'Pizza', 'Burger', 'Chicken Lollypop']);
console.log(myset); // Set(3) {'Pizza', 'Burger', 'Chicken Lollypop'}

// Size of the set
console.log(myset.size); // 3

// Check a element is present in a set
console.log(myset.has('Pizza')); // true
console.log(myset.has('pizza')); // false

// we can also add(), delete(), clear() a set
```

## Maps

Creation, Deleting, Inserting of Maps

```js
const rest = new Map();

rest.set('name', 'KFC');
rest.set('location', 'Magneto Mall');

rest.set('menu', [
  'Chicken Peri Peri',
  'Hot and Crispy',
  'Chicken Rice',
  'Chicken Popcorn',
]);

// or we can set maps as below.
rest
  .set('categories', 'Non Vegeterian')
  .set('open', 11)
  .set('close', 10)
  .set(true, 'Yes we are open!.');

// Getting data
console.log(rest.get('name')); // KFC
console.log(rest.get(true)); // Yes we are open!.

// Check key is present or not
console.log(rest.has('name')); // true

// Delete maps using key
rest.delete('location');

// map has size and clear properties.

// Object can also be a key.
rest.set([1, 2], 'array');
console.log(rest.get([1, 2])); // undefined
// to make it work use below sol
const arr = [1, 2];
rest.set(arr, 'array');
console.log(rest.get(arr)); // array
```

Iterating through Maps

```js
const question = new Map([
  ['question', 'What is best programming for freelancing?'],
  [1, 'Java'],
  [2, 'Flutter'],
  [3, 'JavaScript'],
  [4, 'None'],
  ['correct', 3],
]);

// iterate
for (const [key, value] of question) {
  console.log(key, value);
}

// convert object to maps
new Map(Object.entries(objectName));
```


## Strings

```js
// Strings
const airline = 'Indigo';

console.log(airline[0]); // I
// length
console.log(airline.length); // 6
// index of
console.log(airline.indexOf('n')); // 1
// slicing an array
console.log(airline.slice(2)); // digo (2 is included)
console.log(airline.slice(2, 4)); // di (4 is excluded)

// Replace
const priceInDollar = '2,95$';
const priceInINR = priceInDollar.replace('$', 'INR').replace(',', '.');
console.log(priceInINR);

// Includes
const username = 'sandeep@gmail.com';
if (username.includes('sandeep')) {
  console.log('Name cannot be included in username');
}

// Splitting strings
const data = 'a-very-good-evening-to-everyone';
console.log(data.split('-'));
// ['a', 'very', 'good', 'evening', 'to', 'everyone']

// Joining
console.log(data.split('-').join(' '));
// a very good evening to everyone

// Padding
const firstName = 'Sandeep';
// first param -> total length.
console.log(firstName.padStart(10, '+').padEnd(40, '+'));
console.log('+++Sandeep++++++++++++++++++++++++++++++'.length);

// Example credit card masking - 16 digits to show last 4 digits
const cardNo = '1234567891234567';
const last4Digits = cardNo.slice(-4);
console.log(last4Digits.padStart(16, '#'));

// Repeat
const name = 'Cherry';
console.log(name.repeat(5));
```


