---
title: React typescript web worker
author: Youngjin Kwak
date: 2022-09-03 13:21:00 +0800
categories: [typescript, react]
tags: [typescript, react]
image:
  path: ../images/react-logo.png
  width: 800
  height: 500
  alt: react-logo.
---
# What is web worker
The web worker is for web content to run scripts in background thread. The web worker allows developer to use multithreading in Web.
The web worker also prevents stopping website because of heavy task in stack

# Sample code
The developers can not use web worker made by ts file directly unlike when they use web worker made by js file, so they are required to change
blob data
## Step 1 - web worker
```typescript
// webworker.ts
const workerCode = () => {
  onmessage = (e: MessageEvent) => {
    postMessage('Send message', e.data)
  }
}
const worker = buildWorkerScript(workerCode)

export default worker
```
### Note
- buildWorkerScript is function that creates objectUrl, you can see the code at next step
- postMessage() function sends data to page

## Step 2 - buildWorkerScript
```typescript
// builder.ts
export const buildWorkerScript = (workerCode: () => void) => {
  // create code to string
  let code = workerCode.toString()
  // make block
  code = code.substring(code.indexOf('{') + 1, code.lastIndexOf('}'))
  // Change to blob data
  const blob = new Blob([code], { type: 'application/javascript' })
  // create object url
  return URL.createObjectURL(blob)
}
```

## Step 3 - react page
```tsx
import worker from 'path/to/exportData'
// web worker instance
let webWorker: Worker | null = new Worker(worker)

useEffect(() => {
  if (webWorker) {
    // Receive message
    webWorker.onmessage = (msg: MessageEvent) => {
      console.log('Get message from background: ', msg.data)
    }
    // Get error
    webWorker.onerror = () => {
      console.log('Error')
    }
    // Start process
    webWorker.postMessage('start background process')
  }

  return (() => {
    // Destory web worker instance
    if (webWorker) {
      webWorker.terminate()
      webWorker = null
    }
  })
}, [])
```
### Note
- Because of builder, the developers can just import file and put in the Worker class constructor parameter

# Refs
- https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers
- https://codecompiled.com/web-workers-in-html5
- https://stackoverflow.com/questions/60695105/how-to-use-webworkers-in-react-using-typescript
- https://blog.johnnyreilly.com/2020/02/21/web-workers-comlink-typescript-and-react

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
