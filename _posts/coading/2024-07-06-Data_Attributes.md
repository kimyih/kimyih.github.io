---
layout: post
title: 데이터 속성
date: 2024-07-06 19:58 +0900
description: HTML/CSS
image: ../assets/img/htmlcss.png
category: HTML/CSS
tags: note
published: true
sitemap: true
---

# 데이터 속성(Data Attributes)

## 데이터 속성이란?

HTML5부터 데이터 속성이라는 개념이 추가되었습니다. 데이터 속성은 HTML 요소의 `data-`로 시작하는 속성으로, 특정한 데이터를 DOM 요소에 저장해두기 위해 사용됩니다. 이를 통해 JavaScript를 통해 쉽게 데이터를 읽고 쓸 수 있습니다.

## 데이터 속성 사용 방법

데이터 속성은 `data-`로 시작하며, 하이픈(`-`) 뒤에 임의의 이름을 붙여 사용할 수 있습니다. 예를 들어, `data-user-id`나 `data-role` 같은 속성을 정의할 수 있습니다.

```html
<div id="user" data-user-id="12345" data-role="admin">User Info</div>
```

위의 예시에서 `div` 요소는 `data-user-id`와 `data-role`이라는 두 개의 데이터 속성을 가지고 있습니다.

## 데이터 속성 읽기 및 쓰기

JavaScript를 사용하여 데이터 속성을 쉽게 읽고 쓸 수 있습니다.

### 데이터 속성 읽기

`dataset` 프로퍼티를 사용하여 데이터 속성을 읽을 수 있습니다.

```javascript
const userDiv = document.getElementById("user");
const userId = userDiv.dataset.userId;
const userRole = userDiv.dataset.role;

console.log(userId); // 12345
console.log(userRole); // admin
```

### 데이터 속성 쓰기

`dataset` 프로퍼티를 사용하여 데이터 속성의 값을 설정할 수 있습니다.

```javascript
userDiv.dataset.userId = "67890";
userDiv.dataset.role = "guest";

console.log(userDiv.dataset.userId); // 67890
console.log(userDiv.dataset.role); // guest
```

## 데이터 속성의 활용

데이터 속성은 다양한 상황에서 유용하게 활용될 수 있습니다. 다음은 몇 가지 활용 예시입니다.

### 1. 사용자 정의 데이터 저장

데이터 속성은 HTML 요소에 사용자 정의 데이터를 저장하는 데 사용될 수 있습니다. 이를 통해 JavaScript와의 상호작용을 쉽게 만들 수 있습니다.

```html
<button id="saveBtn" data-status="unsaved">Save</button>
```

```javascript
const saveBtn = document.getElementById("saveBtn");
console.log(saveBtn.dataset.status); // unsaved
```

### 2. UI 상태 저장

데이터 속성을 사용하여 UI 요소의 상태를 저장하고 관리할 수 있습니다.

```html
<div id="sidebar" data-visible="true">Sidebar Content</div>
```

```javascript
const sidebar = document.getElementById("sidebar");

if (sidebar.dataset.visible === "true") {
  sidebar.style.display = "block";
} else {
  sidebar.style.display = "none";
}
```

### 3. 이벤트 핸들러에서 데이터 전달

데이터 속성을 사용하여 이벤트 핸들러에 데이터를 전달할 수 있습니다.

```html
<button class="action-btn" data-action="delete" data-id="1">Delete</button>
<button class="action-btn" data-action="edit" data-id="2">Edit</button>
```

```javascript
document.querySelectorAll(".action-btn").forEach((button) => {
  button.addEventListener("click", (event) => {
    const action = event.target.dataset.action;
    const id = event.target.dataset.id;

    console.log(`Action: ${action}, ID: ${id}`);
    // Action에 따라 처리
  });
});
```

## 결론

데이터 속성은 HTML5에서 제공하는 강력한 기능으로, DOM 요소에 사용자 정의 데이터를 저장하고 JavaScript와 상호작용하는 데 매우 유용합니다. `data-`로 시작하는 속성을 통해 데이터를 저장하고, `dataset` 프로퍼티를 사용하여 데이터를 읽고 쓸 수 있습니다. 다양한 상황에서 데이터 속성을 활용하여 웹 애플리케이션의 유연성을 높일 수 있습니다.
