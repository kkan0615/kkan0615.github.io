---
title: What is different attribute and property in javascript
author: Youngjin Kwak
date: 2022-09-24 20:51:00 +0800
categories: [javascript, html]
tags: [javascript, html]
image:
  path: ../images/javascript-logo.jpeg
  width: 800
  height: 500
  alt: javascript-logo.
---
---
# Overview
The terms attribute and property can be confusing in HTML. You can test all the codes on [playground](https://playcode.io/javascript).

# Attribute vs Property
## Attribute
- Defined by HTML. (related to HTML)
- Attribute value can not be changed.
- Attributes initialize DOM properties when the browser parses the HTML to generate DOM objects for HTML tags.
- referring to additional information of an object.
- Attribute update the property synchronously.

## Property
- Defined by the DOM. (related to DOM)
- Property value can be changed after it's initialized
- describing the characteristics of an object.
- Property change does not affect the attribute.


# See more with code
Let's consider that there is following html element in your project.
```html
<input id="name-input" type="text" value="name">
```
In input html element, there are three attributes. ```id```, ```type``` and ```value```.
Once the browser parses this HTML code, a ```HTMLInputElement``` object will be created.
JS DOM objects consist of many properties such as accept, checked, classList, className, etc.
The properties may be different by DOM objects.

## Check "attribute" is existed in element
```javascript
const nameInput = document.querySelector('#name-input')
console.log(nameInput.hasAttribute('type')) // true
console.log(nameInput.hasAttribute('name')) // false
```

## Get collection of all attributes
```javascript
const nameInput = document.querySelector('#name-input')
console.log(nameInput.attributes) // { 0: Attr { ... }, 1: Attr { ... } }
```

## Remove "attribute"
```javascript
const nameInput = document.querySelector('#name-input')
nameInput.removeAttribute('value')
console.log(nameInput.value) // undefined
```

## Access "property" value by "attribute"
```javascript
const nameInput = document.querySelector('#name-input')
console.log(nameInput.value) // "name"
console.log(nameInput.getAttribute('value')) // "name"
```

## Update "property" value with "attribute"
```javascript
const nameInput = document.querySelector('#name-input')
nameInput.value = 'changed'
nameInput.setAttribute('value', 'changed');
```

# Ref
- (https://stackoverflow.com/questions/6003819/what-is-the-difference-between-properties-and-attributes-in-html)
- (https://gomakethings.com/the-difference-between-attributes-and-properties-in-vanilla-js/#:~:text=In%20JavaScript%20(the%20DOM%2C%20really,property%20is%20the%20current%20state.)
- (https://www.geeksforgeeks.org/what-is-the-difference-between-properties-and-attributes-in-html/)
- (https://javascript.info/dom-attributes-and-properties)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
