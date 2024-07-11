---
layout: post
title: 불변성 유지하기
date: 2024-07-04 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript
tags: Javascript
published: true
sitemap: true
---

# 불변성(Immutability) 유지하기

## 불변성(Immutability)이란?

불변성은 프로그래밍에서 데이터의 원본이 훼손되는 것을 막는 것을 의미합니다. 불변성을 유지하면 코드의 예측 가능성을 높이고, 디버깅을 쉽게 하며, 멀티스레딩 환경에서도 안전하게 동작할 수 있습니다.

## 변수 불변하게 만들기

변수 선언 시 `var` 대신 `const`를 사용하여 변수 자체를 불변하게 만들 수 있습니다. `const`로 선언된 변수는 재할당이 불가능합니다.

```javascript
const name = "John";
// name = "Doe"; // 오류: 재할당 불가
```

## 값 불변하게 만들기

원시형 타입(Primitive Type)은 그 값 자체가 불변합니다. 원시형 타입에는 숫자, 문자열, 불리언 등이 포함됩니다.

```javascript
const number = 42;
const string = "Hello, world!";
const isTrue = true;

// 원시형 타입은 불변하므로 값 자체가 변경되지 않음
```

반면, 객체(Object)는 같은 객체라도 속성 값을 바꿀 수 있어 가변입니다.

### 객체를 불변하게 만드는 방법

1. **`Object.assign()` 사용하기**
   `Object.assign()` 메서드를 사용하여 객체를 복사하고, 복사된 객체를 수정하여 원본 객체의 불변성을 유지할 수 있습니다.

   ```javascript
   const original = { a: 1, b: 2 };
   const copy = Object.assign({}, original, { b: 3 });

   console.log(original); // { a: 1, b: 2 }
   console.log(copy); // { a: 1, b: 3 }
   ```

2. **`Object.freeze()` 사용하기**
   `Object.freeze()` 메서드를 사용하여 객체를 동결하면 객체의 속성을 수정할 수 없게 됩니다.

   ```javascript
   const obj = { a: 1, b: 2 };
   Object.freeze(obj);

   obj.a = 3; // 무시됨, 오류 발생하지 않음
   console.log(obj); // { a: 1, b: 2 }
   ```

3. **중첩 객체(Nested Object) 불변하게 만들기**
   중첩 객체의 경우, 내부 객체도 별도로 불변하게 만들어야 합니다. 이를 위해 재귀적으로 `Object.freeze()`를 적용할 수 있습니다.

   ```javascript
   function deepFreeze(obj) {
     Object.keys(obj).forEach((name) => {
       let prop = obj[name];
       if (typeof prop === "object" && prop !== null) {
         deepFreeze(prop);
       }
     });
     return Object.freeze(obj);
   }

   const nestedObj = {
     a: 1,
     b: {
       c: 2,
       d: 3,
     },
   };

   deepFreeze(nestedObj);
   nestedObj.b.c = 4; // 무시됨
   console.log(nestedObj); // { a: 1, b: { c: 2, d: 3 } }
   ```

4. **불변 함수 사용하기**
   함수형 프로그래밍에서는 불변성을 유지하기 위해 불변 함수(Immutable Function)를 사용합니다. 이는 상태를 변경하지 않고, 새로운 상태를 반환하는 함수입니다.

   ```javascript
   const originalArray = [1, 2, 3];

   const newArray = originalArray.map((num) => num * 2);
   console.log(originalArray); // [1, 2, 3]
   console.log(newArray); // [2, 4, 6]

   const originalObj = { a: 1, b: 2 };
   const newObj = { ...originalObj, b: 3 };
   console.log(originalObj); // { a: 1, b: 2 }
   console.log(newObj); // { a: 1, b: 3 }
   ```

## 결론

불변성을 유지하는 것은 안정적이고 예측 가능한 코드를 작성하는 데 중요합니다. 변수 선언 시 `const`를 사용하고, 객체의 불변성을 유지하기 위해 `Object.assign()`, `Object.freeze()`, 중첩 객체의 재귀적 동결, 그리고 불변 함수를 활용할 수 있습니다. 이러한 방법들을 사용하여 코드를 더욱 견고하게 만들 수 있습니다.
