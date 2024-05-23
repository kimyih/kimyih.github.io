---
layout: post
title: 자바스크립트 - 호이스팅(Hoisting)
date: 2024-05-18 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript 
tags: Javascript
published: true
sitemap: true
---

<br>

# 자바스크립트에서의 호이스팅(Hoisting) 이해하기

자바스크립트는 다른 프로그래밍 언어와는 다르게 호이스팅이라는 독특한 메커니즘을 가지고 있습니다.    
이번 글에서는 호이스팅이 무엇인지, 어떻게 작동하는지, 그리고 이를 어떻게 이해하고 사용할 수 있는지 쉽게 설명하겠습니다.   

<br>

## 호이스팅이란 무엇인가?
---

호이스팅(Hoisting)은 자바스크립트에서 변수나 함수의 선언이 어디에 있든지 간에 최상단으로 끌어 올려지는 것을 의미합니다.  
즉, 변수나 함수를 선언하기 전에 사용할 수 있는 것처럼 보이게 합니다.   

<br>

## 호이스팅의 작동 방식
---

<br>

호이스팅은 변수 선언과 함수 선언을 코드의 최상단으로 끌어올립니다.    하지만 변수의 초기화는 호이스팅되지 않습니다.     
이는 변수가 `undefined`로 초기화된다는 것을 의미합니다.  

<br>

### 변수 호이스팅   
--- 

변수 선언은 호이스팅되지만, 초기화는 호이스팅되지 않습니다.     
예를 들어, 다음 코드를 보겠습니다.   

```javascript
console.log(x); // undefined
var x = 5;
console.log(x); // 5
```
<br>

위 코드에서 `x` 변수는 선언되기 전에 사용되었습니다. 
자바스크립트는 변수 선언을 최상단으로 끌어 올리기 때문에 첫 번째 `console.log(x)`에서 `x`는 `undefined`로 초기화됩니다.     
그런 다음, `x`에 5가 할당되므로 두 번째 `console.log(x)`에서 5가 출력됩니다.

<br>

### 함수 호이스팅
---

함수 선언도 호이스팅됩니다.     
함수는 변수와 다르게 전체 함수가 호이스팅됩니다.   
예를 들어, 다음 코드를 보겠습니다.    

```javascript
console.log(add(2, 3)); // 5

function add(a, b) {
    return a + b;
}
```

<br>

위 코드에서 `add` 함수는 선언되기 전에 호출되었습니다.    
자바스크립트는 함수 선언 전체를 최상단으로 끌어올리기 때문에 함수 호출이 정상적으로 작동합니다.   

<br>

## 호이스팅의 한계
---

호이스팅은 `var`로 선언된 변수와 함수 선언에만 적용됩니다.     
`let`과 `const`로 선언된 변수는 호이스팅되지만, 초기화되기 전까지는 접근할 수 없습니다.     
이를 "일시적 사각지대(TDZ)"라고 합니다.   

<br>

### `let`과 `const`의 호이스팅    
--- 

```javascript
console.log(y); // ReferenceError: y is not defined
let y = 10;
```

<br>

위 코드에서 `y` 변수는 `let`으로 선언되었기 때문에 호이스팅은 되지만, 초기화되기 전까지는 사용할 수 없습니다.     
따라서 `ReferenceError`가 발생합니다.   

<br>

### 함수 표현식의 호이스팅
--- 

함수 표현식은 변수에 할당된 함수로, 변수 선언만 호이스팅되고 함수 정의는 호이스팅되지 않습니다.   

<br>

```javascript
console.log(subtract(5, 3)); // TypeError: subtract is not a function

var subtract = function(a, b) {
    return a - b;
};
```
<br>

위 코드에서 `subtract`는 함수 표현식입니다.     
변수 선언만 호이스팅되기 때문에 `subtract`는 `undefined`로 초기화됩니다.     
따라서 함수 호출 시 `TypeError`가 발생합니다.   

<br>

## 호이스팅 이해하기
---

호이스팅을 이해하기 위해서는 코드가 실제로 어떻게 실행되는지 생각해 보는 것이 중요합니다.   
예를 들어, 다음 코드를 보겠습니다.    

<br>

```javascript
console.log(a); // undefined
var a = 2;

foo(); // "Hello"

function foo() {
    console.log("Hello");
}
```
<br>

위 코드는 실제로 다음과 같이 실행됩니다:

<br>

```javascript
var a;
function foo() {
    console.log("Hello");
}

console.log(a); // undefined
a = 2;

foo(); // "Hello"
```
<br>

변수 선언 `var a`와 함수 선언 `function foo()`가 코드의 최상단으로 끌어 올려졌습니다.     
따라서 첫 번째 `console.log(a)`는 `undefined`를 출력하고, 함수 `foo`는 정상적으로 호출됩니다.   

<br>

## 호이스팅의 장점과 단점
---

<br>

### 장점
1. **코드 가독성**: 함수 선언을 코드의 어느 위치에서든 사용할 수 있어 가독성이 향상됩니다.
2. **유연성**: 코드 작성 순서에 구애받지 않고 변수와 함수를 사용할 수 있어 유연하게 코드를 작성할 수 있습니다.

### 단점
1. **예측 불가능성**: 호이스팅으로 인해 변수가 `undefined`로 초기화되기 때문에 예기치 않은 결과가 발생할 수 있습니다.
2. **버그 발생 가능성**: 호이스팅을 이해하지 못하면 버그가 발생할 가능성이 높아집니다.

<br>
<br>


## 결론
---

자바스크립트의 호이스팅은 변수와 함수 선언을 최상단으로 끌어 올리는 메커니즘입니다.     
이를 통해 코드의 유연성과 가독성을 높일 수 있지만, 예기치 않은 결과를 초래할 수 있으므로 주의가 필요합니다.     
`let`과 `const`를 사용하면 호이스팅의 영향을 줄이고, 더욱 명확한 코드를 작성할 수 있습니다.   

이 글이 호이스팅을 이해하는 데 도움이 되었기를 바랍니다.
