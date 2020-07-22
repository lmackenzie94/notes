# JavaScript Notes

---

## Tables of Contents

1. [Overview](#overview)
2. [Var, Let, Const](#vars)
3. [Closures](#closures)
4. [Currying](#currying)
5. [Bind, Call, Apply](#bca)
6. [Event Propagation / Bubbling / Capturing](#events)
7. [Hoisting](#hoist)
8. [The arguments object / rest parameters](#args)

<br><br>

<a name="overview"></a>

## Overview

- First created in **1995** by Brendan Eich
- Syntax is based on Java and C
- Was originally created as a browser-only language, but is now used in many environments.
- Is a **scripting language** (i.e. no compilation step in the execution of code - the JS engine reads, interprets, and runs your code on the fly)
- Is **dynamically typed** (i.e. variables are not bound to a data type. For example, a variable originally set to a string can later be changed to a number)
- Is **single threaded** (i.e. code is executed in order and cannot move on to the next piece of code before the current code is finished)
- Everything is an object (except primitive types)
- **Nine Data Types:** Object (non-primitive), Function, Symbol, Number, BigInit, String, Boolean, Null, Undefined
  - "Typeof null" returns "object" - this is an error in the language
- Common JS engines: **V8** (Chrome and Opera); **SpiderMonkey** (Firefox)
  - Engines "parse" (read) the script and "compiles" (converts) it to machine language, which then runs.
- Is a “safe” programming language (i.e. it does not provide low-level access to memory or CPU)
- Common languages that get compiled to JS before running in the browser:
  - CoffeeScript (syntactic sugar), TypeScript (strict typing; Microsoft), Flow (typing; Facebook), Dart (stand-alone language that can be transpiled to JS; Google)

---
<br><br>

<a name="vars"></a>

## Var, Let, Const

**Var** - function scoped.

**Let** - block-scoped; CAN be reassigned; can be initialized without setting a value.

**Const** - block-scoped; can NOT be reassigned ("constant"); must assign a value when the variable is declared.

> **TIP:** it's common practice to name hard-coded variables (i.e. not evaluated at run-time) with capitals and underscores. <br>
ex. const BIRTHDAY = "03.25.1994"

---
<br><br>

<a name="closures"></a>

## Closures

A closure **gives you access to an outer function's scope from an inner function**, regardless of whether the execution contexts of the outer function still exists.

```javascript
function greet() {
  const greeting = 'Hello'
  return function(name){
    console.log(`${greeting}, ${name}`)
  }
}
```

Above, the execution context of the inner function has "closed in" the outer variables that it would normally have access to anyway.

---
<br><br>

<a name="currying"></a>

## Currying

Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c). Put another way, currying **transforms a function with multiple arguments into a sequence of functions each taking a single argument.**

---
<br><br>

<a name="bca"></a>

## Bind, Call, Apply

> All have to do with the <code>this</code> variable, which is created by the JS engine with every new execution context.

**Bind:** allows us to set the <code>this</code> variable NOW while allowing you to execute the function LATER, because it **returns a new function object**

**Call:** similar to bind, except it's used to set the <code>this</code> variable NOW and execute the function NOW. 

**Apply:** exact same as call, except it accepts an array of arguments instead of one by one.

---
<br><br>

<a name="events"></a>

## Event Propagation - Bubbling & Capturing

> REMEMBER: When an event occurs on a DOM element, that event does not entirely occur on that just one element.

**Bubbling:** When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors
 - most, but not all events bubble (ex. focus)
 - the most deeply nested element that caused the event is called a target element, accessible as event.target.
 - because of bubbling, we could add a listener on a parent element (ex. form) and handle clicks within using <code>event.target</code>
    - this is called **event delegation** and is one of the most powerful event handling patterns.
 - while it's possible to stop bubbling using <code>event.stopPropagation()</code> and event.stopImmediatePropagation()</code> , it's rarely necessary.

Note the differences from <code>this (=event.currentTarget):</code>

<code>event.target</code> – is the “target” element that initiated the event, it doesn’t change through the bubbling process.
<code>this</code> – is the “current” element, the one that has a currently running handler on it.
<br><br>

**Capturing:** the event starts from <code>window</code> and goes down to every element until it reaches the target element
  - rarely used and normally invisible to us.
  - to use, set the 3rd parameter of <code>.addEventListener()</code> to <code>true</code>

### SUMMARY
When an event happens:
  1) it **moves down from the document root** to <code>event.target</code>. On the way, it calls all event listeners/handlers with the 3rd (capture) param set to <code>true</code>
  2) next, the **handlers are called on the target element** itself
  3) then, the **event bubbles up to the root** calling all event listeners/handlers without the 3rd param (defaults to <code>false</code>

### ASIDE
> **Three ways of assigning event handlers:**
>  1) HTML attribute: <code>onclick="..."</code>
>  2) DOM property: <code>elem.onclick = function</code>
>  3) Methods: <code>elem.addEventListener(event, handler[, phase])</code> to add, <code>removeEventListener</code> to remove.

---
<br><br>

<a name="hoist"></a>

## Hoisting

> Definition: "an act of raising or lifting"

While it's helpful to imagine code being moved to the top of their scope when the JS engine interprets your code, remeber that **nothing actually moves.**

The aforementioned interpretation happens in two phases: **compilation** and **execution**. During compilation, the JS engine parses the code for all function and variable declaration and alots space in memory. This process of “lifting” the variable and giving it a space in memory is called hoisting.

**Are variables declared with let and const hoisted?**

Yes! 

- <code>let</code>, <code>const</code>, and <code>class</code> are **hoisted but not initialized.**
    - The time between these variables being declared and being evaluated is referred to as the **temporal dead zone**. If you try to access these variables within this dead zone, you will get the reference error.

- <code>var</code> and <code>function</code> (i.e. function declarations) are **hoisted and automatically initalized to <code>undefined</code>**.
    - NOTE: only during the execution phase does the variable get assigned its value. This is why in the 'age' example below, the first log prints <code>undefined</code> not <code>26</code>.

```javascript
console.log(name) // Uncaught ReferenceError: name is not defined
let name = 'Luke'

console.log(age) // undefined
var age = 26
console.log(age) // 26
```

---
<br><br>

<a name="args"></a>

## The <code>arguments</code> object

- Is an Array-like object accessible inside non-arrow functions that contains the values of the arguments passed to that function.

```javascript
function func1(a,b,c){
  console.log(arguments) // Arguments(3) [1, 2, 3, callee: ƒ, Symbol(Symbol.iterator): ƒ]
  console.log(arguments[0]) // 1
}

func1(1,2,3)
```

> If you're writing ES6 compatible code, then **rest parameters** should be preferred.

### Rest Parameters
- allows us to represent an indefinite number of arguments as an array.

```javascript
function func2(a, b, ...moreArgs){
  console.log(a) // 1
  console.log(b) // 2
  console.log(moreArgs) // [3, 4, 5]
}

func2(1,2,3,4,5)
```

**Unlike <code>arguments</code>, rest parameters work with arrow functions:**
```javascript
const func3 = (a, b, ...moreArgs) => {
  console.log(a) // a
  console.log(b) // b
  console.log(moreArgs) // ['c', 'd', 'e']
}

func3('a','b','c','d','e')
```

---
<br><br>

## Key Terms

**Lexical Environment** - where something sits physically in the code you write, and what surrounds it. A lexical environment exists in programming languages in which where you write something is important.

<br>

### To add:

- <code>==</code> vs <code>===</code>
- Higher Order Functions
- "use strict"
- <code>this</code>
- prototype
- immediately invoked function expression (IIFE)
- [others](https://dev.to/macmacky/70-javascript-interview-questions-5gfi#14-whats-the-difference-between-and-)
