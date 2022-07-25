# Introduction
Below are some short lessons and resources on programming concepts.

# The 'event loop'
As a single threaded language, JavaScript or ECMAScript, can only execute one line of code at a time. The currently running line is kept as part of a call stack (which you can see in your debugger) as a list of functions. Each new function, as it is executed, is pushed to the top of the call stack with its scopes and popped from the top of the stack upon its return. Using the callback queue and the event loop, built into the ECMAScript environment, it is possible to queue function calls for a new call stack for later execution. This is primarily how DOM events, such as click or scroll, are able to execute callback handler functions.

[Video - What is the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)<br/><br/>

# Set theory
A 'set' is, [mathematically speaking](https://en.wikipedia.org/wiki/Set_theory), an unordered group/pile of unique items Two sets can intersect, such that they have a series of indentical and potentially differing items. A set may be a subset or superset of any other, in that it contains only part of or includes the entirety of the second set. Sets can be joined in a union forming larger sets or split into further subsets; think [venn diagrams](https://en.wikipedia.org/wiki/Venn_diagram).

[Webpage - Basic set theory](https://plato.stanford.edu/entries/set-theory/basic-set-theory.html)<br>
[Video - Introduction to set theory - Discrete Mathematics](https://www.youtube.com/watch?v=tyDKR4FG3Yw)

### ... in JavaScript
Set theory is used in a variety of ways in both the [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) and [libraries](https://en.wikipedia.org/wiki/List_of_JavaScript_libraries) associated with JavaScript.

[jQuery](https://api.jquery.com/) is a utility library, predominantly used for manipulating the [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model). jQuery's main function, usually `$()`, returns a subset of document elements (`<div>, <span>, <a>`) against which to perform a variety of functions. jQuery has functions for [uniting jQuery sets](https://api.jquery.com/add/), for [generating jQuery subsets](https://api.jquery.com/filter/) and for [traversing the DOM heirarchy](https://api.jquery.com/children/). It is possible using jQuery to [attach a single event handler](https://api.jquery.com/on/) to all of the elements in the set using a single line. jQuery uses an [extended version of the CSS selector](https://api.jquery.com/jQuery/) syntax to select a subset of the elements in the document.

[Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) is a core JavaScript class designed to hold a set of variables ordered by an index, starting at index 0. Array has native functions for [uniting arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat), for [generating Array subsets](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) and for [transforming](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) and [manipulating](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) array items.

[Underscore.js](https://underscorejs.org/) and [lodash](https://lodash.com/docs/4.17.15) are both utility libraries for JavaScript. They both contain a series of functions which allow for Array [interections](https://lodash.com/docs/4.17.15#intersection), [differences](https://lodash.com/docs/4.17.15#difference), [unions](https://lodash.com/docs/4.17.15#union), [sorting](https://lodash.com/docs/4.17.15#sortedIndex), [grouping](https://lodash.com/docs/4.17.15#groupBy), etc.

As may be apparant from the above libraries, implementations of the core set theory concepts often allow for non-unique set items and often extend sets with sort order, item names and a whole raft of problem specific capabilities.

### ... in Databases
Set theory is the foundation on which modern databases function.

In [SQL (structured query language)](https://en.wikipedia.org/wiki/SQL), each table in a database is a set of unique rows/items. SQL allows the database administrators and systems designers to select and join the tables using the `FROM ... ON ...` clause, create subsets using the `WHERE` clause, and provides extra behaviour for sorting in `ORDER BY`, grouping in `GROUP BY` and projecting the result into a new table/set of the selected columns using the `SELECT` clause.

### ... in CSS
Each CSS statement begins with a [CSS selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors), the rules inside this statement are applied to the set of elements selected from the DOM by the selector. jQuery utilises this selector syntax in order to select DOM elements from within JavaScript.

# Primitives, object references and operators

## Primitives

## Object references

## Operators

# Patterns and paradigms

## Paradigms

### Functional vs object-orientated

#### Functional

#### Object orientated 

### Imperative vs declarative

#### Imperative

#### Declarative

## Patterns

### Sort

### MVC

### Observer/observable

# Modularisation

## Functions

## Classes

## Modules

## APIs

## Libraries

# Compilers

## Abstract Syntax Tress

## Bundlers

## Transpilers

## Pseudo-languages

# Design, implementation and planning

## Software development methodologies 

## Object-orientated design

## Project planning

### Gantt charts

### Critical path

### Risk management and critical thinking

# Media distribution

## Transport

## Encoding

# Accessibility

## Tools

### Market coverage

## Specifications

### Minimum compatible implementations

# Final notes
One of the newest and most documented engineering subdiciplines. Resources.