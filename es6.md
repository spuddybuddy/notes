# ES6

Source: https://hacks.mozilla.org/category/es6-in-depth/

## [for-of](https://hacks.mozilla.org/2015/04/es6-in-depth-iterators-and-the-for-of-loop/)
```
for (VAR of ITERABLE) {
  STATEMENTS
}

for (var word of uniqueWords) {
  console.log(word);
}

for (var [key, value] of phoneBookMap) {
  console.log(key + "'s phone number is: " + value);
}
```
## [iterators](https://hacks.mozilla.org/2015/04/es6-in-depth-iterators-and-the-for-of-loop/)
```
var zeroesForeverIterator = {
  [Symbol.iterator]: function () {
    return this;
  },
  next: function () {
    return {done: false, value: 0};
  }
};
```
### optional methods
```
  // Called if loop exits prematurely
  return: function() { DO CLEANUP }
  throw: function(exc) { ??? }
```
## [generators](https://hacks.mozilla.org/2015/05/es6-in-depth-generators/)
Iterator generating function.
```
function* range(start, stop) {
  for (var i = start; i < stop; i++)
    yield i;
}

for (var value of range(start, stop)) {
  alert("Ding! at floor #" + value);
}
```
Can use generators to coordinate with asynchronous operations in the caller by passing values to next().  See: https://hacks.mozilla.org/2015/07/es6-in-depth-generators-continued/
## [template strings](https://hacks.mozilla.org/2015/05/es6-in-depth-template-strings-2/)
Within backtick strings, include `${EXPR}` to implement string interpolation. `EXPR` will be evaluated and coerced to string. 
```
function authorize(user, action) {
  if (!user.hasPrivilege(action)) {
    throw new Error(
      `User ${user.name} is not authorized to do ${action}.`);
  }
}
```
## [rest parameters & defaults](https://hacks.mozilla.org/2015/05/es6-in-depth-rest-parameters-and-defaults/)
```
function containsAll(haystack, ...needles) {
  for (var needle of needles) {
    if (haystack.indexOf(needle) === -1) {
      return false;
    }
  }
  return true;
}
```
Call assigns parameters 2-N to `needles` Array.
```
function animalSentence(animals2="tigers", animals3="bears") {
  return `Lions and ${animals2} and ${animals3}! Oh my!`;
}
```
Defaults evaluated left-to-right at call-time.  Can be expressions.  Dynamically scoped?
## [destructuring](https://hacks.mozilla.org/2015/05/es6-in-depth-destructuring/)
```
var [first, second, third] = someArray;

var [foo, [[bar], baz]] = [1, [[2], 3]];
console.log(foo);
// 1
console.log(bar);
// 2
console.log(baz);
// 3

var [,,third] = ["foo", "bar", "baz"];
console.log(third);
// "baz"
```
### rest argument
```
var [head, ...tail] = [1, 2, 3, 4];
console.log(tail);
// [2, 3, 4]
```
### objects
```
var robotA = { name: "Bender" };
var robotB = { name: "Flexo" };

var { name: nameA } = robotA;
var { name: nameB } = robotB;

console.log(nameA);
// "Bender"
console.log(nameB);
// "Flexo"
```
### assignment
`({ safe } = {});`
### default values
```
var [missing = true] = [];
console.log(missing);
// true
```
### iteration
```
var map = new Map();
map.set(window, "the global");
map.set(document, "the document");

for (var [key, value] of map) {
  console.log(key + " is " + value);
}
// "[object Window] is the global"
// "[object HTMLDocument] is the document"

for (var [key] of map) {
  // ...
}

for (var [,value] of map) {
  // ...
}
```
### return values
```
function returnMultipleValues() {
  return {
    foo: 1,
    bar: 2
  };
}
var { foo, bar } = returnMultipleValues();
```
## [arrow functions](https://hacks.mozilla.org/2015/06/es6-in-depth-arrow-functions/)
Automatically binds lexically scoped `this`
```
var selected = allJobs.filter(job => job.isSelected());
var total = values.reduce((a, b) => a + b, 0);
var chewToys = puppies.map(puppy => ({})); // ok
$("#confetti-btn").click(event => {
  playTrumpet();
  fireConfettiCannon();
});
```
## [symbols](https://hacks.mozilla.org/2015/06/es6-in-depth-symbols/)
Symbols are values that programs can create and use as property keys without risking name collisions.
```
var mySymbol = Symbol();
```
Can share symbols by using a string key.
```
Symbol.for("cat") // Always returns same Symbol
```
## [collections](https://hacks.mozilla.org/2015/06/es6-in-depth-collections/)

Iteration is done in insertion order.
### Set
```
new Set()
new Set(iterable);
Set.prototype.add(value)
Set.prototype.clear()
Set.prototype.delete(value)
Set.prototype.entries()
Set.prototype.forEach() // f(value, value, set)
Set.prototype.has(value)
Set.prototype.values()
Set.prototype.size()
Set.prototype[@@iterator]()
```
### Map
```
new Map()
new Map(iterable) // Iterable of [key, value]
Map.prototype.clear()
Map.prototype.delete(key)
Map.prototype.entries()
Map.prototype.forEach() // f(value, key, map)
Map.prototype.get(key)
Map.prototype.has(key)
Map.prototype.keys()
Map.prototype.set(key, value)
Map.prototype.values()
Map.prototype.size()
Map.prototype[@@iterator]()
```
## [proxies](https://hacks.mozilla.org/2015/07/es6-in-depth-proxies-and-reflect/)
Reflection API, for metaprogramming and customizing property access and method calls.  Useful for logging, mocking, debugging.
## [classes](https://hacks.mozilla.org/2015/07/es6-in-depth-classes/)
```
class Circle {
    constructor(radius) {
        this.radius = radius;
        Circle.circlesMade++;
    };

    static draw(circle, canvas) {
        // Canvas drawing code
    };

    static get circlesMade() {
        return !this._count ? 0 : this._count;
    };
    static set circlesMade(val) {
        this._count = val;
    };

    area() {
        return Math.pow(this.radius, 2) * Math.PI;
    };

    get radius() {
        return this._radius;
    };
    set radius(radius) {
        if (!Number.isInteger(radius))
            throw new Error("Circle radius must be an integer.");
        this._radius = radius;
    };
}
```
## [subclassing](https://hacks.mozilla.org/2015/08/es6-in-depth-subclassing/)
`Foo extends Bar` sets prototype of Bar to Foo and sets prototype of Bar.prototype to Foo.prototype.
`super` is used to access the prototype of the superclass.
```
class Shape {
    get color() {
        return this._color;
    }
    set color(c) {
        this._color = parseColorAsRGB(c);
        this.markChanged();  // repaint the canvas later
    }
}

class Circle extends Shape {
  // As above
}
```
## [let and const](https://hacks.mozilla.org/2015/07/es6-in-depth-let-and-const/)
### let
`let` is a sane, lexically scoped replacement for `var`.
* `let` is block scoped
* `let` variable declared in a loop is rebound on each loop iteration (okay to capture in closures)
* `let` variable cannot be redeclared
* `let` variable cannot be accessed before declaration
* `let` declarations do not create properties on the global object

### const
A `let` variable assigned only at declaration.
## [modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/)
`export` determines what declarations are available to other modules.
You can export any top-level function, class, var, let, or const.
```
export function detectCats(canvas, options) {
  var kittydar = new Kittydar(options);
  return kittydar.detectCats(canvas);
}

export class Kittydar {
  ... several methods doing image processing ...
}

// This helper function isn't exported.
function resizeCanvas() {
  ...
}
```
`import` brings in exported declarations from another file.
```
import {detectCats, Kittydar} from "kittydar.js";

function go() {
  var canvas = document.getElementById("catpix");
  var cats = detectCats(canvas);
  drawRectangles(canvas, cats);
}

// Import all declarations.
import * as cows from "cows";
```
`export` can re-export declarations.
```
// import "sri-lanka" and re-export some of its exports
export {Tea, Cinnamon} from "sri-lanka";

// import "equatorial-guinea" and re-export some of its exports
export {Coffee, Cocoa} from "equatorial-guinea";

// import "singapore" and export ALL of its exports
export * from "singapore";
```
If you want to lazy-load imports, arrange modules into bundles, etc. then you'll need library and tool support.
e.g. http://webpack.github.io/docs/


