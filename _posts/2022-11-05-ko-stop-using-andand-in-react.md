---
title: React에서 조건문으로 랜더링시 "&&" 사용하지 맙시다.
author: Youngjin Kwak
date: 2022-11-05 15:30:00 +0800
categories: [korean, react]
tags: [javascript]
image:
  path: ../images/react-logo.png
  width: 800
  height: 500
  alt: react-logo.
---
---
# Overview
React 내에서 조건적으로 Rendering 하는 방법은 많습니다. 그중에서 이 포스팅은 "&&"을 이용한 조건 Rendering 에 관한 이야기를 할 것입니다.
"&&" 을 사용하여 Rendering 할 경우 코드는 가독성은 좋지만, 가끔 UI 버그를 유발하는 경우가 있습니다.
그래서 이 포스팅은 왜 "&&" 을 사용하지 말아야하는 것과 사용 하더라도 어떻게 잘 사용해야 할까에 대한 내용을 담고 있습니다.

# "&&" React 내에서 사용하는 법
```tsx
interface Prop {
  condition: boolean
}

const MyComponent = ({ condition }: Prop) => {

  return (
    <div>
      <h1>Condition</h1>
      { condition && <SomeComponent /> }
    </div>
  );
}
```
## 코드 간단 설명
- 만약 condition variable 이 ```true``` 일 경우, ```<SomeComponent />```을 Rendering 합니다.
- 만약 condition variable 이 ```false``` 일 경우, ```<SomeComponent />```을 Rendering 하지 않습니다.

## 무엇이 문제 일까?
코드만 보면 문제가 될 것이 없어 보입니다. "&&" 은 리엑트에서 정의 된 것도 아닌 자바스크립트 문법중 하나이며
실제로 ```if``` 조건 문에 ```AND```를 표현하기위해 자주 사용됩니다.

# Ref

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
