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

# 왜 "&&"을 사용하지 말아야 할까?
사실은 "&&" 를 사용해도 좋습니다. "무조건" 사용하지 말라는 뜻은 아닙니다. 하지만 이는 condition이 확실하게 ```true``` 혹은 ```false```인 boolean 으로 나올 수 있을 때의 이야기입니다.
만약에 condition이 boolean이 아닌 ```null``` 혹은 ```undefined```라면 어떤 결과가 나올까요? 결론 부터 말씀을 드리면 **"ERROR"** 가 나옵니다

## 예시
3 가지 예시와 결과를 알아 볼 것입니다.
### 만약 condition이  ```true```, ```false```일 경우
Component가 정상적으로 Rendering 됩니다.
### 만약 condition이 ```0```일 경우
UI가 정상적으로 Rendering 됩니다. 그러나 우리가 보고싶던 Component 가 아닌 0이 보일 것입니다.
### 만약 condition이 ```undefined``` 일 경우
```error: "Uncaught Error: Error(...): Nothing was returned from render.``` 문구가 console 창에 찍히게 됩니다.
이는 명백히 Return statment가 없거나, 아무것도 Rendering하지 않을 때 나타납니다.

# 해결책 및 다른 방법
이 문제를 해결하기위한 다른 방법으로는 ```?```을 사용한 삼항 연산자가 있습니다.
```tsx
interface Prop {
  condition: boolean
}

const MyComponent = ({ condition }: Prop) => {

  return (
    <div>
      <h1>Condition</h1>
      { condition ? <SomeComponent /> : null }
    </div>
  );
}
```
## 코드 간단 설명
condition이 ```true``` 일 경우 Rendering 하는 접근법 자체는 같습니다. 하지만 삼항 연사를 사용 했으며 만약 ```false``` 일 경우 ```null``` 을 반환하도록 명백히 표현한 것이 다릅니다.
하지만 삼항 연사는 "&&" 과 달리 코드가 길어지는 단점을 지니고 있습니다.

# Ref
[Stop Using “&&” for Conditional Rendering in React - Jakub Kozak](https://medium.com/geekculture/stop-using-for-conditional-rendering-in-react-a0f7b96200f8)
[Why You Should Stop Using the && Operator in React... - Eric Murphy]('https://www.youtube.com/watch?v=muqFuBGNmLk&ab_channel=EricMurphy)

# Support
[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/youngjinkwak)
