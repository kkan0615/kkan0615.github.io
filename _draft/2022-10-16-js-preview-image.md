---
title: Javascript how to preview image without server
author: Youngjin Kwak
date: 2022-10-16 12:21:00 +0800
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
In this article, I am going to show how to preview an image without server. I also show sample codes for Vue3 and React.

Press following website link to watch live preview.
[playcode.io](https://playcode.io/)
[stackblitz with react](https://stackblitz.com/edit/react-hooks-demo-acd7xr?file=index.js)
[vue3 srf playground](https://sfc.vuejs.org/#eNo9j71uwzAMhF+F5eIWqCV0NZQA3foGXbikjpw40B9EOR0EvXspp8imu9N9OFb8TEndN4sTGp7zmgqwLVs6Ulh9irlAhWwXaLDk6GGQrwMFCnMMXMDzBQ49fx2+rHMRvmN255fhjYLRD5yARBTrkzsVKwrAXD+Ote7l1owWtbtrSFuB++jj2boDoeSEEhn9bOM7PlaN/pTUjWOQ3bW36T9gwgl2p3uytmvCaymJJ615mfu1N1YxX7S8VN5CWb1Vlv34k+Mv2yxgwo5oFBq2P3/sZE8=)

# Vanilla JS
## Use createObjectURL()
```createObjectURL()``` take a file, blob or MediaSource object to create object URL.
It returns a string containing an object URL that can be used to reference the contents of the specified source .
Ex) ```blob:https://preview-javascript.playcode.io/bec63a00-4355-48de-a4f8-533f26b7e6f9```

```html
<input id="input-image" type="file" accept="image/*" >
<img id="preview-image">
```
```javascript
const inputImageElement = document.getElementById('input-image')

inputImageElement.onchange = (event) => {
  // Get First file
  const [file] = inputImageElement.files
  // Find the preview image
  const imagePreviewElement = document.getElementById('preview-image')
  if (imagePreviewElement && file) {
    // Create object Url
    imagePreviewElement.src = URL.createObjectURL(file)
  }
}
```
## Use FileReader()
```FileReader``` is object for reading File or blob asynchronously.
```FileReader``` contains many instance reading methods.
In this case, we are going to use ```readAsDataURL()``` which change file to DataUrl
```html
<input id="input-image" type="file" accept="image/*" >
<img id="preview-image">
```
We are going to use same HTML that we used in ```createObjectURL()```
```javascript
const reader = new FileReader()
reader.onload = function(){
  const output = document.getElementById('preview-image');
  output.src = reader.result;
}
reader.readAsDataURL(event.target.files[0])
```
# Vue 3 version
```vue
<script setup>
import { ref, computed, onBeforeUnmount } from 'vue'

const file = ref()
const src = ref('')

onBeforeUnmount(() => {
  if(file.value) {
    URL.revokeObjectURL(file.value)
    src.value = ''
  }
})

const onChangeImageInput = (event) => {
  const newFile = event.target.files[0]
  if(file.value) {
    URL.revokeObjectURL(file.value)
    src.value = ''
  }
  file.value = newFile
  src.value = URL.createObjectURL(newFile)
}
</script>
<template>
  <input type="file" accept="image/*" @change="onChangeImageInput">
  <img
    v-if="src"
    :src="src"
    alt="preview-image"
  >
</template>
```
### Note
- It is required to free memory before unmount component

# React version
```jsx
import React, { memo, useCallback, useState, useEffect } from 'react'
import { render } from 'react-dom'

const App = () => {
  const [file, setFile] = useState()
  const [src, setSrc] = useState('')

  useEffect(() => {
    // create the preview
    if(file) {
      setSrc(URL.createObjectURL(file))
    }

    // free memory when ever this component is unmounted
    return () => URL.revokeObjectURL(file)
  }, [file]);

  const handleChangeImageInput = (event) => {
    setFile(event.target.files[0]);
  };

  return (
    <div>
      <input type="file" accept="image/*" onChange={handleChangeImageInput} />
      {src && <img src={src} alt="preview-image" />}
    </div>
  );
};

render(<App />, document.getElementById('root'));
```
### Note
- It is required to free memory before unmount component

# Ref
- [MDN - URL.createObjectURL()](https://developer.mozilla.org/en-US/docs/Web/API/URL/createObjectURL)
- [MDN - FileReader](https://developer.mozilla.org/en-US/docs/Web/API/FileReader)
- [FileReader](https://www.javascripture.com/FileReader)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
