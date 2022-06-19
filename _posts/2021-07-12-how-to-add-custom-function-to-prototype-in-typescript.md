---
title: How to add custom function to prototype with typescript
author: Youngjin Kwak
date: 2021-07-12 20:56:00 +0800
categories: [Typescript, Skills]
tags: [typescript, skill]
---

# Overview
This example is tested on vue + typescript. However, it's not big different with others.

## Step 1 - Create .ts file
Create typescript file. In the example, <mark>array.ts</mark> is created

## Step 2 - Dive into code
```typescript
interface Array<T> {
  removeOne(o: T): Array<T>
}

if (typeof Array.prototype.removeOne !== 'function') {
  /**
   * Remove target data
   * @param o - target data
   * @return Spliced Array
   */
  Array.prototype.removeOne = function (o) {
    return this.splice(this.indexOf(o), 1)
  }
}
```
#### Exchange to javascript
```javascript
  Array.prototype.removeOne = function (o) {
    return this.splice(this.indexOf(o), 1)
  }
```

You have to use function instead of the arrow function to use "this" in the function. This points out target array

## Step 3 - import to your index
import the file to your main or index file. In the example, i imported to main.ts
```typescript
// ...
/* Utils prototype */
import '@/utils/array'
// ...
```

## Step 4 - use them!
If you can search on IDE intelligence, you are success to access!
```typescript
// Just use without any import!
[1,2,3].removeOne(2)
```

# Conclusion
If you follow all the steps well, you can
