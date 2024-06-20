---
layout: post
title: 콜백 함수와 재귀 함수
date: 2024-06-12 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript
tags: Javascript
published: true
sitemap: true
---

# 콜백 함수와 재귀 함수

프로그래밍에서 함수는 코드의 재사용성과 모듈화를 높이는 중요한 역할을 합니다. 특히 콜백 함수와 재귀 함수는 복잡한 작업을 효율적으로 처리하기 위해 자주 사용되는 기법입니다. 이 문서에서는 콜백 함수와 재귀 함수의 개념과 사용 방법에 대해 설명합니다.

## 1. 콜백 함수

콜백 함수는 다른 함수의 파라미터로 전달되어, 그 함수의 내부에서 실행되는 함수입니다. 콜백 함수는 비동기 작업이나 이벤트 처리에 유용하게 사용됩니다.

### 1.1 콜백 함수의 사용 예시

- **기본 예시**:

  ```javascript
  function greet(name, callback) {
    console.log("Hello, " + name);
    callback();
  }

  function afterGreet() {
    console.log("This is a callback function.");
  }

  greet("John", afterGreet);
  ```

  이 예시에서 `greet` 함수는 `name`과 `callback` 두 개의 파라미터를 받습니다. `afterGreet` 함수가 콜백 함수로 전달되어 `greet` 함수 내부에서 실행됩니다.

- **비동기 작업에서의 사용**:

  ```javascript
  function fetchData(callback) {
    setTimeout(function () {
      console.log("Data fetched");
      callback("Data");
    }, 2000);
  }

  function processData(data) {
    console.log("Processing: " + data);
  }

  fetchData(processData);
  ```

  이 예시에서는 `fetchData` 함수가 비동기 작업(2초 후에 데이터를 가져오는 작업)을 수행하고, 완료된 후에 콜백 함수 `processData`를 호출합니다.

## 2. 재귀 함수

재귀 함수는 함수 내부에서 자기 자신을 다시 호출하여 작업을 수행하는 함수입니다. 재귀 함수는 반복적인 작업을 처리하거나 복잡한 문제를 단순화하는 데 유용합니다.

### 2.1 재귀 함수의 사용 예시

- **기본 예시**:

  ```javascript
  function factorial(n) {
    if (n === 0) {
      return 1;
    }
    return n * factorial(n - 1);
  }

  console.log(factorial(5)); // 출력: 120
  ```

  이 예시에서 `factorial` 함수는 입력값 `n`의 팩토리얼을 계산합니다. `n`이 0일 때 1을 반환하고, 그렇지 않으면 `n`과 `factorial(n - 1)`의 곱을 반환합니다.

- **피보나치 수열**:

  ```javascript
  function fibonacci(n) {
    if (n <= 1) {
      return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
  }

  console.log(fibonacci(6)); // 출력: 8
  ```

  이 예시에서 `fibonacci` 함수는 입력값 `n`의 피보나치 수를 계산합니다. `n`이 1 이하일 때 `n`을 반환하고, 그렇지 않으면 `fibonacci(n - 1)`과 `fibonacci(n - 2)`의 합을 반환합니다.

## 3. 콜백 함수와 재귀 함수의 차이

- **콜백 함수**는 주로 비동기 작업이나 이벤트 처리를 위해 사용되며, 함수가 다른 함수의 파라미터로 전달되어 내부에서 실행됩니다.
- **재귀 함수**는 함수 내부에서 자기 자신을 호출하여 반복적인 작업을 수행하거나 복잡한 문제를 해결하는 데 사용됩니다.

## 결론

콜백 함수와 재귀 함수는 각각 비동기 작업 처리와 반복적인 문제 해결에 유용하게 사용되는 기법입니다. 콜백 함수는 다른 함수의 파라미터로 전달되어 해당 함수의 실행 흐름을 제어하며, 재귀 함수는 자기 자신을 호출하여 복잡한 문제를 간단하게 해결할 수 있습니다. 이 두 가지 기법을 이해하고 적절히 활용하면 더 효율적이고 유지보수하기 쉬운 코드를 작성할 수 있습니다.
