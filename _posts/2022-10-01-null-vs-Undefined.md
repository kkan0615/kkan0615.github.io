---
title: Javascript Undefined vs Null vs Undeclared
author: Youngjin Kwak
date: 2022-10-08 11:52:00 +0800
categories: [javascript]
tags: [javascript]
image:
  path: ../images/javascript-logo.jpeg
  width: 800
  height: 500
  alt: javascript-logo.
---
---
# Overview
We will discuss about what’s the difference between null, undefined and undeclared, well-known javascript interview question.
You can test all codes with [javascript playground](https://codesandbox.io/s/ll8bj?file=/src/index.js)


# Undeclared
Undeclared means a variable is undeclared with an appropriate keyword like ```var```, ```let``` or ```const```.
Accessing an undeclared variable will throw a ```ReferenceError: tes is not defined``` error
## Example
```javascript
x = 'test string';
console.log(x);
```

# Undefined
A variable has not been assigned yet after it is declared. ```undefined``` is a ```primitive data type```.

## Example
```javascript
let x;
console.log(x); // undefined
console.log(typeof x); // undefined

function test() {};
console.log(test()); // undefined

const testObj = {};
console.log(testObj.fake); // undefined
```
## Note
- A function that does not contain any ```return``` returns ```undefined```
- Non-existent properties in an object returns ```undefined```
- A variable can be set to equal ```undefined```

# Null
A variable is declared and assigned by a value of ```null```.
It means ```null``` must be assigned.
```null``` is also ```primitive data type``` like undefined.
## Example
```javascript
let x = null;
console.log(x); // null
console.log(typeof x); // object
```
## Note
- ```typeof null``` prints ```object```, but null is ```primitive value```.

### Why is typeof null "object"
A fix was proposed for ECMAScript (via an opt-in), but was rejected. It would have resulted in typeof null === "null".

# More
- In loosely equal(==), ```undefined == null``` is ```ture```
- In strictly equal (===) ```undefined === null``` is ```false```

# Ref
- [JS Interview Question: What’s the difference between a variable that is: null, undefined or undeclared?](https://dev.to/nashmeyah/undefined-vs-null-vs-undeclared-9f8#:~:text=Null%20is%20pointing%20to%20nothing,const%2C%20var%2C%20or%20let.)
- [What's the difference between undeclared, undefined and null in JavaScript?](https://rlynjb.medium.com/js-interview-question-what-s-the-difference-between-a-variable-that-is-null-undefined-or-bf7233cef1c2)
- [https://dev.to/nashmeyah/undefined-vs-null-vs-undeclared-9f8#:~:text=Null%20is%20pointing%20to%20nothing,const%2C%20var%2C%20or%20let.](https://www.30secondsofcode.org/articles/s/javascript-undeclared-undefined-null)
- [Undefined vs. Null vs. Undeclared](https://dev.to/nashmeyah/undefined-vs-null-vs-undeclared-9f8#:~:text=Null%20is%20pointing%20to%20nothing,const%2C%20var%2C%20or%20let.)
- [undefined와 null의 차이점이란 ?](https://99geo.tistory.com/69#:~:text=undefined%EC%9D%80%20%EB%B3%80%EC%88%98%EB%A5%BC%20%EC%84%A0%EC%96%B8,%EC%9E%90%EB%A3%8C%ED%98%95%EC%9D%B4%20%EC%97%86%EB%8A%94%20%EC%83%81%ED%83%9C%EC%9D%B4%EB%8B%A4.)
- [Why is typeof null "object"?](https://stackoverflow.com/questions/18808226/why-is-typeof-null-object)
- [JavaScript — Null vs. Undefined](https://codeburst.io/javascript-null-vs-undefined-20f955215a2)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
