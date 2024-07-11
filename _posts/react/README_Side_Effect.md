---
layout: post
title: Side-Effect
date: 2024-07-08 11:00 +0900
description: REACT
image: ../assets/img/react2.png
category: REACT
tags: REACT
published: true
sitemap: true
---

# Side-Effect

## Side-Effect란?

Side-Effect(부작용)는 함수가 실행되면서 함수 외부에 존재하는 값이나 상태를 변경시키는 행위를 말합니다. 이는 함수형 프로그래밍에서 피해야 할 사항 중 하나로, 함수의 예측 가능성을 떨어뜨리고 디버깅을 어렵게 만듭니다.

### 예시

다음은 Side-Effect를 포함하는 함수의 예시입니다.

```javascript
let globalValue = 0;

function incrementGlobalValue() {
  globalValue += 1; // globalValue를 변경하는 Side-Effect 발생
}

incrementGlobalValue();
console.log(globalValue); // 1
```

위 예시에서 `incrementGlobalValue` 함수는 전역 변수 `globalValue`의 값을 변경하는 Side-Effect를 가지고 있습니다.

## React에서의 Side-Effect

React에서는 컴포넌트의 렌더링 과정에서 Side-Effect를 처리하기 위해 `useEffect` 훅을 제공합니다. `useEffect` 훅은 함수 컴포넌트 내에서 부작용을 수행할 수 있게 합니다.

### useEffect 사용 예시

다음은 React 컴포넌트에서 `useEffect`를 사용하는 예시입니다.

```javascript
import React, { useState, useEffect } from "react";

function ExampleComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`; // Side-Effect: document.title 변경

    // Clean-up 함수 반환
    return () => {
      document.title = "React App";
    };
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

위 예시에서 `useEffect` 훅은 `count` 값이 변경될 때마다 실행되어 `document.title`을 업데이트합니다. 또한 컴포넌트가 언마운트될 때 또는 `count` 값이 변경되기 직전에 clean-up 함수를 호출하여 제목을 초기 상태로 복원합니다.

## useEffect의 기본 구조

`useEffect` 훅은 다음과 같은 기본 구조를 가집니다.

```javascript
useEffect(() => {
    // Side-Effect 코드

    return () => {
        // Clean-up 코드
    };
}, [의존성 배열]);
```

- 첫 번째 매개변수는 실행할 Side-Effect 코드입니다.
- 두 번째 매개변수는 의존성 배열로, 이 배열에 포함된 값이 변경될 때마다 Side-Effect가 실행됩니다. 이 배열이 비어 있으면 컴포넌트가 마운트될 때 한 번만 실행됩니다.

## Side-Effect를 피하는 방법

Side-Effect를 피하기 위해 함수형 프로그래밍에서는 다음과 같은 방법을 사용할 수 있습니다.

1. **불변성 유지**: 함수 내에서 외부 상태를 변경하지 않고, 새로운 값을 반환합니다.

```javascript
const add = (a, b) => a + b; // 외부 상태를 변경하지 않음
```

2. **순수 함수 작성**: 동일한 입력에 대해 항상 동일한 출력을 반환하는 함수를 작성합니다.

```javascript
let counter = 0;

function pureIncrement(value) {
  return value + 1; // 외부 상태를 변경하지 않음
}

counter = pureIncrement(counter);
console.log(counter); // 1
```

3. **useEffect 활용**: React 컴포넌트에서 Side-Effect를 처리할 때는 `useEffect` 훅을 사용하여 부작용을 격리합니다.

## 결론

Side-Effect는 함수의 외부 상태를 변경하는 행위로, 예측 가능성을 떨어뜨리고 디버깅을 어렵게 만듭니다. React에서는 `useEffect` 훅을 사용하여 Side-Effect를 관리할 수 있습니다. 함수형 프로그래밍에서는 불변성을 유지하고 순수 함수를 작성하여 Side-Effect를 피할 수 있습니다. 이러한 원칙들을 잘 활용하여 안정적이고 유지보수하기 쉬운 코드를 작성해 보세요.
