---
layout: post
title: 함수 선언식과 함수 표현식
date: 2024-06-15 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript
tags: Javascript
published: true
sitemap: true
---

# 함수 선언식과 함수 표현식

JavaScript에서 함수를 정의하는 방법은 크게 두 가지가 있습니다: 함수 선언식과 함수 표현식. 이 두 가지 방법은 함수의 정의와 호출 시점, 그리고 스코프 처리 방식에서 차이가 있습니다. 이 문서에서는 함수 선언식과 함수 표현식의 차이점과 각각의 특징에 대해 설명합니다.

## 함수 선언식

함수 선언식은 함수의 일반적인 선언 형태입니다. 이 방식은 `function` 키워드 다음에 함수 이름을 명시하여 함수를 정의합니다. 함수 선언식으로 정의된 함수는 호이스팅(hoisting)에 의해 함수 선언부가 스코프의 최상단으로 끌어올려지므로, 함수 정의 이전에 호출할 수 있습니다.

### 함수 선언식 예시

```javascript
function greet(name) {
  return "Hello, " + name;
}

console.log(greet("John")); // 출력: Hello, John
```

위 예시에서 `greet` 함수는 함수 선언식으로 정의되었습니다. 이 함수는 정의 이전에 호출할 수 있으며, 이는 JavaScript의 호이스팅 덕분입니다.

### 호이스팅

호이스팅은 JavaScript의 고유한 동작 방식으로, 변수 선언과 함수 선언이 스코프의 최상단으로 끌어올려지는 것을 말합니다. 함수 선언식의 경우, 함수 전체가 호이스팅되므로 함수 정의 이전에 호출해도 문제가 없습니다.

```javascript
console.log(greet("John")); // 출력: Hello, John

function greet(name) {
  return "Hello, " + name;
}
```

## 함수 표현식

함수 표현식은 함수를 변수에 할당하여 정의하는 방식입니다. 이 방식은 함수 이름을 생략할 수 있으며, 익명 함수(anonymous function)를 사용하는 것이 일반적입니다. 함수 표현식으로 정의된 함수는 할당된 변수의 스코프 내에서만 호출할 수 있으며, 함수 정의 이전에는 호출할 수 없습니다.

### 함수 표현식 예시

```javascript
const greet = function (name) {
  return "Hello, " + name;
};

console.log(greet("John")); // 출력: Hello, John
```

위 예시에서 `greet` 함수는 함수 표현식으로 정의되었습니다. 이 함수는 변수 `greet`에 할당된 후에만 호출할 수 있습니다.

### 호이스팅의 차이

함수 표현식의 경우, 변수 선언만 호이스팅되며, 함수의 정의는 호이스팅되지 않습니다. 따라서 함수 정의 이전에 함수를 호출하려고 하면 참조 오류(reference error)가 발생합니다.

```javascript
console.log(greet("John")); // 오류: greet is not defined

const greet = function (name) {
  return "Hello, " + name;
};
```

## 함수 선언식과 함수 표현식의 차이점

1. **호이스팅**:

   - 함수 선언식: 함수 전체가 호이스팅되므로 함수 정의 이전에 호출할 수 있습니다.
   - 함수 표현식: 변수 선언만 호이스팅되므로 함수 정의 이전에 호출할 수 없습니다.

2. **익명 함수**:

   - 함수 선언식: 항상 함수 이름을 명시해야 합니다.
   - 함수 표현식: 함수 이름을 생략할 수 있으며, 익명 함수를 사용할 수 있습니다.

3. **스코프**:
   - 함수 선언식: 함수가 정의된 스코프 전체에서 접근 가능합니다.
   - 함수 표현식: 함수가 할당된 변수의 스코프 내에서만 접근 가능합니다.

## 결론

함수 선언식과 함수 표현식은 각각의 용도와 상황에 맞게 사용됩니다. 함수 선언식은 함수의 호이스팅 덕분에 코드의 어느 위치에서든 호출할 수 있으며, 함수 표현식은 더 명확한 스코프 관리를 제공합니다. JavaScript 개발에서는 이 두 가지 방법을 이해하고 적절하게 활용하여 코드를 작성하는 것이 중요합니다.
