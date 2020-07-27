# Testing Notes

---

## Tables of Contents

1. [Overview](#overview)
2. [Types](#types)
3. [Test-Driven Development](#tdd)
4. [Tools](#tools)
5. [Testing React](#react)

<br><br>

<a name="overview"></a>

## Overview

> "Write tests. Not too many. Mostly integration" - Kent C. Dodds

- Put simply, a test is code that throws an error when the actual result of something does not match the expected output.
- Test behaviour (what app should do) instead of implementation (how app works).
- Tests generally follow a common structure comprised of three phases:<br/>
	1. **Arrange** - setup initial app state (ex. visit a web page, query for an element)<br/>
	2. **Act** - take an action (ex. interact with that element)<br/>
	3. **Assert** - make an assertion (ex. make an assertion about page content)<br/>
- Always make sure you can break your tests.

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

> In short, write tests before the code.

**Red-Green Testing:** write "shell" function -> write tests -> tests fail -> write code -> tests pass!
- Why? More efficient; better code; fewer bugs; great code coverage; requires planning = fewer false starts.

<br><br>

<a name="tools"></a>

## Tools

1) **Jest**
	- fully-featured testing framework. Runs all your tests. Has an entire assertion library.
	- Works great with React, but not limited to it.

2) **Enzyme**
	- a library specifically for testing React components.
	- integrates with many full testing libraries, including Jest.
	- creates a virtual DOM for testing.
	- allows testing without a browser.
	- uses React DOM but also gives us a tool kit for searching through the DOM, simulating simple events, etc. 

<br><br>

<a name="react"></a>

## Testing React

- Similar to testing other JavaScript code.
- Broadly two ways:
	1) Rendering component trees in a simplified test environment and asserting on their output.
	2) Running a complete app in a realistic browser environment (also known as “end-to-end” tests).

### Tools:
**Jest:** (see above) is a JavaScript test runner that lets you access the DOM via jsdom.
**React Testing Library:** is a set of helpers that let you test React components without relying on their implementation details. This approach makes refactoring a breeze and also nudges you towards best practices for accessibility. 

### Testing Recipes: 
- assumes you're using Jest as a test runner.
- for more detail, see the [React docs](https://reactjs.org/docs/testing-recipes.html)

**Setup/Teardown**
- use beforeEach() and afterEach() to render our React tree to a DOM element that's attached to <code>document</code>

**act()**
- a helper that ensures all updates related to tasks like rendering, user events, data fetching, etc. have been applied to the DOM before you make any assertions.

> Not necessary if using *React Testing Library* since all its helpers are wrapped with act()

**Rendering**
- you might want to test whether a component renders correctly for given props.

```javascript
act(() => {
    render(<Hello name="Jenny" />, container);
  });
  expect(container.textContent).toBe("Hello, Jenny!");
```

**Data Fetching**
- Instead of calling real APIs in all your tests, you can mock requests with dummy data to make them run faster and prevent flaky tests due to an unavailable backend.

**Mocking Modules**
- Some modules might not work well inside a testing environment, or may not be as essential to the test itself. Mocking out these modules with dummy replacements can make it easier to write tests for your own code.

**Events**
- React recommends dispatching real DOM events on DOM elements, and then asserting on the result. 
- without *React Testing Library* use <code>.dispatchEvent()</code>; with, use <code>fireEvent()</code>

**Timers**
**Snapshot Testing**
**Multiple Renderers**
**Something Missing?**


