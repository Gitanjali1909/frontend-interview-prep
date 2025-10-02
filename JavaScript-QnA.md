# JavaScript Interview Q&A

---

## 1. What are `var`, `let`, and `const`?

**Answer:**  
- `var` → function-scoped, can be re-declared & updated.  
- `let` → block-scoped, can be updated but not re-declared.  
- `const` → block-scoped, cannot be updated or re-declared.

```
var a = 10;
let b = 20;
const c = 30;
```

**Visual:**
```
Scope
 ├─ Global
 │   ├─ var a
 │   ├─ let b
 │   └─ const c
 └─ Function/Block
```

---

## 2. What is hoisting?

**Answer:**  
* Variable and function declarations are moved to the top of their scope.  
* Initializations are **not hoisted**.

```
console.log(x); // undefined
var x = 5;

foo(); // works
function foo() { console.log("Hello"); }
```

**Visual:**
```
Compilation: var x; function foo() {}
Execution: x = 5; foo()
```

---

## 3. Explain closures.

**Answer:**  
* Function that **remembers its lexical scope** even after outer function finishes.

```
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  };
}
const counter = outer();
console.log(counter()); // 1
console.log(counter()); // 2
```

**Visual:**
```
outer() scope
 └─ inner() remembers count
```

---

## 4. Difference between `==` and `===`

**Answer:**  
- `==` → value equality (type coercion allowed)  
- `===` → strict equality (type + value)

```
5 == '5'  // true
5 === '5' // false
```

---

## 5. Difference between `null` and `undefined`

**Answer:**  
- `undefined` → variable declared, not assigned  
- `null` → explicitly “no value”

```
let a;
console.log(a); // undefined
let b = null;
console.log(b); // null
```

---

## 6. Explain `this` keyword

**Answer:**  
* Refers to the **current execution context**.

```
console.log(this); // window/global object

function foo() { console.log(this); }
foo(); // window (in browsers)

const obj = { foo };
obj.foo(); // obj
```

**Visual:**
```
Function call -> global
Method call   -> owning object
Arrow func    -> lexical this
```

---

## 7. What is the event loop?

**Answer:**  
* JS is single-threaded. Event loop handles async callbacks **without blocking** the main thread.

```
console.log("Start");
setTimeout(() => { console.log("Timeout"); }, 0);
console.log("End");
```

**Output:**
```
Start
End
Timeout
```

**Visual:**
```
Call Stack -> Web API -> Callback Queue -> Event Loop -> Stack
```

---

## 8. Event bubbling and capturing

**Answer:**  
- Bubbling → event moves child → parent → ancestor  
- Capturing → ancestor → parent → child  

```
child.addEventListener('click', e => console.log('Child clicked'), false);
```

**Visual:**
```
Capturing: Grandparent -> Parent -> Child
Bubbling: Child -> Parent -> Grandparent
```

---

## 9. Arrow functions vs regular functions

**Answer:**  
- Arrow → no own `this`, cannot be constructor, shorter syntax  
- Regular → dynamic `this`, usable as constructor  

```
const add = (a, b) => a + b;
```

---

## 10. Callback functions

**Answer:**  
* A function passed as argument to be called later.

```
function greet(name, callback) {
  console.log(`Hi ${name}`);
  callback();
}
greet('Alice', () => console.log('Callback executed'));
```

---

## 11. Promises

**Answer:**  
* Represent future completion of async operation.  
* States: pending → resolved/rejected.  

```
let p = new Promise((resolve) => resolve('Done'));
p.then(res => console.log(res));
```

---

## 12. Async/Await

**Answer:**  
* Syntax sugar for Promises. Writes async code like sync.

```
async function fetchData() {
  let res = await fetch('url');
  console.log(await res.json());
}
```

---

## 13. Synchronous vs Asynchronous

**Answer:**  
- Sync → blocks until done.  
- Async → non-blocking.  

```
console.log("A");
setTimeout(() => console.log("B"), 0);
console.log("C"); // A C B
```

---

## 14. JavaScript data types

**Answer:**  
- Primitive: string, number, boolean, null, undefined, symbol, bigint  
- Reference: objects, arrays, functions

---

## 15. Template literals

**Answer:**  
* Backticks with `${}` for interpolation.

```
let name = 'Alice';
console.log(`Hello ${name}`);
```

---

## 16. Destructuring

**Answer:**  
* Extract values from arrays/objects.

```
const [a, b] = ;
const {x, y} = {x: 10, y: 20};
```

---

## 17. Default parameters

**Answer:**  
* Functions can have default args.

```
function greet(name='Guest') { console.log(`Hi ${name}`); }
greet(); // Hi Guest
```

---

## 18. Spread/Rest operator

**Answer:**  
- Spread → expand values  
- Rest → collect into array  

```
const arr2 = [..., 3]; //
function sum(...nums) { return nums.reduce((a,b)=>a+b,0); }
```

---

## 19. JS modules

**Answer:**  
* Export & import across files.

```
// module.js
export const x = 5;

// main.js
import { x } from './module.js';
```

---

## 20. Higher-order functions

**Answer:**  
* Functions that take/return functions.

```
const doubled =.map(n => n*2);
```

---

## 21. Deep vs shallow copy

**Answer:**  
- Shallow: shared nested refs.  
- Deep: full clone.  

```
let obj = { a: 1, b: { c: 2 } };
let shallow = { ...obj };
let deep = JSON.parse(JSON.stringify(obj));
```

---

## 22. What is an IIFE?

**Answer:**  
* Function runs immediately.  

```
(function() { console.log("Hi"); })();
```

---

## 23. Difference between call, apply, and bind

**Answer:**  
- `call`: invoke with args list  
- `apply`: invoke with args array  
- `bind`: returns new bound function  

```
function greet(g){ console.log(g, this.name); }
const user = { name: "Alice" };
greet.call(user, "Hi");
greet.apply(user, ["Hello"]);
const bound = greet.bind(user, "Hey"); bound();
```

---

## 24. Currying

**Answer:**  
* Convert multi-arg fn → nested single-arg fns.

```
const curry = a => b => c => a+b+c;
console.log(curry(1)(2)(3)); // 6
```

---

## 25. Prototypal inheritance

**Answer:**  
* Objects inherit via prototype chain.  

```
const parent = { greet(){console.log("Hi");} };
const child = Object.create(parent);
child.greet();
```

---

## 26. Event delegation

**Answer:**  
* Listener on parent handles bubbling children.  

```
document.getElementById("list").addEventListener("click", e => {
  if(e.target.tagName === "LI") console.log("Item clicked");
});
```

---

## 27. Map, filter, reduce

**Answer:**  
- `map` → transform array  
- `filter` → select items  
- `reduce` → accumulate  

```
.map(x=>x*2);       //
.filter(x=>x>1);    //
.reduce((a,b)=>a+b,0); // 6
```

---

## 28. Optional chaining & nullish coalescing

**Answer:**  
- `?.` → safely access nested props  
- `??` → fallback for null/undefined  

```
let user = { profile: { name: "Bob" } };
console.log(user.profile?.name); // Bob
console.log(user.age ?? 18);     // 18
```

---

## 29. Debouncing vs throttling

**Answer:**  
- Debounce → run after inactivity  
- Throttle → run max once per interval  

```
function debounce(fn, delay) {
  let t; return (...args) => {
    clearTimeout(t); t=setTimeout(()=>fn(...args), delay);
  };
}
```

---

## 30. Object.freeze vs Object.seal

**Answer:**  
- `freeze`: no add/remove/edit.  
- `seal`: edit props ok, but no add/remove.  

```
let obj = { a: 1 };
Object.freeze(obj); // fully locked
Object.seal(obj);   // props editable only
```

---

## 31. Difference between Promise.all, Promise.any, Promise.allSettled, and Promise.race

**Answer:**  
- `Promise.all`: waits for all promises to resolve or rejects on first error.  
- `Promise.any`: resolves as soon as any promise resolves; rejects if all fail.  
- `Promise.allSettled`: waits for all to settle, returns their statuses.  
- `Promise.race`: resolves or rejects as soon as first promise settles.

---

## 32. What is callback hell? How do promises/async fix it?

**Answer:**  
- Nested callbacks causing unreadable code.  
- Promises and async/await flatten code and handle errors better.

---

## 33. What are web workers?

**Answer:**  
- Background threads running JS separate from the main thread to handle heavy tasks without blocking UI.

---

## 34. Difference between synchronous and asynchronous scripts (defer vs async)

**Answer:**  
- `async`: script executes as soon as it's downloaded, does not wait for HTML parsing.  
- `defer`: script executes after HTML parsing is complete, preserving order.

---

## 35. Difference between localStorage, sessionStorage, and cookies

**Answer:**  
- `localStorage`: persists with no expiration.  
- `sessionStorage`: cleared on tab close.  
- Cookies: sent with HTTP requests, size limited.

---

## 36. What is CORS? Why do we need it?

**Answer:**  
- Cross-Origin Resource Sharing controls how browsers and servers communicate to prevent unauthorized cross-domain requests.

---

## 37. Explain same-origin policy

**Answer:**  
- Browser security model restricting scripts from accessing resources from a different origin (protocol, domain, port).

---

## 38. Difference between for…of, for…in, and forEach

**Answer:**  
- `for...of`: iterates values of iterable objects.  
- `for...in`: iterates enumerable properties (keys).  
- `forEach`: array method to execute a function on each item.

---

## 39. Explain memoization. Implement it in JS

**Answer:**  
- Technique to cache results of expensive function calls.

```
const memoize = (fn) => {
  const cache = {};
  return (arg) => cache[arg] ??= fn(arg);
};
```

---

## 40. Explain the difference between setTimeout and setImmediate

**Answer:**  
- `setTimeout`: executes after the timer completes (minimum delay).  
- `setImmediate`: executes after I/O events callbacks (Node.js specific).

---

## 41. How does garbage collection work in JavaScript?

**Answer:**  
- Automatically frees memory of objects no longer referenced by the code.

---

## 42. Difference between NaN, Infinity, and isNaN()

**Answer:**  
- `NaN`: result of invalid math operation.  
- `Infinity`: value greater than any number.  
- `isNaN()`: checks if a value is NaN.

---

## 43. Explain event bubbling pitfalls with setTimeout(() => {}, 0)

**Answer:**  
- setTimeout callbacks run after current call stack and microtasks, possibly leading to unexpected event ordering.

---

## 44. Difference between Object.freeze and Object.seal

**Answer:**  
- `freeze`: no modifications allowed.  
- `seal`: prevents adding/removing properties, but allows modification.

---

## 45. Difference between promises and observables

**Answer:**  
- Promise: resolves once with single value.  
- Observable: streams multiple values over time.

---

## 46. How does JavaScript handle memory leaks?

**Answer:**  
- Occur when unused objects are still referenced, e.g., by closures or global variables, preventing garbage collection.

---

## 47. Explain immutability in JavaScript

**Answer:**  
- Data that cannot be changed after creation; changes return new copies instead.

---

## 48. Difference between global, function, and block scope

**Answer:**  
- Global: accessible everywhere.  
- Function: accessible within the function.  
- Block: accessible within `{}` (let/const).

---

## 49. Write code to flatten a nested array

**Answer:**

```
const flatten = arr => arr.flat(Infinity);
```

---

## 50. Explain prototypes and prototypal inheritance

**Answer:**  
- Each object has a prototype object from which it inherits properties and methods.

```
const proto = { greet() { return "Hi"; } };
const obj = Object.create(proto);
console.log(obj.greet());
```

---

