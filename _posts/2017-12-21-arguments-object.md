---
layout: post
title: "Javascript Arguments Object"
date: 2017-12-21
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
Like an Array, arguments can be accessed by an index and has a length. 
```javascript
 arguments[0] // firstarg
 arguments[1] // 2
 arguments[2] // true
 arguments.length // 4
 ```
### Arguments is an Object, Not an Array 
Arguments can not use array methods, like pop() and push().
Different ways to put arguments object into an array:
```javascript
  var args = [].slice.call(arguments); 
  var args = [].slice.call(arguments, 1); // start copying elements from index 1
  var args = [...arguments];  // ES6 
  var args = Array.from(arguments); // ES6
  // note Array.from(arguments, 1); is invalid
 ```

### For more info:
[Arguments Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments)

[Array.from()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)

## Example Use. 


Pass an array, followed by one or more arguments to the destroy function.
```javascript
destroy([1, 2, 3, 1, 2, 3], 2, 3);
 ```
Task: Remove all elements from the initial array that are of the same value as these arguments.
In the example, removing 2 and 3 from the array [1, 2, 3, 1, 2, 3] will result in [1, 1]

```javascript
function destroy(arr) {  
 var destroyNums = [].slice.call(arguments, 1); // [2, 3]
 
 // keep val if decision is true
 var arr2 = arr.filter(function(val) {
     var decision = false;
     // if array destroyNums does not have val, indexOf will return -1
     if (destroyNums.indexOf(val) === -1) {
       decision = true;
     }
     return decision;   
 }); 
 
 console.log("the final array: " + arr2) ; // the final array: 1, 1
 return arr2;  
}
 ```
 *The challenge is from [freecodecamp](https://www.freecodecamp.org/challenges/seek-and-destroy), and the solution is my own*
