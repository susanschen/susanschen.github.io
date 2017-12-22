---
layout: post
title: "Javascript Arguments Object"
date: 2018-12-21
---
# My Notes on Javascript
## Arguments Object

You can pass more arguments to a function than it accepts.
```javascript
function sample(one) { 
 console.log(one); // firstarg
 console.log(arguments); // Arguments(4) ["firstarg", 2, true, "sugar", callee: f, Symbol(Symbol.iterator): f]
}

sample('firstarg', 2, true, 'sugar');
```
Like an Array, it can be accessed by an index and has a length. 
```javascript
 arguments[0] // firstarg
 arguments[1] // 2
 arguments[2] // true
 arguments.length // 4
 ```
### Arguments is an Object, Not an Array 
Arguments does not have any other array methods, like pop() and push(), but you can convert it to an array.
Different ways to put arguments object into an array:
```javascript
  var args = [].slice.call(arguments); 
  var args = [...arguments];  // ES6 
  var args = Array.from(arguments); // copies all elements
  var args = Array.from(arguments, 1); // start copying elements from index 1
 ```

### For more info:
[source: mozilla.org](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)
