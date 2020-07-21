# JavaScript Notes

---

## Tables of Contents

1. [Overview](#overview)
2. [Obejcts](#objects)
3. [Arrays](#arrays)
4. [Var, Let, Const](#vars)
5. [Closures](#closures)
6. [Currying](#currying)

---

<a name="overview"></a>

### Overview

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

<a name="vars"></a>

### Var, Let, Const

**Var** - function scoped.

**Let** - block-scoped; CAN be reassigned; can be initialized without setting a value

**Const** - block-scoped; can NOT be reassigned ("constant"); must assign a value when the variable is declared


**TIP:** it's common practice to name hard-coded variables (i.e. not evaluated at run-time) with capitals and underscores.

- ex. const BIRTHDAY = "03.25.1994"

---

<a name="closures"></a>

### Closures

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

<a name="currying"></a>

### Currying

Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c). Put another way, currying **transforms a function with multiple arguments into a sequence of functions each taking a single argument.**

---

#### <span style="color:red">Key Terms</span>

**Lexical Environment** - where something sits physically in the code you write, and what surrounds it. A lexical environment exists in programming languages in which where you write something is important.
