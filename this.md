# THIS
---

* The value of **this** is determined by how a function is called.

* ES2015 introduced **arrow functions (=>)** which retains the **this** value of the *enclosing lexical context*.

---
### Global Context
In the **global execution context** (outside of any function), **this** refers to the global object.  

``` js
this === window

Example:
  this.b = "I'm outside"
  console.log(window.b, this.b, b) // returns "I'm outside"
```
---
### Function Context
* Inside a **function**, the value of this depends on how the function is called.

##### Simple Call: 
```js
      [ No Strict Mode ] 
  function abc() { return this; }

  abc() === window // In Browser
  abc() === global // In Node
```
---
```js
      [   Strict Mode  ] 
  function abc() { 
    'use strict';
    return this; 
  }

  abc() === undefined // In Browser && In Node
```
---
##### Using Call and Apply:
When a function uses **this** inside its body, the *value can be binded to an object* using **call** or **apply**.
```js
Example 1:

  const abc = { val : 'Custom' }; // val lives inside FUNCTION
  const val = 'Global';           // Val lives GLOBALLY

  function test() { return this.val; };

  test();                          // Returns 'Global'
  test.call(abc); test.apply(abc); // Returns 'Custom'
```
---
```js
Example 2:

  function add(firstNum) { 
    return firstNum + this.secondNum;
  }

  let abc = { secondNum : 2 };

  // 1st Parameter 'abc' replaces this, parameters > 1 are passed to add
  add.call(abc, 1);

  // 1st Parameter 'abc' replaces this, parameters > 1 in []format are passed to add
  add.apply(abc, [1]);
```
---
##### Using Bind:
* fn.bind(obj) creates a new function **with the same body and scope**, but **this** is permanently bound to the 1st arg of bind.

```js
function abc() { return this.a };
let def = abc.bind( { a: 'test' } ); // { a: 'test' } becomes this

def(); // Returns 'test' 

// In abc() => this.a becomes 37
let xyz = { a : 37, abc : abc }; 

// Trigger abc() with context this.a as 37
xyz.abc(); // Returns 37
```
---
##### Arrow Functions:
* In arrow functions, **this** retains the value of the **enclosing lexical context.**
```js
Example 1:
  const global = this;
  const abc    = (() => this);
  const def    = { func : abc };
  const ghi    = abc.bind(def);

  abc()         === global; // true ; 
  def.func()    === global; // true ; def.func accesses 'const abc()'
  abc.call(def) === global; // true ; def becomes this in abc()
  ghi()         === global; // true ; 
```

```js
Example 2:
  const abc = { xyz : function() { return (() => this) } };
  const def = abc.xyz();
  const ghi = abc.xyz;

  def()   === abc;    // true
  ghi()() === window; // true
