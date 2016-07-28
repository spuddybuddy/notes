# ES6

## for-of
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
## iterators
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
## generators
iterator generating function.
```
function* range(start, stop) {
  for (var i = start; i < stop; i++)
    yield i;
}

for (var value of range(start, stop)) {
  alert("Ding! at floor #" + value);
}
```
[Q.async](http://jlongster.com/A-Study-on-Solving-Callbacks-with-JavaScript-Generators): interesting (experimental) way to write asynchronous code by iterative continuation passing.
## template strings
Within backtick strings, include `${EXPR}` to implement string interpolation. `EXPR` will be evaluated and coerced to string. 
```
function authorize(user, action) {
  if (!user.hasPrivilege(action)) {
    throw new Error(
      `User ${user.name} is not authorized to do ${action}.`);
  }
}
```
## rest parameters & defaults
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
## destructuring
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
