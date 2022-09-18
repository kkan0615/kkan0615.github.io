---
title: Javascript How to convert numbers between different bases
author: Youngjin Kwak
date: 2022-09-17 18:21:00 +0800
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
In this post, we will discuss how to convert numbers between different bases.
If you would like to test online, here is the [link](https://www.programiz.com/javascript/online-compiler/).

# Convert from number type to hex string type
```javascript
number.toString(radix)
```
```toString()``` is well known function for change type number to string.
if you pass the number type of radix as argument, ```toString(radix)``` returns a converted hex string value based on radix.
radix argument should be a number type and between 2 and 36.
Otherwise, there will be an error.

## Codes
We will look some example codes that is mostly used.

### Binary
```javascript
const num = 10;
console.log(num.toString(2)); // '1010'
```

### Ternary
```javascript
const num = 10;
console.log(num.toString(3)); // '101'
```

### Octal
```javascript
const num = 10;
console.log(num.toString(8)); // '12'
```

### Hexadecimal
```javascript
const num = 10;
console.log(num.toString(16)); // 'a'
```

# Convert from string type to decimal number type
Until now, we have seen how to change number to string.
From now on, we will discuss how to change string to number.
```javascript
parseInt(string, radix)
```
```parseInt(string)``` function is used for converting string type to int type.
if you pass the number type of radix as argument, ```parseInt(string, radix)``` returns a converted int value based on radix.
## Code
### Hexadecimal to Decimal
```javascript
const hex = 'a';
console.log(parseInt(hex, 16)); // 10
```


# Ref
- https://api.dart.dev/stable/2.13.4/dart-core/List-class.html#instance-properties

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
