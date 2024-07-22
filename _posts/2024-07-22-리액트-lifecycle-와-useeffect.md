---
layout: post
title: 리액트 lifecycle 와 useEffect
date: 2024-07-22 23:43 +0900
description: 리액트 lifecycle 와 useEffect에 대해서 알아보자!
category: [프론트엔드,study]
tags: [react]
image:
  path: https://github.com/user-attachments/assets/d678ff80-375a-4b4b-b047-48d8047df52d
  alt: 'lifecycle'
pin: true
math: true
mermaid: true
author: sbs1253
---
# 리액트 lifecycle 와 useEffect

오늘은 리액트 lifecycle 와 useEffect가 어떤 기능을 해주는지 알아보도록 하겠습니다.

### 리액트의 라이프 사이클

![lifecycle](https://github.com/user-attachments/assets/d678ff80-375a-4b4b-b047-48d8047df52d)

이 사진을 보면 리액트의 라이프 사이클이 나와있는데 간단하게 3가지 순서라고 보면 된다.  

- 생성될 때 : class로 생각하면 constructor라고 생각하면 된다. 초깃값 설정 부분이다.  
- 업데이트할 때 : useState를 사용해서 업데이트가 되거나 render가 될 때를 말한다.  
- 제거할 때 : 어떠한 이유로 컴포넌트가 제거될 때를 말한다.

### useEffect는 어떤 역할을?

리액트 함수형 컴포넌트에서는  `componentDidMount` `componentDidUpdate`  `componentWillUnmount`를 사용하지 못한다.
그 역할을 하는 게 useEffect이다. 간단한 예시를 들어보자면

#### componentDidMount

``` jsx
useEffect(() => {
console.log('componentDidMount일 때 실행합니다.');
}, []);
```
이렇게 useEffect 함수를 실행할 때 `[]` 의존성 배열을 주지 않으면 처음 렌더링 될 때 실행되는 `componentDidMount`처럼 작동한다.  
  
그렇게 되면 컴포넌트가 render 되고 useEffect가 실행되므로 API 호출할 때 유용하게 사용이 가능하다. 자세한 건 다음 포스팅에서 다루겠다!

#### componentDidUpdate

``` jsx
const [count, setCount] =  useState(0);

useEffect(() => {
console.log('componentDidUpdate일 때 실행합니다.',data);
setData(count+1)
}, [count]);
```
이 코드에선 의존성 배열로 `data`값을 전달한다. 이렇게 되면 초기 실행 후 `data`값이 변할 때 useEffect가 다시 실행되어 값이 업데이트가 된다.

#### componentWillUnmount

``` jsx
useEffect(() => {
console.log('componentDidMount일 때 실행합니다.');
return () => { console.log('Component will unmount'); };
}, []);
```
이 코드를 보면 함수를 return 하는데 컴포넌트가 제거될 때 componentWillUnmount처럼 실행되게 된다.

### 총 정리

``` jsx
  const [count, setCount] = useState(0);

  useEffect(() => {
    // 이 부분은 컴포넌트가 마운트되거나 count가 업데이트될 때 실행됩니다.
    console.log('Component mounted or updated with count:', count);

    // 반환된 함수는 다음 의존성 값이 변경되기 직전이나 컴포넌트가 언마운트될 때 실행됩니다.
    return () => {
      console.log('Cleaning up after count:', count);
    };
  }, [count]); // count가 변경될 때마다 useEffect가 실행됩니다.
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

```

**버튼 클릭 전 (`count = 0`)**

- `console.log('Component mounted or updated with count:', 0);` 실행
- console에 `Count: 0`이 표시됨

**버튼 클릭 (setCount(1))**

- `count`가 변경되기 **직전에** 정리 함수가 실행
- `console.log('Cleaning up after count:', 0);`
- `count`가 1로 업데이트됨
- 새로운 `count` 값에 대해 `useEffect`의 첫 번째 함수 부분이 실행됨
- `console.log('Component mounted or updated with count:', 1);`
- console에 `Count: 1`이 표시됨

![예시](https://github.com/user-attachments/assets/392e32e0-fe86-4a25-add8-4b7fffcfabc8)
