
## Default Parameters

```js
const createBooking = function (flightNo, numOfPassengers = 1, price = 5000) {};
```

## Pass by Value

**In JS there is no pass by reference feature. we can pass reference to function.**

```js
const flight = 'Vis123';
const sandeep = {
  firstName: 'Sandeep',
  lastName: 'Dewangan',
  DOB: '13-12-1990',
};

const checkIn = function (flightName, passenger) {
  flightName = 'Indi123';
  passenger.firstName = 'Sandeep Kumar';
};

checkIn(flight, sandeep);
// Parameter passed by Value, (Primitive Types)
console.log(flight); // Vis123
// Parameter passed by value (Object Types)
console.log(sandeep); // firstName: 'Sandeep Kumar'
```

## First Class Functions

JavaScript treats functions as first class citizens. This means function are just a simple values.

Example

```js
function incr(a){
	return a++;
}
```

## Hight Order Functions

A function which receives another function as an argument and that returns a new function or Both.

Example

```js
// addEventListener is higher order function
addEventListener('click', greet); 

// count() is higher order function
function count(){
	let count = 0;
		return function(){
			count++;
		}
}
```

Higher Order Function - function which receives another function as an argument

```js
const upperFirstWord = function (str) {
  const [firstWord, ...others] = str.split(' ');
  return [firstWord.toUpperCase(), ...others].join(' ');
};
// Higher order function
const transformer = function (str, fn) {
  // Original String: Javascript is best of all.
  console.log(`Original String: ${str}`);
  // Transformed String: JAVASCRIPT is best of all.
  console.log(`Transformed String: ${fn(str)}`);
  // Name of called function: upperFirstWord
  console.log(`Name of called function: ${fn.name}`);
};

console.log(transformer('Javascript is best of all.', upperFirstWord));
```

Higher Order Function - Function returning function

```js
const greet = function (greet) {
  return function (name) {
    console.log(`${greet} ${name}, howz you!`);
  };
};

const greetNamaskar = greet('Namaskar');
greetNamaskar('Darsh'); // Namaskar Darsh, howz you!

// alternatively
greet('Namaste')('Sandeep'); // Namaste Sandeep, howz you!

// using arrow function
const greetings = (g) => (n) => console.log(`${g} ${n}, howz you!`);
greetings('Swadika')('Chandu'); // Swadika Chandu, howz you!
```

## Call Method

**Manually manipulating the this keyword using call().**

```js
const indigo = {
  flightName: 'Indigo',
  flightCode: 'IN',
  bookings: [],
  book(flightNumber, passengerName) {
    console.log(
      `Thanks ${passengerName}, for booking on ${this.flightName}, ${this.flightCode}, ${flightNumber}`
    );
    this.bookings.push(
      `Thanks ${passengerName}, for booking on ${this.flightName}, ${this.flightCode}, ${flightNumber}`
    );
  },
};

const indigoPassenger1 = indigo.book('101', 'Sandeep Dewangan');
const indigoPassenger2 = indigo.book('101', 'Darsh Dewangan');
console.log(indigo.bookings);

// Suppose i want to have same book() function for another airline.

const vistara = {
  flightName: 'Vistara',
  flightCode: 'VIS',
  bookings: [],
};

// i want book function to vistara flight also. Copy and pasting the book method is not
// considered as a good practice.
// hence we can use call()

indigo.book.call(vistara, '102', 'Sandeep');
// call indigo book method for...vistara object
// here the this keyword is set for vistara not for indigo.
```

## Bind Method

```js
const indigo = {
  flightName: 'Indigo',
  flightCode: 'IN',
  bookings: [],
  book(flightNumber, passengerName) {
    console.log(
      `Thanks ${passengerName}, for booking on ${this.flightName}, ${this.flightCode}, ${flightNumber}`
    );
    this.bookings.push(
      `Thanks ${passengerName}, for booking on ${this.flightName}, ${this.flightCode}, ${flightNumber}`
    );
  },
};

const indigoPassenger1 = indigo.book('101', 'Sandeep Dewangan');
const indigoPassenger2 = indigo.book('101', 'Darsh Dewangan');
console.log(indigo.bookings);

const vistara = {
  flightName: 'Vistara',
  flightCode: 'VIS',
  bookings: [],
};

// Case I
const bookIndigoFlight = indigo.book.bind(indigo); // this points to indigo
const bookVistaraFlight = indigo.book.bind(vistara); // this points to vistara
bookIndigoFlight('102', 'ABc');
bookVistaraFlight('102', 'AXXX');

// Case II
const bookIndigoFlight101 = indigo.book.bind(indigo, '101'); // first parameter is binded
const bookVistaraFlight101 = indigo.book.bind(vistara, '101');
bookIndigoFlight101('Khushbu'); // now just pass the second param.
bookVistaraFlight101('Indu');
```

### Bind() -> `this` keyword working with Event Listener

```js
const indigo = {
  flightName: 'Indigo',
  flightCode: 'IN',
  bookings: [],
  book(flightNumber, passengerName) {
    console.log(
      `Thanks ${passengerName}, for booking on ${this.flightName}, ${this.flightCode}, ${flightNumber}`
    );
    this.bookings.push(
      `Thanks ${passengerName}, for booking on ${this.flightName}, ${this.flightCode}, ${flightNumber}`
    );
  },
};

const vistara = {
  flightName: 'Vistara',
  flightCode: 'VIS',
  bookings: [],
};

// ----- PROBLEM -------
// for event listeners, the this keyword is the name of the
// tag from which the event listener is called.
indigo.planes = 100;
indigo.buyPlanes = function () {
  console.log(this); // <input type="submit" value="Buy a flight" class="buy">
  this.planes++;
  console.log(this.planes); // NaN
};

// it will point to <input>......
document.querySelector('.buy').addEventListener('click', indigo.buyPlanes);

// ----- SOLUTION with Bind() -------
indigo.planes = 100;
indigo.buyPlanes = function () {
  console.log(this); // {flightName: 'Indigo', flightCode: 'IN', bookings: Array(0), planes: 100, book: ƒ, …}
  this.planes++;
  console.log(this.planes); // 101
};

// now it will point to indigo object.
document
  .querySelector('.buy')
  .addEventListener('click', indigo.buyPlanes.bind(indigo));
```

## Immediately Invoked Function Expressions

Executed only once.

```js
// Normal function
(function () {
  console.log('This function called once...');
})();

// Arrow function
(() => console.log('This function ALSO called once...'))();
```

## Closures

A **closure** is the combination of a function bundled together (enclosed) with references to its surrounding state

We can't make closures manually.

```js
const secureBooking = function () {
  let passengerCount = 0;

  return function () {
    console.log(++passengerCount);
  };
};

const book = secureBooking();
book();
book();
book();

// Check through internal properties
console.dir(book);
```




