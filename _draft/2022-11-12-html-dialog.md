---
title: HTML Tag "dialog" with react
author: Youngjin Kwak
date: 2022-09-17 18:21:00 +0800
categories: [react]
tags: [react, html, javascript]
image:
  path: ../images/javascript-logo.jpeg
  width: 800
  height: 500
  alt: javascript-logo.
---
---
# Overview

# Open Dialog
Add ```open``` attribute to open a modal If no ```open```, it means modal is closed
```html
<dialog open>
  Dialog content
</dialog>
```

# JavaScript API for handling Dialog
```html
<button onclick="window.dialog.show();">open dialog</button>

<dialog id="dialog">
  Dialog content
  <button onclick="window.dialog.close();">close</button>
</dialog>
```

# Ref
- [dialog: The Dialog element - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dialog)
- [Some Hands-On with the HTML Dialog Element - Chris Coyier](https://css-tricks.com/some-hands-on-with-the-html-dialog-element/)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
