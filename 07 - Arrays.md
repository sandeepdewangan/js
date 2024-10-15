## Simple Array Methods

```js
// Slice
let arr = ['a', 'b', 'c', 'd', 'e'];
console.log(arr.slice(2)); // ['c', 'd', 'e']
console.log(arr.slice(2, 4)); // ['c', 'd']

// Splice - spliced elements are removed from the orig arrary.
console.log(arr.splice(2)); // ['c', 'd', 'e']
console.log(arr); // ['a', 'b']

// Reverse - mutate the original array
console.log(arr); // ['a', 'b']
console.log(arr.reverse()); // ['b', 'a']
console.log(arr); // ['b', 'a']

// Joins array
const arrJoin = [1, 2, 3, 4, 5];
console.log(arrJoin.join('*')); // 1*2*3*4*5

// At
// Get the last value of an array - traditional ways
console.log(arrJoin[arrJoin.length - 1]); // 5
console.log(arrJoin.slice(-1)[0]); // 5

// new way using at, we can use negative indexing
console.log(arrJoin.at(-1)); // 5
```

## Looping through arrays using `forEach`

```js
const arr = [1, 3, 4, 5, 6, -1, 3];

arr.forEach(function (element, index, array) {
  // First loop
  // element: 1
  // index: 0
  // array: [1, 3, 4, 5, 6, -1, 3]
});
```

==Note:== 
1. We cannot use `break` or `continue` method using forEach.
2. We can use `forEach` for sets and maps.

## Some Array Methods
## Map, Filter, Reduce

1. Map takes an array process it and returns a new array.
2. Filter array based on some conditions and returns an new  array.
3. Reduce array based on reducing an array to a single value.

```js
// map Example
const tx = [200, 300, 400, 500, -200, -300];
const inrToDollar = 84.0;
const transactionsUSD = tx.map((t) => t * inrToDollar);
// map returns a new / transformed array
console.log(transactionsUSD); // [16800, 25200, 33600, 42000, -16800, -25200]

// filter example
const deposit = tx.filter((t) => t > 0);
const withdrawl = tx.filter((t) => t < 0);
console.log(deposit); // [200, 300, 400, 500]
console.log(withdrawl); // [-200, -300]

// reduce example
// accumulator is the total values performed by expression.
// 0 -> start value of accumulator.
const balance = tx.reduce((accumulator, current) => accumulator + current, 0);
console.log(balance);
```

==Note:== **Importance of map, filter and reduce method is that we can chain them together to produce output.**

## find

1. Used to find element in array based on condition.
2. Returns the first element of the array which satisfy the condition.

### find()

```js
const tx = [500, 400, 200, 600];
const txGreaterThan500 = tx.find((t) => t > 500);
console.log(txGreaterThan500); // 600
```

### findIndex()

```js
// findIndex
const tx = [500, 400, 200, 600];
const indexTxGreaterThan500 = tx.findIndex((t) => t > 500);
console.log(indexTxGreaterThan500); // 3
```

## Some and Every

```js
// some - returns true if atleast one of the ele passes the tests.
const tx = [500, 400, 200, 600, -200];
const anyWidhdrawalExists = tx.some((t) => t < 0);
console.log(anyWidhdrawalExists); // true

// every - returns true if all the ele passes the tests.
const isAllDeposits = tx.every((t) => t > 0);
console.log(isAllDeposits); // false
```

## Flat and flatMap

1. Flattern the nested array.
2. only goes one level deep by default
3. to modify the depth, pass the number of depth..

```js
const arr = [2, 3, [4, 5], [4, 6], [[2, 3], 3, 4]];
console.log(arr);
console.log(arr.flat(2)); // go 2 level deep.
```

`flatMap()` -> maps and then flatten the input.

## Sort

```js
const names = ['Sandeep', 'Khushbu', 'Darsh'];
console.log(names.sort()); // ['Darsh', 'Khushbu', 'Sandeep'] // mutable

// to sort numbers
const num = [200, 300, 100, -400];
num.sort((a, b) => {
  if (a > b) return 1; // SWITCH ORDER
  if (a < b) return -1; // KEEP ORDER
});

// OR simple use math trick
num.sort((a, b) => a - b);

console.log(num); // [-400, 100, 200, 300]
```

## Arrays creation and filling

```js
// create an array of length 7
const arr = new Array(7); // empty array
// fill the empty array
arr.fill(5); // fills all the array with number 5
arr.fill(1, 0, 5); // will fill the array with number 1 from index 0 to 5.
console.log(arr); // [1, 1, 1, 1, 1, 5, 5]

// from method
const arr2 = Array.from({ length: 7 }, () => 1); // fills the array with 7
console.log(arr2); // [1, 1, 1, 1, 1, 1, 1]

const arr3 = Array.from({ length: 7 }, (current, index) => index + 1);
console.log(arr3); // [1, 2, 3, 4, 5, 6, 7]
```
