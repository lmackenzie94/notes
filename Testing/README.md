# Testing Notes

---

## Tables of Contents

1. [Overview](#overview)
2. [Types](#types)
3. [Test-Driven Development](#tdd)
3. [Testing React](#react)

<br><br>

<a name="overview"></a>

## Overview

> "Write tests. Not too many. Mostly integration" - Kent C. Dodds

- Put simply, a test is code that throws an error when the actual result of something does not match the expected output.
- Don't test implementation detail (user doesn't care what an element's id or class is).
- Tests generally follow a common structure comprised of three phases:
		1. **Arrange** - setup initial app state (ex. visit a web page, query for an element)
		2. **Act** - take an action (ex. interact with that element)
    3. **Assert** - make an assertion (ex. make an assertion about page content) 

<br><br>

<a name="types"></a>

## Types

**Unit:** Testing of individual units like functions or classes by supplying input and making sure the output is as expected (I.e. do pieces work in isolation)
- <ins>Best Tool:</ins> JEST

**Integration:** Testing processes across several units to achieve their goals, including their side effects (I.e. ensure different pieces of your application work together)
- Integration tests strike a great balance on the trade-offs between confidence and speed/expense.
- <ins>Best Tool:</ins> JEST

**Functional (e2e):** Testing how scenarios function on the product itself, by controlling the browser or the website. These tests usually ignore the internal structure of the application entirety and looks at them from the outside like on a black box (all you know is what goes in and what comes out).
- <ins>Best Tools:</ins> Cypress & Testcafe

**Static:** a software testing method that involves examination of the program's code and its associated documentation but does not require the program be executed.
- <ins>Best Tools:</ins> ESLint & FlowType & Prettier
      
> Integration tests often obviates the need for unit tests because if functions work properly together, they likely work properly in isolation.

<br><br>

<a name="tdd"></a>

## Test-Driven Development (TDD)

<br><br>

<a name="react"></a>

## Testing React
