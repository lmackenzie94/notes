# JavaScript Notes

---

### Tables of Contents

1. [Overview](#overview)
2. [Obejcts](#objects)
3. [Arrays](#arrays)
4. [Var, Let, Const](#vars)
5.

---

<a name="overview"></a>

#### Overview

- First created in 1995 by Brendan Eich
- Syntax is based on Java and C
- Was originally created as a browser-only language, but is now used in many environments.
- Is a **scripting** language (i.e. no compilation step in the execution of code)
- Everything is an object (except primitive types)
- Is "**dynamically typed**" (i.e. variables are not bound to a data type)
- **Eight Data Types:** Object (non-primitive) & Symbols, Array, Number, BigInit, String, , Boolean, Null, Undefined
  - "Typeof null" returns "object" - this is an error in the language
- Common JS engines: **V8** (Chrome and Opera); **SpiderMonkey** (Firefox)
  - Engines "parse" (read) the script and "compiles" (converts) it to machine language, which then runs.
- Is a “safe” programming language (i.e. it does not provide low-level access to memory or CPU)
- Common languages that get compiled to JS before running in the browser:
  - CoffeeScript (syntactic sugar), TypeScript (strict typing; Microsoft), Flow (typing; Facebook), Dart (stand-alone language that can be transpiled to JS; Google)

---

<a name="vars"></a>

#### Var, Let, Const

**Var** - function scoped.
**Let** - block-scoped; CAN be reassigned; can be initialized without setting a value
**Const** - block-scoped; can NOT be reassigned ("constant"); must assign a value when the variable is declared

TIP: it's common practice to name hard-coded variables (i.e. not evaluated at run-time) with capitals and underscores.

- ex. const BIRTHDAY = "03.25.1994"

---

#### <span style="color:red">Key Terms</span>

**Lexical Environment** - where something sits physically in the code you write, and what surrounds it. A lexical environment exists in programming languages in which where you write something is important.
