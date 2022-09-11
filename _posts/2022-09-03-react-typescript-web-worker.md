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
The web worker is used for preventing to stop website because of heavy task in stack

# Sample code
Unfortunately, developers can not use web worker made by ts file directly unlike when they use web worker made by js file, so they are required to change
the code to blob data and blob to url
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
- buildWorkerScript is for creating the code to objectUrl. we will discuss more at next step
- postMessage() function is used for sending the data to page

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
### Note
- Take function code as parameter
- Change code in file to Blob
- Generate url in order to use it as Worker's url

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
- postMessage() function in page sends message to background (worker).
- Because of builder, the developers can just import file and put in the Worker class constructor parameter.

# Refs
- https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers
- https://codecompiled.com/web-workers-in-html5
- https://stackoverflow.com/questions/60695105/how-to-use-webworkers-in-react-using-typescript
- https://blog.johnnyreilly.com/2020/02/21/web-workers-comlink-typescript-and-react

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
