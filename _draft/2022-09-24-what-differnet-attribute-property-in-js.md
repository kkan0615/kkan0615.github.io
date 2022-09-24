---
title: What is different attribute and property in javascript
author: Youngjin Kwak
date: 2022-09-17 18:21:00 +0800
categories: [javascript, html]
tags: [javascript, html]
image:
  path: ../images/javascript-logo.jpeg
  width: 800
  height: 500
  alt: javascript-logo.
---
---
# What is "property"?
JS DOM objects contain dozens of properties like accept, checked, classList, className, etc.
The properties may be different by DOM objects.

## How to get property
```html
<a id="home-link" href="/" class="link">home</a>
```
```javascript
console.log(link.classList) // { 0: "link" }
console.log(link.className) // "link"
```


# See more with code
Let's consider that there is following html element in your project.
```html
<input type="text" value="Name:">
```
In input html element, there are two attributes. One is ```type```. The other one is ```value```
Once the browser parses this code, a ```HTMLInputElement``` object will be created.

# Ref
(https://stackoverflow.com/questions/6003819/what-is-the-difference-between-properties-and-attributes-in-html)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
