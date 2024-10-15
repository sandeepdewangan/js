Pillars of OOP
1. Abstraction
2. Encapsulation
3. Inheritance
4. Polymorphism

==Note:==
1. JS don't have any classes which traditional OOP has.
2. 
## Constructor and `new` Operator

```js
new Person()
```

`new` keyword does the following:
1.  New {} is created.
2. function is called, this = {}
3. {} linked to prototype
4. function automatically return

```js
const Person = function (fname, lname, dob) {
  // instance properties
  this.firstName = fname;
  this.lastName = lname;
  this.DOB = dob;

  // instance methods
  // never do this, bez when we have thousands of objects
  // we will have thousands of this method copies.
  // we will use prototype inheritance.
  this.calAge = function () {
    console.log(2024 - this.DOB);
  };
};

const sandy = new Person('Sandeep', 'Dewangan', 1990);
console.log(sandy); // Person {firstName: 'Sandeep', lastName: 'Dewangan'}
sandy.calAge(); // 34

console.log(sandy instanceof Person); // true
```

## Prototypes

```js
const Person = function (fname, lname, dob) {
  // instance properties
  this.firstName = fname;
  this.lastName = lname;
  this.DOB = dob;
};

// declare object methods
Person.prototype.calAge = function () {
  console.log(2024 - this.DOB);
};

// check prototype properties
console.log(Person.prototype);
// {calAge: ƒ}
// constructor: ƒ (fname, lname, dob)

const sandy = new Person('Sandeep', 'Dewangan', 1990);
console.log(sandy); // Person {firstName: 'Sandeep', lastName: 'Dewangan'}
console.log(sandy instanceof Person); // true
sandy.calAge(); // 34

console.log(sandy.__proto__);
// calAge: ƒ();
// constructor: ƒ(fname, lname, dob);
console.log(Person.prototype.isPrototypeOf(sandy)); // true
```

## ES6 Classes

1. Classes are not hoisted.
2. Classes are first class citizens.
3. Classes are executed in strict mode.

```js
class PersonCl {
  constructor(firstName, lastName, DOB) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.DOB = DOB;
  }
  calAge() {
    console.log(2024 - this.DOB);
  }
}

const sandy = new PersonCl('Sandeep', 'Dewangan', 1990);
sandy.calAge(); // 34
```

## Getters and Setters

* Getter can be used as a property.
* Setter can also be set as if setting a property.

```js
const account = {
  onwer: 'Sandeep',
  transactions: [100, 200, 300],

  get latest() {
    return this.transactions.slice(-1).pop();
  },
  set latest(tx) {
    this.transactions.push(tx);
  },
};

console.log(account.latest);
account.latest = 50;
console.log(account.transactions); // [100, 200, 300, 50]
```

Setting a property which already existed

```js
class PersonCl {
  constructor(fullName, DOB) {
    this.fullName = fullName;
    this.DOB = DOB;
  }

  // getter
  get fullName() {
    return this._fullName;
  }

  // setter
  set fullName(name) {
    this._fullName = name;
  }
}

const sandy = new PersonCl('Sandeep Dewangan', 1990);
console.log(sandy.fullName); // Sandeep Dewangan
```

## Static Methods

```js
static hey = function () {
    console.log('Hey from static...');
  };
PersonCl.hey(); //  Hey from static...
```

## Object create

```js
const PersonProto = {
  calAge() {
    console.log(2024 - this.DOB);
  },
};

const sandy = Object.create(PersonProto);
console.log(sandy);

// {}[[Prototype]]: Object
// calAge: ƒ calAge()
// [[Prototype]]: Object

sandy.calAge(); // NaN

// adding methods to prototype
sandy.DOB = 1990;
sandy.calAge(); // 34
```

## Inheritance

Traditional JS

```js
// Class
const Person = function (fName, DOB) {
  this.fName = fName;
  this.DOB = DOB;
};
// Methods
Person.prototype.calAge = function () {
  console.log(2024 - this.DOB);
};

// Class
const Student = function (fName, DOB, course) {
  // Inheritance
  Person.call(this, fName, DOB, course);
  this.course = course;
};
// Create Object
Student.prototype = Object.create(Person.prototype);

const sandy = new Student('Sandeep', 1990, 'CSE');
sandy.calAge(); // 34
console.log(sandy);
// DOB: 1990;
// course: 'CSE';
// fName: 'Sandeep';
```

Using ES6

```js
class PersonCl {
  constructor(fullName, DOB) {
    this.fullName = fullName;
    this.DOB = DOB;
  }

  calAge() {
    console.log(2024 - this.DOB);
  }
}

class StudentCl extends PersonCl {
  constructor(fullName, DOB, course) {
    super(fullName, DOB);
    this.course = course;
  }
}

const sandy = new StudentCl('Sandeep Dewangan', 1990, 'CSE');
sandy.calAge();
console.log(sandy);
```

## Encapsulation

```js
class Account {
  // Public fields - Instance. (without let or const)
  locale = navigator.language;

  // Private fields - Instance.
  #transactions = [];
  #pin;

  // constructor
  constructor(owner, pin) {
    this.owner = owner;
    this.#pin = pin;
  }

  // public methods
  getTransactions() {
    return this.#transactions;
  }

  // private methods
  #loadApproval() {
    return true;
  }
}

const acc = new Account('Sandeep', 1234);
console.log(acc.locale);
// console.log(acc.#transactions); // Private field
console.log(acc.getTransactions());
console.log(acc);
```

## Chainable Method

Use this  keyword to make method chainable.

```js
class Account {
  // Private fields - Instance.
  #transactions = [];

  deposit(amount) {
    this.#transactions.push(amount);
    return this;
  }

  withdraw(amount) {
    this.#transactions.push(-amount);
    return this;
  }
}

const acc = new Account('Sandeep', 1234);
acc.deposit(500).withdraw(200).deposit(100);
console.log(acc.getTransactions()); // [500, -200, 100]
```
