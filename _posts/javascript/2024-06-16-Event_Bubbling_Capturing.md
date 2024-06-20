---
layout: post
title: 이벤트 버블링과 이벤트 캡처
date: 2024-06-16 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript
tags: Javascript
published: true
sitemap: true
---

# 이벤트 버블링과 이벤트 캡처

JavaScript에서는 이벤트가 발생했을 때, 해당 이벤트가 DOM 트리 구조를 따라 전파되는 방식이 있습니다. 이 전파 방식에는 이벤트 버블링과 이벤트 캡처 두 가지가 있습니다. 이 문서에서는 이벤트 버블링과 이벤트 캡처의 개념과 차이점, 그리고 이벤트 전파를 막는 방법에 대해 설명합니다.

## 이벤트 버블링 (Event Bubbling)

이벤트 버블링은 특정 요소에서 이벤트가 발생했을 때, 그 이벤트가 상위 요소로 전파되는 특성을 말합니다. 즉, 이벤트가 발생한 요소부터 시작하여 DOM 트리의 최상위 요소까지 순차적으로 이벤트가 전달됩니다.

### 예시

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>이벤트 버블링 예시</title>
  </head>
  <body>
    <div id="outer" style="padding: 50px; background-color: lightblue;">
      Outer Div
      <div id="middle" style="padding: 50px; background-color: lightgreen;">
        Middle Div
        <div id="inner" style="padding: 50px; background-color: lightcoral;">
          Inner Div
        </div>
      </div>
    </div>
    <script>
      document.getElementById("outer").addEventListener("click", function () {
        alert("Outer Div clicked");
      });
      document.getElementById("middle").addEventListener("click", function () {
        alert("Middle Div clicked");
      });
      document.getElementById("inner").addEventListener("click", function () {
        alert("Inner Div clicked");
      });
    </script>
  </body>
</html>
```

위 예시에서, 가장 안쪽의 `Inner Div`를 클릭하면 'Inner Div clicked', 'Middle Div clicked', 'Outer Div clicked' 알림이 순차적으로 나타납니다. 이는 이벤트가 `inner` div에서 발생하고, 상위 요소인 `middle` div와 `outer` div로 버블링되기 때문입니다.

## 이벤트 캡처 (Event Capturing)

이벤트 캡처는 이벤트 버블링과 반대 방향으로, 이벤트가 최상위 요소에서부터 시작하여 하위 요소로 전파되는 특성을 말합니다. 이를 사용하려면 `addEventListener` 메서드의 세 번째 파라미터로 `{ capture: true }` 옵션을 설정해야 합니다.

### 예시

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>이벤트 캡처 예시</title>
  </head>
  <body>
    <div id="outer" style="padding: 50px; background-color: lightblue;">
      Outer Div
      <div id="middle" style="padding: 50px; background-color: lightgreen;">
        Middle Div
        <div id="inner" style="padding: 50px; background-color: lightcoral;">
          Inner Div
        </div>
      </div>
    </div>
    <script>
      document.getElementById("outer").addEventListener(
        "click",
        function () {
          alert("Outer Div clicked");
        },
        { capture: true }
      );
      document.getElementById("middle").addEventListener(
        "click",
        function () {
          alert("Middle Div clicked");
        },
        { capture: true }
      );
      document.getElementById("inner").addEventListener(
        "click",
        function () {
          alert("Inner Div clicked");
        },
        { capture: true }
      );
    </script>
  </body>
</html>
```

위 예시에서, `Inner Div`를 클릭하면 'Outer Div clicked', 'Middle Div clicked', 'Inner Div clicked' 알림이 역순으로 나타납니다. 이는 이벤트가 최상위 요소인 `outer` div에서부터 하위 요소인 `inner` div로 캡처되기 때문입니다.

## 이벤트 전파 막기 (Stop Propagation)

이벤트 전파를 막기 위해서는 이벤트 객체의 `stopPropagation()` 메서드를 사용합니다. 이 메서드는 현재 이벤트가 더 이상 상위 또는 하위 요소로 전파되지 않도록 합니다.

### 예시

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>이벤트 전파 막기 예시</title>
  </head>
  <body>
    <div id="outer" style="padding: 50px; background-color: lightblue;">
      Outer Div
      <div id="middle" style="padding: 50px; background-color: lightgreen;">
        Middle Div
        <div id="inner" style="padding: 50px; background-color: lightcoral;">
          Inner Div
        </div>
      </div>
    </div>
    <script>
      document.getElementById("outer").addEventListener("click", function () {
        alert("Outer Div clicked");
      });
      document
        .getElementById("middle")
        .addEventListener("click", function (event) {
          event.stopPropagation();
          alert("Middle Div clicked");
        });
      document.getElementById("inner").addEventListener("click", function () {
        alert("Inner Div clicked");
      });
    </script>
  </body>
</html>
```

위 예시에서, `Inner Div`를 클릭하면 'Inner Div clicked', 'Middle Div clicked' 알림이 나타나지만, 'Outer Div clicked' 알림은 나타나지 않습니다. 이는 `middle` div의 클릭 이벤트 핸들러에서 `stopPropagation()` 메서드를 호출하여 이벤트 전파를 막았기 때문입니다.

## 결론

이벤트 버블링과 이벤트 캡처는 JavaScript에서 이벤트가 전파되는 두 가지 방식입니다. 이벤트 버블링은 하위 요소에서 상위 요소로, 이벤트 캡처는 상위 요소에서 하위 요소로 전파됩니다. 이벤트 전파를 막기 위해서는 `stopPropagation()` 메서드를 사용할 수 있습니다. 이 개념들을 이해하고 적절히 활용하면, 더욱 효율적이고 관리하기 쉬운 이벤트 처리를 구현할 수 있습니다.
