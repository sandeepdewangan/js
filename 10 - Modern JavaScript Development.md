## Modules

Reusable piece of code that encapsulates implementation details.

Difference between ES6 Module vs Script.


|                     | ES6 Module              | Script      |
| ------------------- | ----------------------- | ----------- |
| Top-level variables | Scoped to module        | Global      |
| Default mode        | Strict mode             | Sloppy mode |
| Top level `this`    | undefined               | window      |
| import and exports  | YES                     | NO          |
| HTML linking        | `<script type="module"` | `<script>`  |
| File downloading    | Asyn                    | Sync        |

## Named Import and Exports

```html
<script type="module" defer src="script.js"></script>
```

`shopping_cart.js`

```js
const cart = [];

// Named Export
export const addToCart = function (product, quantity) {
  cart.push({ product, quantity });
  console.log(`${product} with ${quantity} is added to the cart!`);
};

// exporting multiple variables
const totalPrice = 235;
const totalQty = 7;

export { totalPrice, totalQty as qty };
```

`script.js`

```js
// addToCart is named export hence, requires exact match of name.
import { addToCart, totalPrice as price, qty } from './shopping_cart.js';

addToCart('Headphone', 2);
console.log(price, qty);

// importing everything
import * as ShoppingCart from './shopping_cart.js';
ShoppingCart.addToCart('Mouse', 10);
```

## Default Exports

Used when we want to export only one thing per module.

`shopping_cart.js`

```js
const cart = [];

export default function (product, quantity) {
  cart.push({ product, quantity });
  console.log(`${product} with ${quantity} is added to the cart!`);
}
```

`script.js`

```js
import add from './shopping_cart.js';
add('Wifi Router', 2);
```

## Top Level `await`

**Top Level await will block whole module.**

```js
console.log('Fetching Data');
const res = await fetch('https://jsonplaceholder.typicode.com/posts');
const data = res.json();
```

## Node Package Manager 

**Initialization**

`npm init`

**Install Library**

`npm install leaflet`

**Install Packages Existing JSON file**

`npm install`

## Bundling with Parcel

`npm install parcel --save-dev`

`npx parcel index.html`

Parcel will bundle up all the html and JS code. 

## JSON - Running Scripts 

```json
"scripts": {
    "start": "parcel index.html",
    "build": "parcel build index.html"
  },
```

Build and Start Server
`npm run start`

Final Build
`npm run build`

