---
title: How to publish vue3 typescript component with vite on NPM
author: Youngjin Kwak
date: 2022-06-02 12:05:00 +0800
categories: [Vue3, Typescript, Skills, 'vite', 'npm']
tags: [vue3, typescript, skill, 'vite', 'npm']
---

# Let's create component
## Step 1 - Start new project with vite
Here is the official vite website <a href="https://vitejs.dev/guide/">link</a>
```
yarn create vite [project-name] --template vue-ts
```
My post will use typescript, so you have to use "vue-ts" <br>

## Step 2 - Make empty main.ts, change the name, and make a code.
Change the main.ts to index.ts (if you keep the name main.ts, you can do it. Just change index.ts to main.ts in vite config later) <br>
```
// index.ts (main.ts)

import [your component name] from './App.vue'

export default [your component name]
```

## Step 3 - Write down
``` vue
<template>
  <div
    :style="{
      height: height,
      width: width,
    }"
  >
    test
  </div>
</template>
<script setup lang="ts">
const props = defineProps({
  height: {
    type: String,
    required: false,
    default: '600px',
  },
  width: {
    type: String,
    required: false,
    default: '1024px',
  },
})
</script>
```

# Testing before publish
## In component project
```
npm link
```

## In new project
Create new project for testing locally with same way used to start component project. <br>
In new project, type following code.
```
npm link [project-name]
```
From now on, you can test your component in new project. <br>
In local test, you can't see any type of component. However when you publish you will be able to see types.

# Publish
## Step 1 - Build
Before you publish you have change vite.config.ts, package.json

### vite.config.ts
You have to download "rollup-plugin-typescript2" (<a href="https://www.npmjs.com/package/rollup-plugin-typescript2">link</a>) to generate types for your .vue file <br>
You also have to change build option. Look at this <a href="https://vitejs.dev/guide/build.html#library-mode">link</a>.
```typescript
import { defineConfig } from 'vite'
import * as path from 'path'
import vue from '@vitejs/plugin-vue'
import typescript2 from 'rollup-plugin-typescript2'
import { fileURLToPath } from 'url'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    // Generate types for components
    typescript2({
      check: false,
      include: ['src/**/*.vue'],
      tsconfigOverride: {
        compilerOptions: {
          sourceMap: true,
          declaration: true,
          declarationMap: true,
        }
      },
      exclude: [
        'vite.config.ts'
      ]
    })
  ],
  build: {
    cssCodeSplit: false,
    lib: {
      entry: path.resolve(__dirname, 'src/index.ts'), // or main.ts
      name: [projectName],
      fileName: (format) => `[project-name].${format}.js`
    },
    rollupOptions: {
      // make sure to externalize deps that shouldn't be bundled
      // into your library
      external: ['vue'],
      output: {
        // Provide global variables to use in the UMD build
        // for externalized deps
        globals: {
          vue: 'Vue'
        }
      }
    }
  },
})
```
Change all "[project-name]" and [projectName] to your custom name

### Package.json
```
{
...
  "name": [project-name],
  "files": [
    "dist"
  ],
  "version": [version],
  "author": [author],
  "description": [description],
  "repository": [repository link],
  "license": "MIT",
  "main": "./dist/[project-name].umd.js",
  "module": "./dist/[project-name].es.js",
  "types": "./dist/App.vue.d.ts",
  "exports": {
    ".": {
      "import": "./dist/[project-name].es.js",
      "require": "./dist/[project-name].umd.js"
    },
    "./dist/style.css": "./dist/style.css",
    "./dist/index.d.ts": "./dist/index.d.ts"
  },
  ...
}
```
#### Note
- Change all "[project-name]" to your custom name <br>
- Name must be unique, this means your project name must not be published on NPM.
- If you don't have github Repository, repository link can be empty.

After you change vite.config.ts and package.json, build your code!
```
yarn build
```
After build, you can get at least App.vue.d.ts, es.js, and umd.js file.

## Step 2 - Publish!
### Login to NPM
```
npm login
```
#### Note
If you don't have account, please sign up NPM first

### Publish
```
npm publish
```
### Note
Whenever you publish, change the version in package.json.

# Conclusion
After you are success to publish, check the TS mark on the top.

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
