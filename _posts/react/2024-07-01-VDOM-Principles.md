---
layout: post
title: VirtualDOM 이란?
date: 2024-07-01 11:00 +0900
description: REACT
image: ../assets/img/react2.png
category: REACT
tags: REACT
published: true
sitemap: true
---

안녕하세요! 오늘은 Virtual DOM의 작동 원리를 알아보겠습니다!

---

# Virtual DOM의 작동 원리

## 개요

Virtual DOM(가상 DOM)은 UI의 효율적인 렌더링을 위해 고안된 기술로, 실제 DOM을 직접 조작하는 대신 UI의 가상 표현을 메모리에 두고 이를 통해 실제 DOM과 동기화합니다. 이 글에서는 Virtual DOM의 작동 원리에 대해 자세히 설명합니다.

## Virtual DOM의 개념

Virtual DOM은 실제 DOM의 가상 표현으로, 브라우저가 직접 접근하지 않는 메모리 내의 구조체입니다. 이를 통해 UI 상태의 변경을 추적하고, 변경된 부분만을 실제 DOM에 반영함으로써 성능을 최적화합니다.

## 작동 원리

### 1. 초기 렌더링

애플리케이션이 처음 로드될 때, Virtual DOM 트리가 생성됩니다. 이 트리는 실제 DOM과 동일한 구조를 가지며, 메모리 내에서 유지됩니다. 초기 렌더링 시에는 전체 UI가 Virtual DOM 트리에 반영되고, 이를 기반으로 실제 DOM이 생성됩니다.

### 2. 상태 변경 감지

애플리케이션의 상태가 변경되면, 새로운 Virtual DOM 트리가 생성됩니다. 이 새로운 트리는 변경된 상태를 반영하며, 이전의 Virtual DOM 트리와 비교(differencing)하는 과정이 시작됩니다.

### 3. Diffing 알고리즘

diffing 알고리즘은 이전 Virtual DOM 트리와 새로운 Virtual DOM 트리를 비교하여 변경된 부분을 찾아냅니다. 이 과정은 다음과 같은 단계로 이루어집니다:

- **노드 비교**: 각 노드를 순회하며, 태그 이름, 속성, 자식 노드 등을 비교합니다.
- **변경 감지**: 변경된 노드를 찾고, 추가, 수정, 삭제된 노드를 기록합니다.
- **최소 변경 계산**: 실제 DOM에 최소한의 변경만을 적용하기 위해, 변경 사항을 최적화합니다.

### 4. 패칭(Patching)

diffing 알고리즘을 통해 변경된 부분이 감지되면, 실제 DOM에 이를 반영하는 패칭 과정이 시작됩니다. 패칭은 다음과 같은 단계로 이루어집니다:

- **삽입**: 새로 추가된 노드를 실제 DOM에 삽입합니다.
- **삭제**: 제거된 노드를 실제 DOM에서 삭제합니다.
- **수정**: 변경된 속성이나 내용을 실제 DOM에 업데이트합니다.

이 과정은 최소한의 연산으로 실제 DOM을 업데이트하여 성능을 극대화합니다.

## 예제 코드

React를 사용하여 Virtual DOM의 작동 원리를 이해할 수 있는 간단한 예제를 살펴보겠습니다:

```jsx
import React, { useState } from "react";

function TodoList() {
  const [todos, setTodos] = useState(["할 일 1", "할 일 2"]);

  const addTodo = () => {
    setTodos([...todos, `할 일 ${todos.length + 1}`]);
  };

  return (
    <div>
      <h1>할 일 목록</h1>
      <ul>
        {todos.map((todo, index) => (
          <li key={index}>{todo}</li>
        ))}
      </ul>
      <button onClick={addTodo}>할 일 추가</button>
    </div>
  );
}

export default TodoList;
```

이 예제에서, `useState` 훅을 사용하여 상태를 관리합니다. 할 일 목록이 변경될 때마다 새로운 Virtual DOM 트리가 생성되고, 이전 트리와 비교하여 변경된 부분만을 실제 DOM에 반영합니다.

## 결론

Virtual DOM은 UI의 효율적인 렌더링을 위해 필수적인 기술입니다.
메모리 내의 가상 표현을 통해 상태 변화를 추적하고, 실제 DOM과 동기화하는 과정을 통해 성능을 최적화합니다. 앞으로도 다양한 프레임워크와 라이브러리에서 Virtual DOM을 활용한 최적화 기술이 발전할 것입니다.
