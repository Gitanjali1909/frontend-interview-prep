# JavaScript Interview Q&A

A curated list of 20 common JavaScript interview questions with **short answers, code examples, and mini diagrams** for quick revision. 🚀

---

## 1. What are `var`, `let`, and `const`?

**Answer:**  
- `var` → function-scoped, can be re-declared & updated.  
- `let` → block-scoped, can be updated but not re-declared.  
- `const` → block-scoped, cannot be updated or re-declared.

```js
var a = 10;
let b = 20;
const c = 30;
````

**Visual:**

```text
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

```js
console.log(x); // undefined
var x = 5;

foo(); // works
function foo() { console.log("Hello"); }
```

**Visual:**

```text
Compilation: var x; function foo() {}
Execution: x = 5; foo()
```

---

## 3. Explain closures.

**Answer:**

* Function that **remembers its lexical scope** even after outer function finishes.

```js
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

```text
outer() scope
 └─ inner() remembers count
```

---

## 4. Difference between `==` and `===`

**Answer:**

* `==` → value equality (type coercion allowed)
* `===` → strict equality (type + value)

```js
5 == '5'  // true
5 === '5' // false
```

**Visual:**

```text
5 == '5'  -> converts '5' -> 5 == 5 ✅
5 === '5' -> type mismatch ❌
```

---

## 5. Difference between `null` and `undefined`

**Answer:**

* `undefined` → variable declared, not assigned
* `null` → explicitly “no value”

```js
let a;
console.log(a); // undefined
let b = null;
console.log(b); // null
```

**Visual:**

```text
Declared but empty -> undefined
Explicit no value -> null
```

---

## 6. Explain `this` keyword

**Answer:**

* Refers to the **current execution context**.

```js
console.log(this); // window/global object

function foo() { console.log(this); }
foo(); // window

const obj = { foo };
obj.foo(); // obj
```

**Visual:**

```text
Function call -> global
Method call   -> owning object
Arrow func    -> lexical this
```

---

## 7. What is the event loop?

**Answer:**

* JS is single-threaded. Event loop handles async callbacks **without blocking** the main thread.

```js
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

```text
Call Stack -> Web API -> Callback Queue -> Event Loop -> Stack
```

---

## 8. Event bubbling and capturing

**Answer:**

* Event bubbling → event moves from **child → parent → ancestor**
* Event capturing → event moves from **ancestor → parent → child**

```js
child.addEventListener('click', e => console.log('Child clicked'), false);
```

**Visual:**

```text
Capturing: Grandparent -> Parent -> Child
Bubbling: Child -> Parent -> Grandparent
```

---

## 9. Arrow functions vs regular functions

**Answer:**

* Arrow functions **do not have their own `this`**
* Cannot be used as constructors
* Shorter syntax

```js
const add = (a, b) => a + b;
```

**Visual:**

```text
Arrow -> lexical this
Function -> dynamic this
```

---

## 10. Callback functions

**Answer:**

* A function passed as an argument to another function, executed later.

```js
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
* Methods: `.then()`, `.catch()`, `.finally()`

```js
let p = new Promise((resolve, reject) => resolve('Done'));
p.then(res => console.log(res));
```

---

## 12. Async/Await

**Answer:**

* Syntax sugar over Promises, allows **writing async code like sync**.

```js
async function fetchData() {
  let res = await fetch('url');
  console.log(await res.json());
}
```

---

## 13. Synchronous vs Asynchronous

**Answer:**

* Sync → executes one by one, blocks code
* Async → executes independently, non-blocking

```js
console.log("A");
setTimeout(() => console.log("B"), 0);
console.log("C");
// Output: A C B
```

---

## 14. JavaScript data types

**Answer:**

* Primitive → string, number, boolean, null, undefined, symbol, bigint
* Reference → objects, arrays, functions

---

## 15. Template literals

**Answer:**

* Backticks `` ` `` for string interpolation and multi-line strings

```js
let name = 'Alice';
console.log(`Hello ${name}`);
```

---

## 16. Destructuring

**Answer:**

* Extract values from arrays/objects

```js
const [a, b] = [1, 2];
const {x, y} = {x: 10, y: 20};
```

---

## 17. Default parameters

**Answer:**

* Functions can have default values

```js
function greet(name='Guest') { console.log(`Hi ${name}`); }
greet(); // Hi Guest
```

---

## 18. Spread/Rest operator

**Answer:**

* Spread `...` → expand elements
* Rest `...` → collect elements into array

```js
const arr = [1,2];
const arr2 = [...arr,3]; // [1,2,3]
function sum(...nums) { return nums.reduce((a,b)=>a+b,0); }
```

---

## 19. JS modules

**Answer:**

* Export & import code between files

```js
// module.js
export const x = 5;

// main.js
import { x } from './module.js';
```

---

## 20. Higher-order functions

**Answer:**

* Functions that take or return functions

```js
const numbers = [1,2,3];
const doubled = numbers.map(n => n*2);
```
