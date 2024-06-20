---
layout: post
title: Promise와 콜백 지옥
date: 2024-06-14 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript
tags: Javascript
published: true
sitemap: true
---

# Promise와 콜백 지옥

JavaScript에서 비동기 처리를 위해 주로 사용되는 두 가지 방법은 콜백 함수와 Promise입니다. 두 방법 모두 비동기 작업을 처리하지만, 코드의 가독성과 유지보수성 측면에서 차이가 있습니다.

## 콜백 (Callback)

콜백 함수는 함수의 파라미터로 전달되어 함수 내부에서 실행되는 함수입니다. 비동기 작업의 순서를 제어하기 위해 콜백 함수를 중첩해서 사용하면, 코드의 흐름을 쉽게 이해할 수 있습니다. 그러나 함수가 많아질수록 중첩된 콜백 함수들로 인해 코드의 가독성이 떨어지는 현상이 발생합니다. 이를 콜백 지옥(callback hell)이라고 합니다.

### 콜백 함수 사용 예시

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

위 코드에서 볼 수 있듯이, 중첩된 콜백 함수로 인해 코드가 오른쪽으로 점점 밀려나는 현상이 발생하며, 이는 가독성을 크게 저하시킵니다.

## Promise

Promise는 비동기 작업의 결과값을 나타내는 객체로, 작업이 성공하거나 실패한 후 그 결과값을 처리할 수 있도록 도와줍니다. Promise는 `.then` 메서드를 통해 비동기 작업의 순서를 정의할 수 있으며, 콜백 지옥을 피할 수 있게 해줍니다. 그러나 함수가 많아지면 여전히 가독성이 떨어질 수 있습니다.

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

위 예시에서 Promise를 사용하여 각 비동기 작업을 체인 형태로 연결함으로써, 콜백 지옥을 피하고 가독성을 개선할 수 있습니다. `.then` 메서드를 사용하여 작업의 순서를 정의하고, `.catch` 메서드를 사용하여 에러를 처리할 수 있습니다.

## 결론

콜백 함수와 Promise는 모두 JavaScript에서 비동기 작업을 처리하는 중요한 방법입니다. 콜백 함수는 간단한 비동기 작업에 유용하지만, 중첩된 콜백으로 인해 콜백 지옥이 발생할 수 있습니다. Promise는 이러한 문제를 해결하기 위해 고안된 방법으로, 비동기 작업을 더 체계적으로 관리할 수 있도록 도와줍니다. 그러나 함수가 많아질 경우, 여전히 가독성 문제가 발생할 수 있으므로, 상황에 맞게 적절한 방법을 선택하여 사용하는 것이 중요합니다.
