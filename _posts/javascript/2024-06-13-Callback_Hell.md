---
layout: post
title: 콜백 지옥 및 해결 방법
date: 2024-06-13 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript
tags: Javascript
published: true
sitemap: true
---

# 콜백 지옥 및 해결 방법

## 콜백 지옥

콜백 지옥(callback hell)은 비동기 작업을 처리할 때 중첩된 콜백 함수가 많아지면서 코드가 복잡하고 가독성이 떨어지는 현상을 말합니다. 콜백 함수는 비동기 작업을 순차적으로 처리하기 위해 자주 사용되지만, 함수가 많아질수록 코드의 가독성과 유지보수성이 크게 저하됩니다. 콜백 지옥은 특히 Node.js와 같은 비동기 처리를 많이 사용하는 환경에서 자주 발생합니다.

### 콜백 지옥 예시

```javascript
function fetchData(callback) {
  setTimeout(function () {
    console.log("Data fetched");
    callback("Data");
  }, 2000);
}

function processData(data, callback) {
  setTimeout(function () {
    console.log("Data processed");
    callback("Processed Data");
  }, 2000);
}

function saveData(data, callback) {
  setTimeout(function () {
    console.log("Data saved");
    callback("Saved Data");
  }, 2000);
}

fetchData(function (data) {
  processData(data, function (processedData) {
    saveData(processedData, function (savedData) {
      console.log(savedData);
    });
  });
});
```

위 예시에서 볼 수 있듯이, 콜백 함수가 중첩되면서 코드가 오른쪽으로 계속 밀려나는 형태를 보입니다. 이는 가독성을 저하시키고, 디버깅과 유지보수를 어렵게 만듭니다.

## 콜백 지옥을 해결하는 방법

콜백 지옥을 해결하기 위해서는 주로 `Promise`를 사용합니다. `Promise`는 비동기 작업을 처리할 때 콜백 함수 대신 사용할 수 있는 객체로, 비동기 작업의 결과를 처리하는데 더 직관적이고 가독성이 좋은 방법을 제공합니다.

### Promise 사용 예시

```javascript
function fetchData() {
  return new Promise(function (resolve, reject) {
    setTimeout(function () {
      console.log("Data fetched");
      resolve("Data");
    }, 2000);
  });
}

function processData(data) {
  return new Promise(function (resolve, reject) {
    setTimeout(function () {
      console.log("Data processed");
      resolve("Processed Data");
    }, 2000);
  });
}

function saveData(data) {
  return new Promise(function (resolve, reject) {
    setTimeout(function () {
      console.log("Data saved");
      resolve("Saved Data");
    }, 2000);
  });
}

fetchData()
  .then(processData)
  .then(saveData)
  .then(function (savedData) {
    console.log(savedData);
  })
  .catch(function (error) {
    console.error(error);
  });
```

위 예시에서는 `fetchData`, `processData`, `saveData` 함수를 `Promise`로 변환하여 사용합니다. 이를 통해 콜백 함수의 중첩을 피하고, 비동기 작업을 순차적으로 처리할 수 있습니다. `then` 메서드는 각 비동기 작업의 성공 결과를 처리하고, `catch` 메서드는 에러를 처리합니다.

### 결론

콜백 지옥은 비동기 작업을 처리할 때 콜백 함수가 중첩되어 발생하는 문제로, 코드의 가독성과 유지보수성을 저하시킵니다. 이를 해결하기 위해 `Promise`를 사용하면 더 직관적이고 가독성 좋은 코드를 작성할 수 있습니다. `Promise`를 사용하면 비동기 작업을 순차적으로 처리할 수 있으며, 에러 처리를 간편하게 할 수 있습니다.
