---
layout: post
title: 리액트 useState와 StrictMode
date: 2024-07-11 00:02 +0900
description: useState 작동원리와 StrictMode 사용 이유
category: [프론트엔드,study]
tags: [react]
pin: true
math: true
mermaid: true
author: sbs1253
---

# React useState와 클로저

React의 `useState`는 상태(state)를 관리하기 위한 훅(hook)이다. 이 훅은 클로저를 사용하여 상태를 업데이트하고 유지한다.

### useState 동작 방식

1. `useState`를 호출하여 상태 변수를 선언한다.
2. 초기 상태값을 인자로 전달한다.
3. 상태값과 상태를 갱신하는 함수를 반환한다.

```jsx
const [count, setCount] = useState(0);
```

### 클로저와 상태 관리

React는 `useState`를 사용할 때 클로저를 사용하여 상태값을 캡처하고 유지한다. 다음과 같이 동작한다.

- `useState` 호출 시 초기 상태값을 내부 변수에 저장한다.
- 상태값을 변경하는 함수(`setCount`)는 클로저를 통해 이 변수에 접근하여 값을 갱신한다.
- 상태가 변경될 때마다 컴포넌트가 다시 렌더링되며 최신 상태값을 사용한다.

----------

# React.StrictMode와 console.log 두 번 출력

### React.StrictMode의 동작 방식

`React.StrictMode`는 개발 중 더 엄격한 검사와 경고를 제공하기 위한 도구다. 이를 사용하면 특정 메서드와 라이프사이클 메서드가 두 번 호출된다. 이로 인해 `console.log`가 두 번 출력되는 현상이 발생한다.

```jsx

import React from  'react';
import ReactDOM from  'react-dom/client';

function App() {
  console.log('App rendered');
  return <div>Hello, world!</div>;
}

ReactDOM.createRoot(document.getElementById('root')).render(
 <React.StrictMode>
  <App  />
 </React.StrictMode>
);

```

### 컴포넌트가 두 번 렌더링되는 이유

- **의도적인 부작용 검출:** 초기 렌더링과 상태 업데이트 시 발생할 수 있는 부작용을 감지하기 위해 컴포넌트를 두 번 렌더링한다.
- **개발 편의성 향상:** 불필요한 부작용을 미리 찾아내어 안정성을 높인다.

----------

# 변수 값이 변하지 않는 이유와 useState의 역할

### 일반 변수 vs. useState

1. **일반 변수:** 컴포넌트 함수가 다시 호출될 때마다 초기화된다. 상태를 유지하지 않는다.
2. **useState 사용 시:** 상태가 유지되며, 컴포넌트가 다시 렌더링될 때 상태값을 재사용한다.

```jsx
 function App() {
   let count = 0;
   const [counter, setCounter] = useState(0);
   const increase = () => {
     count += 1;
     setCounter(counter+1);
   };
 }
```

### 상태값 변경과 렌더링

- **상태값 변경:** `useState`의 상태 변경 함수(`setCount`)를 호출하여 상태를 갱신한다.
- **렌더링:** 상태가 변경되면 React는 컴포넌트를 다시 렌더링하여 최신 상태값을 반영한다.
- **지연 적용:** 상태 변경은 비동기적으로 처리되며, 다음 렌더링 사이클에서 적용된다.
