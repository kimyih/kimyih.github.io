---
layout: post
title: 자바스크립트 - this
date: 2024-05-20 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript 
tags: Javascript
published: true
sitemap: true
---

# 자바스크립트에서 `this` 키워드 이해하기
---

자바스크립트의 `this` 키워드는 문맥에 따라 다른 객체를 참조하기 때문에 이해하기 어려울 수 있습니다.    
이번 글에서는 `this`가 어떻게 동작하는지, 그리고 다양한 상황에서 `this`가 무엇을 가리키는지 쉽게 설명하겠습니다.   

<br>

## 1. 단독으로 사용할 경우 (전역 컨텍스트)
---

### 특징
단독으로 `this`를 사용할 경우, 전역 객체인 `window`를 가리킵니다.    브라우저 환경에서는 `window` 객체가 전역 객체이며, Node.js 환경에서는 `global` 객체가 전역 객체입니다.   

<br>

### 예제
```javascript
console.log(this); // window (브라우저 환경)
```
<br>

위 예제에서 `this`는 전역 컨텍스트에서 사용되었기 때문에 `window` 객체를 가리킵니다.   

<br>

## 2. 함수 안에서 사용할 경우 (일반 함수 컨텍스트)
---

### 특징
일반 함수 안에서 `this`는 함수가 호출될 때 결정됩니다.   
호출하는 주체에 따라 `this`가 달라질 수 있습니다.    
호출 방법에 따라 `this`가 가리키는 객체가 달라지므로 주의가 필요합니다.   

<br>

### 예제
```javascript
function showThis() {
    console.log(this);
}

showThis(); // window (브라우저 환경)
```

<br>

위 예제에서 `showThis` 함수는 일반 함수로 호출되었기 때문에 `this`는 전역 객체를 가리킵니다.   

<br>

### 주의사항
엄격 모드('strict mode')에서는 함수 안에서 `this`가 `undefined`로 설정됩니다.    

```javascript
'use strict';

function showThisStrict() {
    console.log(this); // undefined
}

showThisStrict();
```

<br>

## 3. 메서드 안에서 사용할 경우
--- 

### 특징
메서드 안에서 `this`는 해당 메서드를 호출한 객체를 가리킵니다.    
이는 메서드를 소유하고 있는 객체를 참조하게 됩니다.    

<br>

### 예제
```javascript
const person = {
    name: 'John',
    greet: function() {
        console.log(this.name);
    }
};

person.greet(); // John
```
<br>

위 예제에서 `greet` 메서드는 `person` 객체의 메서드로 호출되었기 때문에 `this`는 `person` 객체를 가리킵니다.   

<br>

## 4. 이벤트 핸들러 안에서 사용할 경우
---

### 특징
이벤트 핸들러 안에서 `this`는 이벤트를 받는 HTML 요소를 가리킵니다.

<br>

### 예제
```html
<button id="myButton">Click me</button>

<script>
document.getElementById('myButton').addEventListener('click', function() {
    console.log(this); // <button id="myButton">Click me</button>
});
</script>
```

<br>

위 예제에서 버튼을 클릭하면 `this`는 클릭 이벤트를 받는 HTML 요소, 즉 버튼 자신을 가리킵니다.   

<br>

## 5. 생성자 함수 안에서 사용할 경우
---

### 특징
생성자 함수 안에서 `this`는 새롭게 만들어진 객체를 가리킵니다.    
생성자 함수는 일반 함수와 구분되며, 주로 대문자로 시작하는 이름을 갖습니다.   

<br>

### 예제
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

const john = new Person('John', 30);
console.log(john.name); // John
console.log(john.age); // 30
```

<br>

위 예제에서 `Person` 생성자 함수는 `new` 키워드를 사용하여 호출되었기 때문에 `this`는 새롭게 생성된 객체를 가리킵니다.   

<br>

## 원리와 작동 방식
---


### this 바인딩 원리

- **전역 컨텍스트**: 전역에서 사용된 `this`는 전역 객체를 가리킵니다.   
- **함수 컨텍스트**: 함수 내부에서 `this`는 함수를 호출한 객체를 가리킵니다.   
- **메서드 컨텍스트**: 메서드 내부에서 `this`는 메서드를 소유한 객체를 가리킵니다.   
- **이벤트 핸들러 컨텍스트**: 이벤트 핸들러 내부에서 `this`는 이벤트를 받은 HTML 요소를 가리킵니다.   
- **생성자 함수 컨텍스트**: 생성자 함수 내부에서 `this`는 새롭게 생성된 객체를 가리킵니다.   

<br>

### 바인딩 함수 사용
함수의 `this` 값을 명확하게 설정하기 위해 `bind`, `call`, `apply` 메서드를 사용할 수 있습니다.   

<br>

- **bind**: 새로운 함수로 반환되며, `this` 값을 고정합니다.   
- **call**: 즉시 호출되며, 첫 번째 인자로 `this` 값을 설정합니다.   
- **apply**: `call`과 유사하지만, 인자를 배열로 받습니다.   

<br>

```javascript
function showThis() {
    console.log(this);
}

const obj = { name: 'John' };
const boundShowThis = showThis.bind(obj);
boundShowThis(); // { name: 'John' }

showThis.call(obj); // { name: 'John' }
showThis.apply(obj); // { name: 'John' }
```

<br>
<br>

## 결론
---

자바스크립트에서 `this`는 매우 중요한 키워드로, 문맥에 따라 다르게 동작합니다.    
전역에서, 함수 내부에서, 메서드 내부에서, 이벤트 핸들러에서, 생성자 함수에서 `this`가 어떻게 달라지는지 이해하는 것이 중요합니다.    
또한, `bind`, `call`, `apply` 메서드를 사용하여 `this` 값을 명확하게 설정할 수 있습니다.   

