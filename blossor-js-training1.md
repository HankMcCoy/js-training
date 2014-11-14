JavaScript Training - Part I
============================

Intro
-----
* My premise: to do something well you must understand what you're doing. There are no shortcuts.
* Today: an analysis of the language of JavaScript.
* Next time: an analysis of the various tools available to make working with JavaScript better.

A brief history of JavaScript
-----------------------------
* Created by Brenden Eich in 10 days in May of 1995.
* Released as LiveScript (developed under the name Mocha) in Netscape Navigator. Changed to JS as a marketing ploy.
* Microsoft released JScript in '96, prompting Netscape to seek standardization.
* ECMA 262 Ed. 1 released in '97 as ECMAScript, followed by v2 and v3 in '98 and '99.
* ES3 is the basis of all even vaguely modern JS engines.
* DARK TIMES: '99-'09. ES4, ES4X, ES3.1, MADNESS. Eventually ES3.1 renamed to ES5, published in '09.
* Today: ES5 enjoys very [wide support](http://kangax.github.io/compat-table/es5/) and we're starting to see [features of ES6](http://kangax.github.io/compat-table/es6/) show up in the wild.
* Terminology summary: JavaScript is technically the name of Mozilla's implementation of ECMAScript (which has it's own [version numbers](https://developer.mozilla.org/en-US/docs/Web/JavaScript/New_in_JavaScript/1.8)).
* Understanding the difference between the versions of ES and JS will make a lot of writing on the topic make much more sense.

Nature of the beast
-------------------
* Primarily influenced by Self (prototypes), Scheme (functional), and C (imperative, syntax).
* Dynamically typed - types are associated with values, not variables.
* First-class functions - Can be passed, returned, assigned, can be nested to create closures.
* Prototype-based inheritance - JS does not have classes and never truly will.

Falsiness and equality
----------------------
* `null`, `undefined`, `0`, `''`, `[]`, and `NaN` are considered 'falsy'.
* Two equality operators. `===` pronounced equals and `==` pronounced maybe equals.

```js
// Transitivity. Who needs it?
'' == 0;   // true
0 == '0';  // true
'' == '0'; // false

// More transitivity (or lack thereof).
null != false;      // true
false != undefined; // true
null != undefined;  // false

// Identity, pssssh. Boring.
NaN === NaN; // false
```

Relatively simple syntactic and semantic pitfalls
------------------------------------------------
### Number, String, Object, and Array
Bad:

```js
var str = new String('a');
var num = new Number(3);
var obj = new Object();
var arr = new Array();
```

Good:

```js
var str = 'a';
var num = 3;
var obj = {};
var arr = [];
```

Reasoning:
* `'a' === 'a'` but `'a' !== new String('a')`.
* Literals keep things simpler.

### Variable scoping and hoisting
* Variables are scoped at the function level in JS.
* To create local scope use a self-invoking function

```js
(function () {
  // Do whatever you want to do within a local scope.
})();

// Or
!function () {
  // ...
}();
```

* Variable declarations and function declaration statements are hoisted.

```js
var foo = 1;
function bar() {
  if (!foo) {
    var foo = 10;
  }
  return foo;
}
// Returns 10.
bar();
```

* Function declaration statements are hoisted in their entirety.

```js
foo(); // Works.
bar(); // Breaks.

function foo() {
}
var bar = function () {
};
```

* Takeaway: place function/variable declarations at the top of their enclosing scope when possible.

Numbers
-------
* JavaScript is bad with numbers.

```js
0.1 + 0.2 === 0.3; // false

Math.pow(2, 53) === Math.pow(2, 53) + 1; // true
```

Automatic Semicolon Insertion
-----------------------------
* Semicolons are optional in JS.
* Whether or not to manually insert them is a topic that insights [holy war level fervor](https://github.com/twbs/bootstrap/issues/3057).

```js

// Section A - everything's hunky-dorey
var a = document.title
function d() {
  // ...
}
d()

// Section B - Will throw a TypeError: number is not a function
var a = document.title
(function () {
  // ...
})();

// Section C - hunky-dorey
function a() {
  return {
    foo: 'bar'
  }
}
var b = a().foo

// Section D - Will throw a TypeError: Cannot read property 'foo' of undefined
function a() {
  return
  {
    foo: 'bar'
  }
}
var b = a().foo
```

Strict Mode
-----------
* Introduced in ES5 as a way to opt-in to a stricter variant of JS.
* See MDN for a [complete description](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode).
* Changes include:
  * Prevents accidental global variable declaration.
  * Throws TypeErrors when attempting to assign to read-only properties.
  * Throws TypeErrors when attempting to delete non-deletable properties.
  * Requires that properties in object literals be unique.
  * Requires that function parameter be unique.
  * Prohibits octal syntax.
  * Prohibits `with` statements.
  * Prevents `eval` from introducing variables into the surrounding scope.
* Introduce at the function level instead of globablly to avoid breaking 3rd-party scripts.

Prototypal Inheritance
----------------------
* Not yet implemented

Methods worth knowing
---------------------
* `call`, `apply`
* `map`, `reduce`, `forEach`
* `Object.keys`, `Object.create`
* `slice`, `splice`

Coffeescript
------------
* What it fixes
* Things to beware

Organizing your code
--------------------
* Parameter passing
* Modules
* Testability

Glimpsing the future
--------------------
* ECMAScript 6
* ECMAScript 7
* Transpiled languages
  * CoffeeScript
  * TypeScript (AtScript, Flow)
  * Dart
  * ClojureScript

References
----------
* [JavaScript Weekly](http://javascriptweekly.com/)
* [Daily JS](http://dailyjs.com)
* [MDN](https://developer.mozilla.org/en-US/)
* [The Little Book on Coffeescript](http://arcturo.github.io/library/coffeescript/index.html), a little out of date
* [CoffeeScript Cookbook](http://coffeescriptcookbook.com/chapters/jquery/ajax)
* [Javascript Javascript](http://javascriptweblog.wordpress.com/), a blog about JS
* [Time to drop jQuery?](http://toddmotto.com/is-it-time-to-drop-jquery-essentials-to-learning-javascript-from-a-jquery-background/)
* [History of JS](https://www.w3.org/community/webed/wiki/A_Short_History_of_JavaScript)
* [ECMA 262 standards](http://www.ecma-international.org/publications/standards/Ecma-262-arch.htm)
* [ES5 compatibility](http://kangax.github.io/compat-table/es5/)
* [AirBNB's JS style guide](https://github.com/airbnb/javascript); includes helpful reasoning for why they chose the rules they did
