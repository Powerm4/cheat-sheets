# JS Snippets

### Table of Contents

1. [Generate a random number in a given range](#How-to-generate-a-random-number-in-a-given-range)
2. [Find the difference between two arrays](#How-to-find-the-difference-between-two-arrays)
3. [Convert truthy/falsy to boolean(true/false)](#Convert-truthy-falsy-to-boolean)
4. [Repeat a string](#Repeat-a-string)
5. [Check how long an operation takes](#Check-how-long-an-operation-takes)
6. [Two ways to remove an item in a specific in an array](#Two-ways-to-remove-an-item-in-a-specific-in-an-array)
7. [Did you know you can flat an array?](#Did-you-know-you-can-flat-an-array)
8. [Get unique values in an array](#Get-unique-values-in-an-array)
9. [Copy Text to Clipboard](#Copy-Text-to-Clipboard)
10. [Nested Destructuring](#Nested-Destructuring)
11. [URLSearchParams](#URLSearchParams)
12. [Count elements in an array](#Count-elements-in-an-array)
13. [Aliases with JavaScript Destructuring](#Aliases-with-JavaScript-Destructuring)
14. [The Object.is() method determines whether two values are the same value](#the-objectis-method-determines-whether-two-values-are-the-same-value)
15. [Freeze an object](#Freeze-an-object)
16. [Printing Object keys and values](#Printing-Object-keys-and-values)
17. [Capture the right click event](#Capture-the-right-click-event)
18. [In HTML5, you can tell the browser when to run your JavaScript code](#in-html5-you-can-tell-the-browser-when-to-run-your-javascript-code)
19. [Nullish coalescing operator](#Nullish-coalescing-operator)
20. [Optional chaining](#Optional-chaining)
21. [globalThis](#globalThis)
22. [The second argument of JSON.stringify lets you cherry-pick 🍒 keys to serialize.](#the-second-argument-of-jsonstringify-lets-you-cherry-pick--keys-to-serialize)
23. [Fire an event listener only once.](#Fire-an-event-listener-only-once)
24. [Vanilla JS toggle](#Vanilla-JS-toggle)
25. [Check if a string is a valid JSON](#Check-if-a-string-is-a-valid-JSON)
26. [getBoundingClientRect](#getBoundingClientRect)
27. [Check if a node is in the viewport](#Check-if-a-node-is-in-the-viewport)
28. [Notify when element size is changed](#Notify-when-element-size-is-changed)
29. [Date Formatter](#Date-Formatter)
30. [Reversing string](#Reversing-string)
31. [JavaScript Performance API](#JavaScript-Performance-API)
32. [Array](#Array)
33. [Intl Formatter Docs](#Intl-Formatter-Docs)
34. [Console Logging Methods](#Console-Logging-Methods)
35. [Other](#Other)

<img src="./assets/js/es6_cheatsheet.jpg" alt="cheatsheet" width="300px" align="right"/>
<p align="left">
  <img src="./assets/js/array.jpg" alt="array" width="300px"/>
  <img src="./assets/js/hoisting in js.png" alt="hoisting" width="300px"/>
  <img src="./assets/js/js array.jpeg" alt="array" width="300px"/>
  <img src="./assets/js/asyncjs.gif" alt="asyncjs" width="300px"/>
  <img src="./assets/js/var-let-const.jpg" alt="var-let-const" width="300px"/>
</p>

### How to generate a random number in a given range

```javascript
// Returns a random number(float) between min (inclusive) and max (exclusive)

const getRandomNumber = (min, max) => Math.random() * (max - min) + min;

getRandomNumber(2, 10);

// Returns a random number(int) between min (inclusive) and max (inclusive)

const getRandomNumberInclusive = (min, max) => {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min + 1)) + min;
};

getRandomNumberInclusive(2, 10);
```

**[⬆ Back to Top](#table-of-contents)**

### How to find the difference between two arrays

```javascript
const firstArr = [5, 2, 1];
const secondArr = [1, 2, 3, 4, 5];

const diff = [
  ...secondArr.filter((x) => !firstArr.includes(x)),
  ...firstArr.filter((x) => !secondArr.includes(x)),
];
console.log("diff", diff); //[3,4]

function arrayDiff(a, b) {
  return [
    ...a.filter((x) => b.indexOf(x) === -1),
    ...b.filter((x) => a.indexOf(x) === -1),
  ];
}
console.log("arrayDiff", arrayDiff(firstArr, secondArr)); //[3,4]

const difference = (a, b) => {
  const setA = new Set(a);
  const setB = new Set(b);

  return [...a.filter((x) => !setB.has(x)), ...b.filter((x) => !setA.has(x))];
};

difference(firstArr, secondArr); //[3,4]
console.log("difference", difference(firstArr, secondArr));
```

### Convert truthy falsy to boolean

```javascript ✔
const myVar = null;
const mySecondVar = 1;

console.log(Boolean(myVar)); // false
console.log(!!myVar); // false

console.log(Boolean(mySecondVar)); // true
console.log(!!mySecondVar); // true
```

### Repeat a string

```javascript
let aliens = "";

for (let i = 0; i < 6; i++) {
  aliens += "👽";
}
//👽👽👽👽👽👽

Array(6).join("👽");
//👽👽👽👽👽👽

"👽".repeat(6);
//👽👽👽👽👽👽
```

**[⬆ Back to Top](#table-of-contents)**

### Check how long an operation takes

```javascript
//The performance.now() method returns a DOMHighResTimeStamp, measured in milliseconds.
//performance.now() is relative to page load and more precise in orders of magnitude.
//Use cases include benchmarking and other cases where a high-resolution time is required
//such as media (gaming, audio, video, //etc.)

var startTime = performance.now();
doSomething();
const endTime = performance.now();
console.log("this doSomething took " + (endTime - startTime) + " milliseconds.");
```

**[⬆ Back to Top](#table-of-contents)**

### Two ways to remove an item in a specific in an array

```javascript
//Mutating way ✔
const muatatedArray = ["a", "b", "c", "d", "e"];
muatatedArray.splice(2, 1);
console.log(muatatedArray); //['a','b','d','e']

//Non-mutating way ✔
const nonMuatatedArray = ["a", "b", "c", "d", "e"];
const newArray = nonMuatatedArray.filter((item, index) => !(index === 2));
console.log(newArray); //['a','b','d','e']
```

**[⬆ Back to Top](#table-of-contents)**

### Did you know you can flat an array ✔

```javascript
const myArray = [2, 3, [4, 5], [7, 7, [8, 9, [1, 1]]]];

myArray.flat(); // [2, 3, 4, 5 ,7,7, [8, 9, [1, 1]]]

myArray.flat(1); // [2, 3, 4, 5 ,7,7, [8, 9, [1, 1]]]

myArray.flat(2); // [2, 3, 4, 5 ,7,7, 8, 9, [1, 1]]

//if you dont know the depth of the array you can use infinity
myArray.flat(infinity); // [2, 3, 4, 5 ,7,7, 8, 9, 1, 1];
```

**[⬆ Back to Top](#table-of-contents)**

### Get unique values in an array

```javascript
const numbers = [1, 1, 3, 2, 5, 3, 4, 7, 7, 7, 8];

//Ex1
const unieqNumbers = numbers.filter((v, i, a) => {
  console.log(v);
  console.log(i);
  console.log(a);
  a.indexOf(v) === i;
});
console.log(unieqNumbers); //[1,3,2,5,4,7,8]

//Ex2
const unieqNumbers2 = Array.from(new Set(numbers));
console.log(unieqNumbers2); //[1,3,2,5,4,7,8]

//Ex3
const unieqNumbers3 = [...new Set(numbers)];
console.log(unieqNumbers3); //[1,3,2,5,4,7,8]

//EX4 lodash
const unieqNumbers4 = _.uniq(numbers);
console.log(unieqNumbers4); //[1,3,2,5,4,7,8]
```

**[⬆ Back to Top](#table-of-contents)**

### Copy Text to Clipboard

```javascript
function copyToClipboard() {
  const copyText = document.getElementById("myInput");
  copyText.select();
  document.execCommand("copy");
}
//new API
function copyToClipboard() {
  navigator.clipboard.writeText(document.querySelector("#myInput").value);
}
```

**[⬆ Back to Top](#table-of-contents)**

### Nested Destructuring ✔

```javascript
const user = {
  id: 459,
  name: "JS snippets",
  age: 29,
  education: {
    degree: "Masters",
  },
};

const {
  education: { degree },
} = user;
console.log(degree); //Masters
```

**[⬆ Back to Top](#table-of-contents)**

### URLSearchParams

```javascript
//The URLSearchParams interface defines utility methods to work with the query string of a URL.

const urlParams = new URLSearchParams("?post=1234&action=edit");

console.log(urlParams.has("post")); // true
console.log(urlParams.get("action")); // "edit"
console.log(urlParams.getAll("action")); // ["edit"]
console.log(urlParams.toString()); // "?post=1234&action=edit"
console.log(urlParams.append("active", "1")); // "?post=1234&action=edit&active=1"
```

**[⬆ Back to Top](#table-of-contents)**

### Count elements in an array

```javascript
const myFruits = ["Apple", "Orange", "Mango", "Banana", "Apple", "Apple", "Mango"];

//first option
const countMyFruits = myFruits.reduce((countFruits, fruit) => {
  countFruits[fruit] = (countFruits[fruit] || 0) + 1;
  return countFruits;
}, {});
console.log(countMyFruits);
// { Apple:3, Banana:1, Mango:2, Orange:1 }

//seconf option ✔
const fruitsCounter = {};

for (const fruit of myFruits) {
  fruitsCounter[fruit] = fruitsCounter[fruit] ? fruitsCounter[fruit] + 1 : 1;
}

console.log(fruitsCounter);
// { Apple:3, Banana:1, Mango:2, Orange:1 }
```

**[⬆ Back to Top](#table-of-contents)**

### Aliases with JavaScript Destructuring ✔

```javascript
//There are cases where you want the destructured variable to have a different name than the property name

const obj = {
  name: "JSsnippets",
};

// Grabs obj.name as { pageName }
const { name: pageName } = obj;

//log our alias
console.log(pageName); // JSsnippets
```

**[⬆ Back to Top](#table-of-contents)**

### The Object.is() method determines whether two values are the same value

```javascript
Object.is("foo", "foo"); // true

Object.is(null, null); // true

Object.is(Nan, Nan); // true 😱

const foo = { a: 1 };
const bar = { a: 1 };
Object.is(foo, foo); // true
Object.is(foo, bar); // false
```

**[⬆ Back to Top](#table-of-contents)**

### Freeze an object ✔

```javascript
const obj = {
  name: "JSsnippets",
  age: 29,
  address: {
    street: "JS",
  },
};

const frozenObject = Object.freeze(obj);

frozenObject.name = "weLoveJS"; // Uncaught TypeError

//Although, we still can change a property’s value if it’s an object:

frozenObject.address.street = "React"; // no error, new value is set

delete frozenObject.name; // Cannot delete property 'name' of #<Object>

//We can check if an object is frozen by using
Object.isFrozen(obj); //true
```

**[⬆ Back to Top](#table-of-contents)**

### Printing Object keys and values

```javascript
const obj = {
  name: "JSsnippets",
  age: 29,
};

//Object.entries() method is used to return an array consisting of enumerable property
//[key, value] pairs of the object which are passed as the parameter.

for (let [key, value] of Object.entries(obj)) {
  console.log(`${key}: ${value}`);
}

//expected output:
// "name: Jssnippets"
// "age: 29"
// order is not guaranteed
```

**[⬆ Back to Top](#table-of-contents)**

### Capture the right click event

```javascript
window.oncontextmenu = () => {
  console.log("right click");
  return false; // cancel default menu
};
//or

window.addEventListener(
  "contextmenu",
  () => {
    console.log("right click");
    return false; // cancel default menu
  },
  false,
);
```

**[⬆ Back to Top](#table-of-contents)**

### In HTML5, you can tell the browser when to run your JavaScript code

```javascript

//Without async or defer, browser will run your script immediately, before rendering the elements that's below your script tag.
<script src="myscript.js"></script>

//With async (asynchronous), browser will continue to load the HTML page and render it while the browser load and execute the script at the same time.
//Async is more useful when you really don't care when the script loads and nothing else that is user dependent depends upon that script loading.(for scripts likes Google analytics)
<script async src="myscript.js"></script>

//With defer, browser will run your script when the page finished parsing. (not necessary finishing downloading all image files.
<script defer src="myscript.js"></script>
```

**[⬆ Back to Top](#table-of-contents)**

### Nullish coalescing operator

```javascript
// an equality check against nullary values (e.g. null or undefined). Whenever the expression to the left of the ?? operator evaluates to either //undefined or null, the value defined to the right will be returned.

const foo = undefined ?? "default string";
console.log(foo);
// expected output: "default string"

const age = 0 ?? 30;
console.log(age);
// expected output: "0"
```

**[⬆ Back to Top](#table-of-contents)**

### Optional chaining

```javascript
const car = {};
const carColor = car.name.color;
console.log(carColor);
// error- "Uncaught TypeError: Cannot read property 'carColor' of undefined

//In JavaScript, you can first check if an object exists, and then try to get one of its properties, like this:
const carColor = car && car.name && car.name.color;
console.log(carColor);
//undefined- no error

//Now this new optional chaining operator will let us be even more fancy:

const newCarColor = car?.name?.color;
console.log(newCarColor);
//undefined- no error

//You can use this syntax today using @babel/plugin-proposal-optional-chaining
```

**[⬆ Back to Top](#table-of-contents)**

### globalThis

```javascript
Accessing the global property in JavaScript has always posed some difficulty. This is because
different platforms have different ways to access it.

Client-side JavaScript uses window or self

Node.js uses global

Web workers use self

The globalThis property provides a standard way of accessing the global 'this' value across environments. you can access the global object in a consistent manner without having to know which environment the code is being run in.

console.log(globalThis) //get the global this depends on your environment

```

**[⬆ Back to Top](#table-of-contents)**

# The second argument of JSON.stringify lets you cherry-pick 🍒 keys to serialize.

```javascript
const user = {
  id: 459,
  name: "JS snippets",
  age: 29,
  education: {
    degree: "Masters",
  },
};

JSON.stringify(user, [name, age], 2);

/*
returns

{
  "name": "JS snippets",
  "age": 29
}


*/
```

**[⬆ Back to Top](#table-of-contents)**

### Fire an event listener only once

```javascript
const el = document.getElementById("btn");

function myClickHandler() {
  console.log("this click will only fire once");
}

el.addEventListener("click", myClickHandler, {
  once: true,
});
```

**[⬆ Back to Top](#table-of-contents)**

### Vanilla JS toggle

```javascript
const span = document.querySelector("span");
let classes = span.classList;

span.addEventListener("click", function () {
  let result = classes.toggle("active");

  if (result) {
    console.log("active class was added");
  } else {
    console.log("active class was removed");
  }
});
```

**[⬆ Back to Top](#table-of-contents)**

### Check if a string is a valid JSON

```javascript
function isJson(str) {
  try {
    JSON.parse(str);
  } catch (e) {
    //the json is  not ok
    return false;
  }
  //the json is ok
  return true;
}
```

**[⬆ Back to Top](#table-of-contents)**

### getBoundingClientRect

```javascript
//getBoundingClientRect provides you with important pieces of data about an
//HTML element’s size and positioning.

const bodyBounderies = document.body.getBoundingClientRect();
// =>  {
//       top: Number,
//       left: Number,
//       right: Number,
//       bottom: Number,
//       x: Number,
//       y: Number,
//       width: Number,
//       height: Number,
//     }
```

**[⬆ Back to Top](#table-of-contents)**

### Check if a node is in the viewport

```javascript
const image = document.querySelector(".animate-me");

observer = new IntersectionObserver((entries) => {
  const [myImg] = entries;
  if (myImg.intersectionRatio > 0) {
    myImg.target.classList.add("fancy");
  } else {
    myImg.target.classList.remove("fancy");
  }
});

observer.observe(image);
```

**[⬆ Back to Top](#table-of-contents)**

### Notify when element size is changed

```javascript
const foo = document.getElementById("foo");

const observer = new ResizeObserver((entries) => {
  for (let entry of entries) {
    const cr = entry.contentRect;
    console.log = `Size: ${cr.width}px X ${cr.height}px`;
  }
});
observer.observe(foo);
```

**[⬆ Back to Top](#table-of-contents)**

### Date Formatter

```js
// Date Formatter
function formatDate(userDate) {
  // format from M/D/YYYY to YYYYMMDD
  const dateArr = userDate.split("/");
  const day = dateArr[1].length === 2 ? dateArr[1] : "0" + dateArr[1];
  const month = dateArr[0].length === 2 ? dateArr[0] : "0" + dateArr[0];
  const year = dateArr[2];
  return year + month + day;
}
console.log(formatDate("1/31/2014"));

// or

function formatDate(userDate) {
  // format from M/D/YYYY to YYYYMMDD
  console.log("Parse", Date.parse(userDate)); //Parse number
  console.log("new", typeof new Date(userDate)); //new object

  var x = new Date(userDate);
  var y = x.getFullYear().toString();
  var m = (x.getMonth() + 1).toString();
  var d = x.getDate().toString();
  d.length == 1 && (d = "0" + d);
  m.length == 1 && (m = "0" + m);
  var yyyymmdd = y + m + d;
  return yyyymmdd;
}

console.log(formatDate("12/31/2014"));
```

**[⬆ Back to Top](#table-of-contents)**

### Reversing string

```js
// Simply reversing the string wont give the solution.
// Get each word.
// Reverse It
// Again rejoin

var str = "This is fun, hopefully.";
// console.log(str.split("").reverse().join("").split(" ").reverse().join(" "));

console.log(
  str
    .split(" ")
    .map((el) => el.split("").reverse().join(""))
    .join(" "),
);

// with regex
String.prototype.replaceAll = function (find, replace) {
  var target = this;
  return target.replace(new RegExp(find, "g"), replace);
};
str = "ghktestlllltest-sdds";
str = str.replaceAll("test", "");
console.log(str);

// str = "ghktestlllltest-sdds"
// str = str.replace(/test/g, '');
// alert(str)
```

### JavaScript Performance API

    The Performance API is designed to help developers locate and solve performance problems and optimize page loading speed and user experience. It can be used in the following scenarios:
    - Web Page Performance Monitoring
    - Performance Optimization
    - User Experience Analysis
    - Performance Benchmarking

- Get Page Load Time:
  ```js
  const loadTime =
    window.performance.timing.loadEventEnd - window.performance.timing.navigationStart;
  console.log(`Page load time: ${loadTime}ms`);
  ```
- Measuring Resource Load Time:

  ```js
  const resourceTiming = window.performance.getEntriesByType("resource");
  resourceTiming.forEach((resource) => {
    console.log(`${resource.name} load time: ${resource.duration}ms`);
  });
  ```

- Monitor User Interaction Latency:
  ```js
  const interactionStart = Date.now();
  document.addEventListener("click", () => {
    const interactionEnd = Date.now();
    const interactionDelay = interactionEnd - interactionStart;
    console.log(`User click delay:${interactionDelay}ms`);
  });
  ```
- Page Load Time Monitoring and Optimization:

  ```js
  // Monitoring page load time
  const loadTime =
    window.performance.timing.loadEventEnd - window.performance.timing.navigationStart;
  console.log(`Page load time: ${loadTime}ms`);

  // Monitor resource load time
  const resourceTiming = window.performance.getEntriesByType("resource");
  resourceTiming.forEach((resource) => {
    console.log(`${resource.name} load time: ${resource.duration}ms`);
  });
  ```

- Resource loading performance analysis:

  ```js
  // Monitor the load time of a critical resource
  const keyResources = [
    "https://example.com/css/style.css",
    "https://example.com/js/main.js",
  ];
  keyResources.forEach((resource) => {
    const resourceEntry = window.performance.getEntriesByName(resource)[0];
    console.log(`${resource} load time: ${resourceEntry.duration}ms`);
  });
  ```

- User interaction latency monitoring:

  ```js
  // Monitor user click latency
  const interactionStart = Date.now();
  document.addEventListener("click", () => {
    const interactionEnd = Date.now();
    const interactionDelay = interactionEnd - interactionStart;
    console.log(`User click delay: ${interactionDelay}ms`);
  });
  ```

- Page Animation Performance Monitoring:

  ```js
  // Monitoring animation performance
  function measureAnimationPerformance() {
    const animationStart = performance.now();
    // Execute animation operations
    requestAnimationFrame(() => {
      const animationEnd = performance.now();
      const animationDuration = animationEnd - animationStart;
      console.log(`Animation execution time: ${animationDuration}ms`);
    });
  }

  measureAnimationPerformance();
  ```

- :
  ```js
  const loadTime =
    window.performance.timing.loadEventEnd - window.performance.timing.navigationStart;
  console.log(`Page load time: ${loadTime}ms`);
  ```
  **[⬆ Back to Top](#table-of-contents)**

### Array

```js
// Last element
arr.at(-1);
// 2nd last element
arr.at(-2);
```

**[⬆ Back to Top](#table-of-contents)**

### [Intl Formatter Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)

- Date Time

  ```js
  const formatter = new Intl.DateTimeFormat("en-US");
  console.log(formatter.format(new Date()));
  ```

- Relative Time Format

  ```js
  const formatter = new Intl.RelativeTimeFormat(undefined, { numeric: "auto" });
  console.log(formatter.format(1, "day");
  ```

  **[⬆ Back to Top](#table-of-contents)**

- Number Format

  ```js
  const currencyFormatter = new Intl.NumberFormat(undefined, {
    currency: "USD",
    style: "currency",
  });
  const unitFormatter = new Intl.NumberFormat(undefined, {
    unit: "liter",
    style: "unit",
    unitDisplay: "long",
  });
  const numberFormatter = new Intl.NumberFormat(undefined, { notation: "compact" });
  const fractionFormatter = new Intl.NumberFormat(undefined, {
    maximumFractionDigits: 2,
    minimumFractionDigits: 1,
  });
  console.log(currencyFormatter.format(15412154));
  ```

  **[⬆ Back to Top](#table-of-contents)**

### Console Logging Methods

- To print array as a table

  ```js
  const users = [
    { name: "a", age: 25 },
    { name: "b", age: 26 },
  ];
  console.table(users);
  ```

- To print How much Time it take

  ```js
  console.time("Loop");
  for (let i = 0; i < 100000; i++) {
    //
  }
  console.timeEnd("Loop");
  ```

  **[⬆ Back to Top](#table-of-contents)**

### Other

- JS Built in uuid generator API

  ```js
  console.log(crypto.randomUUID());
  ```

- Get time difference between dates in hour

  ```js
  const today = new Date();
  const yesterday = new Date();
  yesterday.setDate(yesterday.getDate() - 1);
  const timeDiff = today.getTime() - yesterday.getTime();
  const diffInMs = Math.abs(timeDiff);
  const diffInMinutes = Math.floor(diffInMs / (1000 * 60 * 60));
  ```

  **[⬆ Back to Top](#table-of-contents)**
