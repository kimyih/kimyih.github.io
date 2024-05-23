---
layout: post
title: 자바스크립트 - ES6 문법 특징과 차이점 이해하기
date: 2024-05-18 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript 
tags: Javascript
published: true
sitemap: true
---

# ES6 문법 특징과 차이점 이해하기
---

**ECMAScript 6(ES6)** 또는 **ECMAScript 2015** 는 자바스크립트의 최신 표준 중 하나로, 여러 새로운 기능과 문법을 도입하여 자바스크립트 프로그래밍을 더욱 간결하고 효율적으로 만들었습니다.    
이번 글에서는 ES6의 주요 특징과 그 차이점을 쉽게 설명하겠습니다.   

<br>

## 1. 화살표 함수 (Arrow Function)
---

<br>

### 특징
화살표 함수는 ES6에서 도입된 새로운 함수 선언 방법으로, 기존의 함수 선언보다 문법이 간단합니다.    
특히, `this` 키워드의 처리가 직관적이어서 콜백 함수 내에서 `this`를 사용할 때 유용합니다.     

   

### 예제
```javascript
// ES5의 함수 선언
var add = function(a, b) {
    return a + b;
};

// ES6의 화살표 함수
const add = (a, b) => a + b;
```

<br>

화살표 함수는 `function` 키워드 대신 `=>`를 사용하여 함수를 정의합니다.    
매개변수가 하나일 경우 괄호를 생략할 수 있으며, 함수 본문이 단일 표현식일 경우 중괄호와 `return` 키워드도 생략할 수 있습니다.   

<br>

### 화살표 함수와 `this`
화살표 함수는 일반 함수와 달리 자신만의 `this` 바인딩을 가지지 않습니다.    
대신, 자신을 둘러싼 외부 스코프의 `this`를 그대로 가리킵니다.    
이는 콜백 함수나 이벤트 핸들러에서 유용합니다.   

<br>

```javascript
function Person() {
    this.age = 0;

    setInterval(() => {
        this.age++; // `this`는 Person 객체를 가리킴
        console.log(this.age);
    }, 1000);
}

var p = new Person();
```

<br>

위 예제에서 화살표 함수를 사용함으로써 `this`가 `Person` 객체를 가리키게 됩니다.    
일반 함수로 선언하면 `this`가 `window` 객체를 가리키기 때문에 원하는 결과를 얻지 못합니다.   

<br>

## 2. 템플릿 리터럴 (Template Literal)
---

<br>

### 특징
템플릿 리터럴은 백틱(``` ` ```)을 사용하여 문자열을 작성하는 새로운 방법입니다.     
이를 통해 여러 줄의 문자열을 쉽게 작성하고, 문자열 내에서 변수를 간단히 삽입할 수 있습니다.   

<br>

### 예제
```javascript
// ES5의 문자열 결합
var name = "John";
var greeting = "Hello, " + name + "! Welcome to the ES6 tutorial.";

// ES6의 템플릿 리터럴
const name = "John";
const greeting = `Hello, ${name}! Welcome to the ES6 tutorial.`;
```

<br>

템플릿 리터럴은 `${}` 구문을 사용하여 문자열 내에 변수를 삽입할 수 있어, 문자열 결합을 더욱 간편하게 할 수 있습니다.   

<br>

### 여러 줄 문자열
템플릿 리터럴을 사용하면 여러 줄의 문자열을 쉽게 작성할 수 있습니다.    

```javascript
const message = `This is a template literal.
It allows for multiple lines of text
without needing special characters.`;

console.log(message);
```

<br>

위 예제에서 템플릿 리터럴을 사용하여 여러 줄의 문자열을 작성할 수 있습니다.   

<br>

## 3. 기본 매개변수 (Default Parameters)
---

<br>

### 특징
기본 매개변수는 함수 호출 시 인자가 제공되지 않거나 `undefined`인 경우에 기본값을 설정할 수 있는 기능입니다.   

<br>

### 예제
```javascript
// ES5에서의 기본 매개변수 설정
function greet(name) {
    var name = name || "Guest";
    console.log("Hello, " + name);
}

// ES6에서의 기본 매개변수 설정
function greet(name = "Guest") {
    console.log(`Hello, ${name}`);
}

greet(); // Hello, Guest
greet("John"); // Hello, John
```

<br>

ES6에서는 함수 선언 시 매개변수에 기본값을 직접 지정할 수 있어, 코드가 더 간결해집니다.   

<br>

## 4. 비구조화 할당 (Destructuring Assignment)
---

<br>

### 특징
비구조화 할당은 배열이나 객체의 요소를 개별 변수로 추출할 수 있는 문법입니다.    
이를 통해 코드의 가독성을 높이고, 변수 선언을 간단히 할 수 있습니다.   

<br>

### 배열의 비구조화 할당
배열의 요소를 개별 변수로 추출할 수 있습니다.   

```javascript
const numbers = [1, 2, 3];
const [first, second, third] = numbers;
console.log(first); // 1
console.log(second); // 2
```
<br>

### 객체의 비구조화 할당
객체의 속성을 개별 변수로 추출할 수 있습니다. 

```javascript
const person = { name: "John", age: 30 };
const { name, age } = person;
console.log(name); // John
console.log(age); // 30
```

<br>

### 기본값과 함께 사용
비구조화 할당 시 기본값을 설정할 수 있습니다.   

```javascript
const person = { name: "John" };
const { name, age = 25 } = person;
console.log(name); // John
console.log(age); // 25
```
<br>

위 예제에서 `age`는 기본값인 25로 설정됩니다.   

<br>

## 5. 모듈 (Modules)
---

<br>

### 특징
ES6 이전에는 자바스크립트 모듈을 관리하기 위해 여러 라이브러리와 도구를 사용해야 했습니다.   
ES6에서는 `import`와 `export` 키워드를 사용하여 모듈을 쉽게 관리할 수 있습니다.   

<br>

### 예제
```javascript
// math.js 파일에서 함수 내보내기
export function add(a, b) {
    return a + b;
}

export function subtract(a, b) {
    return a - b;
}

// main.js 파일에서 함수 불러오기
import { add, subtract } from './math';

console.log(add(5, 3)); // 8
console.log(subtract(5, 3)); // 2
```
<br>

`export` 키워드를 사용하여 모듈에서 내보낼 함수를 정의하고, `import` 키워드를 사용하여 다른 모듈에서 이 함수를 불러올 수 있습니다.     
이를 통해 코드의 재사용성을 높이고, 모듈 간의 의존성을 명확하게 관리할 수 있습니다.   

<br>

### 디폴트 익스포트
모듈에서 하나의 기본 값을 내보내고 불러올 수 있습니다.   

```javascript
// message.js 파일에서 디폴트 함수 내보내기
export default function() {
    console.log("This is the default export!");
}

// main.js 파일에서 디폴트 함수 불러오기
import showMessage from './message';

showMessage(); // This is the default export!
```

<br>

위 예제에서 `export default`를 사용하여 함수를 내보내고, `import`를 통해 해당 함수를 불러와 사용할 수 있습니다.   

<br>
<br>

## 결론
--- 

ES6는 자바스크립트에 많은 새로운 기능과 문법을 도입하여 개발자들이 더 간결하고 효율적인 코드를 작성할 수 있게 합니다.     
화살표 함수, 템플릿 리터럴, 기본 매개변수, 비구조화 할당, 모듈과 같은 ES6의 주요 특징을 이해하고 사용하면, 더 나은 자바스크립트 코드를 작성할 수 있습니다.    

