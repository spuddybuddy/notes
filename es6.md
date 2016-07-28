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



