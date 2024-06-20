---
layout: post
title: jQuery 메서드 중 attr()과 prop()의 차이
date: 2024-06-11 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript
tags: Javascript
published: true
sitemap: true
---

# jQuery 메서드 중 attr()과 prop()의 차이

jQuery는 HTML 요소를 쉽게 조작할 수 있도록 다양한 메서드를 제공합니다. 그 중 `attr()`과 `prop()` 메서드는 태그들의 속성값을 정의하거나 가져오기 위해 사용됩니다. 이 두 메서드는 비슷해 보이지만, 다루는 대상이 다릅니다. `attr()`은 HTML 속성(attribute)을 다루고, `prop()`은 JavaScript 프로퍼티(property)를 다룹니다. 이 문서에서는 두 메서드의 차이점과 사용 방법에 대해 설명합니다.

## 1. attr() 메서드

`attr()` 메서드는 HTML 요소의 속성을 가져오거나 설정하는 데 사용됩니다. 이 메서드는 HTML 마크업에서 정의된 속성에 접근할 때 유용합니다.

- **속성 값 가져오기**:

  ```javascript
  // id가 "myElement"인 요소의 title 속성 값을 가져옵니다.
  var title = $("#myElement").attr("title");
  ```

- **속성 값 설정하기**:
  ```javascript
  // id가 "myElement"인 요소의 title 속성 값을 "새로운 제목"으로 설정합니다.
  $("#myElement").attr("title", "새로운 제목");
  ```

## 2. prop() 메서드

`prop()` 메서드는 JavaScript 프로퍼티를 가져오거나 설정하는 데 사용됩니다. 이는 HTML 속성보다 더 동적인 JavaScript 객체의 속성을 다룰 때 유용합니다.

- **프로퍼티 값 가져오기**:

  ```javascript
  // 체크박스가 체크되어 있는지 여부를 가져옵니다.
  var isChecked = $("#myCheckbox").prop("checked");
  ```

- **프로퍼티 값 설정하기**:
  ```javascript
  // 체크박스를 체크 상태로 설정합니다.
  $("#myCheckbox").prop("checked", true);
  ```

## 3. 주요 차이점

- **속성 vs 프로퍼티**:

  - `attr()`은 HTML 속성을 다룹니다. 예를 들어, `<input type="text" value="Hello">`에서 `value`는 속성입니다.
  - `prop()`은 JavaScript 프로퍼티를 다룹니다. 같은 `<input>` 요소에서 `value`는 JavaScript 프로퍼티로, 사용자가 입력한 현재 값을 나타냅니다.

- **사용 예시**:

  - `attr('value')`는 초기 설정된 값을 반환합니다.
  - `prop('value')`는 현재 값을 반환합니다.

- **기타**:
  - `attr()`은 문자열 값을 반환하며, 이는 HTML 마크업에 정의된 값입니다.
  - `prop()`은 실제 DOM 요소의 현재 상태를 반영하는 값으로, Boolean, 숫자, 객체 등 다양한 타입을 반환할 수 있습니다.

## 4. 예시 코드

아래 코드는 `attr()`과 `prop()`의 차이를 보여주는 예제입니다.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <title>jQuery attr() vs prop() 예제</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>
      $(document).ready(function () {
        var $input = $("#myInput");
        // 초기 속성 값과 프로퍼티 값 출력
        console.log('attr("value"):', $input.attr("value")); // 초기 속성 값
        console.log('prop("value"):', $input.prop("value")); // 현재 프로퍼티 값

        // 값 변경
        $input.val("변경된 값");
        // 변경 후 속성 값과 프로퍼티 값 출력
        console.log('attr("value") 변경 후:', $input.attr("value")); // 초기 속성 값 (변경되지 않음)
        console.log('prop("value") 변경 후:', $input.prop("value")); // 현재 프로퍼티 값 (변경됨)
      });
    </script>
  </head>
  <body>
    <input type="text" id="myInput" value="초기 값" />
  </body>
</html>
```

## 결론

`attr()`과 `prop()` 메서드는 jQuery에서 속성과 프로퍼티를 다루기 위해 사용됩니다. `attr()`은 HTML 속성을, `prop()`은 JavaScript 프로퍼티를 다루므로 상황에 맞게 적절한 메서드를 사용하는 것이 중요합니다. 이를 통해 웹 요소를 효과적으로 제어할 수 있습니다.
