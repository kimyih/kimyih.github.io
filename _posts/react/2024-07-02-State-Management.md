---
layout: post
title: 상태 관리 라이브러리란?
date: 2024-07-02 11:00 +0900
description: REACT
image: ../assets/img/react2.png
category: REACT
tags: REACT
published: true
sitemap: true
---

안녕하세요! 오늘은 **상태 관리 라이브러리** 에 대해 알아보겠습니다!

---

# ☑️ 상태 관리 라이브러리

## 개요

상태 관리 라이브러리는 리액트와 같은 프론트엔드 프레임워크에서 유동적인 데이터를 담는 변수인 State를 전역적으로 관리하는 툴입니다. 이 글에서는 상태 관리 라이브러리가 무엇인지, 왜 필요한지, 그리고 주요 상태 관리 라이브러리에 대해 자세히 알아보겠습니다.

## 상태 관리 라이브러리란?

상태 관리 라이브러리는 애플리케이션의 상태를 일관되게 관리하고, 여러 컴포넌트 간의 상태 공유를 용이하게 하는 도구입니다. 리액트에서는 컴포넌트별로 지역적인 state를 사용할 수 있지만, 복잡한 애플리케이션에서는 전역 상태 관리가 필요합니다. 이를 위해 Redux, MobX, Context API 등 다양한 상태 관리 라이브러리가 존재합니다.

## 왜 상태 관리 라이브러리가 필요한가?

상태 관리 라이브러리는 다음과 같은 이유로 필요합니다:

1. **전역 상태 관리**: 애플리케이션의 여러 컴포넌트가 동일한 상태를 공유할 때, 전역 상태 관리가 필요합니다. 지역적인 state는 컴포넌트 간 상태 공유가 어려워질 수 있습니다.
2. **일관성 유지**: 상태 관리 라이브러리는 상태의 일관성을 유지하여 예측 가능한 동작을 보장합니다. 이는 디버깅과 유지보수를 용이하게 합니다.
3. **코드 구조 개선**: 전역 상태 관리 도구를 사용하면, 코드 구조를 개선하고, 상태 관리 로직을 중앙 집중화할 수 있습니다.

## 주요 상태 관리 라이브러리

### 1. Redux

Redux는 가장 널리 사용되는 상태 관리 라이브러리 중 하나로, 단일 스토어를 사용하여 상태를 관리합니다. 상태는 불변성을 유지하며, 상태 변경은 오직 액션을 통해서만 가능합니다. Redux의 주요 개념은 다음과 같습니다:

- **스토어(Store)**: 애플리케이션의 모든 상태를 담고 있는 객체입니다.
- **액션(Action)**: 상태 변경을 나타내는 객체로, type과 payload를 포함합니다.
- **리듀서(Reducer)**: 액션을 받아 상태를 변경하는 순수 함수입니다.

### 2. MobX

MobX는 반응형 상태 관리 라이브러리로, 상태가 변경되면 자동으로 관련 컴포넌트가 업데이트됩니다. MobX는 관찰 가능한 상태(observable state)를 사용하여 상태 변화를 추적합니다. 주요 개념은 다음과 같습니다:

- **Observable**: 상태를 관찰 가능한 객체로 만듭니다.
- **Action**: 상태 변경 로직을 포함하는 메서드입니다.
- **Reaction**: 상태가 변경될 때 실행되는 반응형 함수입니다.

### 3. Context API

리액트의 Context API는 경량 상태 관리 도구로, 전역 상태를 관리할 수 있습니다. Context API는 주로 간단한 애플리케이션에서 사용되며, 주요 개념은 다음과 같습니다:

- **Context**: 전역 상태를 담는 객체입니다.
- **Provider**: Context를 컴포넌트 트리에 제공하는 컴포넌트입니다.
- **Consumer**: Context를 구독하여 상태를 사용하는 컴포넌트입니다.

## 예제 코드

아래는 Redux를 사용한 간단한 상태 관리 예제입니다:

```jsx
import { createStore } from "redux"; // Redux의 createStore 함수를 임포트하여 스토어를 생성합니다.
import { Provider, useDispatch, useSelector } from "react-redux"; // React-Redux에서 제공하는 Provider, useDispatch, useSelector 훅을 임포트합니다.

// 액션 타입 정의
const INCREMENT = "INCREMENT"; // 카운트를 증가시키는 액션 타입을 정의합니다.
const DECREMENT = "DECREMENT"; // 카운트를 감소시키는 액션 타입을 정의합니다.

// 액션 생성자
const increment = () => ({ type: INCREMENT }); // INCREMENT 액션 객체를 반환하는 액션 생성자 함수입니다.
const decrement = () => ({ type: DECREMENT }); // DECREMENT 액션 객체를 반환하는 액션 생성자 함수입니다.

// 리듀서
const counter = (state = 0, action) => {
  // 초기 상태를 0으로 설정한 counter 리듀서 함수입니다.
  switch (
    action.type // 액션 타입에 따라 상태를 업데이트합니다.
  ) {
    case INCREMENT: // INCREMENT 액션이 발생하면
      return state + 1; // 상태를 1 증가시킵니다.
    case DECREMENT: // DECREMENT 액션이 발생하면
      return state - 1; // 상태를 1 감소시킵니다.
    default: // 다른 액션 타입이 발생하면
      return state; // 상태를 변경하지 않고 그대로 반환합니다.
  }
};

// 스토어 생성
const store = createStore(counter); // counter 리듀서를 사용하여 Redux 스토어를 생성합니다.

function Counter() {
  const count = useSelector((state) => state); // useSelector 훅을 사용하여 현재 상태를 조회합니다.
  const dispatch = useDispatch(); // useDispatch 훅을 사용하여 액션을 디스패치할 함수를 가져옵니다.

  return (
    <div>
      <p>카운트: {count}</p> // 현재 카운트를 출력합니다.
      <button onClick={() => dispatch(increment())}>증가</button> // 클릭 시 INCREMENT
      액션을 디스패치하여 카운트를 증가시킵니다.
      <button onClick={() => dispatch(decrement())}>감소</button> // 클릭 시
      DECREMENT 액션을 디스패치하여 카운트를 감소시킵니다.
    </div>
  );
}

function App() {
  return (
    <Provider store={store}>
      {" "}
      // Provider 컴포넌트를 사용하여 리액트 컴포넌트 트리에 스토어를 제공합니다.
      <Counter /> // Counter 컴포넌트를 렌더링합니다.
    </Provider>
  );
}

export default App; // App 컴포넌트를 기본 내보내기로 설정합니다.
```

이 예제에서, Redux를 사용하여 상태를 전역적으로 관리하고, `useSelector`와 `useDispatch` 훅을 통해 상태를 조회하고 변경할 수 있습니다.

## 결론

상태 관리 라이브러리는 복잡한 애플리케이션에서 상태를 일관되게 관리하고, 여러 컴포넌트 간의 상태 공유를 용이하게 합니다. Redux, MobX, Context API 등 다양한 도구를 활용하여 애플리케이션의 상태를 효율적으로 관리할 수 있습니다.
