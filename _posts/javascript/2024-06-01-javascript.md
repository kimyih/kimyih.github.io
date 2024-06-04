---
layout: post
title: 자바스크립트 - 스코프(Scope)란?
date: 2024-06-01 17:00 +0900
description: Javascript
image: ../assets/img/Javascript.png
category: Javascript
tags: Javascript
published: true
sitemap: true
---

# 스코프(Scope)란 무엇인가?

프로그래밍에서 스코프(Scope)는 매우 중요한 개념입니다.     
스코프는 변수에 접근할 수 있는 범위를 의미합니다.     
즉, 특정 변수에 접근할 수 있는 코드의 영역을 말합니다.     
스코프는 프로그램의 가독성을 높이고, 변수 충돌을 방지하며, 코드의 구조를 이해하는 데 도움을 줍니다.    
스코프는 크게 두 가지 타입으로 나눌 수 있습니다.     
전역 스코프(global scope)와 지역 스코프(local scope).    
이번 글에서는 이 두 가지 타입의 스코프에 대해 자세히 알아보겠습니다.   

<br>

## 전역 스코프 (Global Scope)
---

전역 스코프는 프로그램의 모든 영역에서 접근할 수 있는 변수를 의미합니다.    
전역 변수는 함수나 블록 밖에서 선언되며, 어디에서든지 접근할 수 있습니다.     
이는 전역 객체의 속성으로 간주됩니다.   
전역 변수는 프로그램의 전체에서 사용될 수 있기 때문에 매우 편리하지만, 잘못 사용하면 변수 충돌이나 의도치 않은 변경이 발생할 수 있습니다.   

<br>

### 전역 변수의 예

```javascript
var globalVariable = "나는 전역 변수입니다.";

function showGlobalVariable() {
    console.log(globalVariable); // "나는 전역 변수입니다."
}

showGlobalVariable();
console.log(globalVariable); // "나는 전역 변수입니다."
```

위 예제에서 `globalVariable`은 함수 안팎에서 모두 접근할 수 있는 전역 변수입니다.    
전역 변수는 프로그램 전체에서 접근할 수 있기 때문에 편리하지만, 코드가 복잡해지면 의도치 않은 변경이나 충돌이 발생할 수 있습니다.   

<br>

### 전역 변수의 주의사항

전역 변수는 프로그램 전체에서 접근할 수 있기 때문에, 의도치 않은 변경이나 충돌이 발생할 수 있습니다.    
따라서, 전역 변수를 최소화하고, 가능하면 지역 변수를 사용하는 것이 좋습니다.     
전역 변수가 많아지면 코드의 복잡성이 증가하고, 유지보수가 어려워질 수 있습니다.   

<Br>

## 지역 스코프 (Local Scope)

지역 스코프는 특정 코드 블록이나 함수 내부에서만 접근할 수 있는 변수를 의미합니다.    
지역 변수는 함수나 블록 내부에서 선언되며, 해당 영역을 벗어나면 접근할 수 없습니다.    
이는 변수의 사용 범위를 제한하여, 코드의 가독성을 높이고, 변수 충돌을 방지합니다.   

<br>

### 지역 변수의 예

```javascript
function showLocalVariable() {
    var localVariable = "나는 지역 변수입니다.";
    console.log(localVariable); // "나는 지역 변수입니다."
}

showLocalVariable();
console.log(localVariable); // ReferenceError: localVariable is not defined
```

위 예제에서 `localVariable`은 함수 내부에서만 접근할 수 있는 지역 변수로, 함수 외부에서는 접근할 수 없습니다.   

<br>

## 블록 스코프 (Block Scope)
---

ES6(ECMAScript 2015)에서 도입된 `let`과 `const` 키워드는 블록 스코프를 지원합니다.   
블록 스코프는 중괄호 `{}`로 감싸진 코드 블록 내에서만 유효한 변수를 의미합니다.    
이를 통해 변수를 더욱 안전하게 관리할 수 있습니다.   

<Br>

### 블록 스코프의 예

```javascript
if (true) {
    let blockVariable = "나는 블록 변수입니다.";
    console.log(blockVariable); // "나는 블록 변수입니다."
}

console.log(blockVariable); // ReferenceError: blockVariable is not defined
```

위 예제에서 `blockVariable`은 `if` 블록 내부에서만 유효하며, 블록 외부에서는 접근할 수 없습니다.    
`const` 키워드도 동일한 방식으로 작동합니다.   

<Br>
 
## 함수 스코프와 블록 스코프의 차이

전통적인 자바스크립트에서는 `var` 키워드를 사용하여 변수를 선언하면 함수 스코프를 가집니다.     
그러나 `let`과 `const` 키워드는 블록 스코프를 가지므로, 중괄호 `{}` 내부에서만 유효합니다.   

<Brr>

### 함수 스코프의 예

```javascript
function functionScope() {
    var functionVariable = "나는 함수 변수입니다.";
    if (true) {
        var functionVariable = "나는 함수 변수입니다.";
        console.log(functionVariable); // "나는 함수 변수입니다."
    }
    console.log(functionVariable); // "나는 함수 변수입니다."
}

functionScope();
```

위 예제에서 `var` 키워드로 선언된 `functionVariable`은 함수 스코프를 가지며, 블록 내외에서 동일한 변수로 간주됩니다.   

<Br>

## 스코프 체인 (Scope Chain)

스코프 체인은 변수를 찾을 때 스코프가 중첩된 구조를 따라 상위 스코프를 차례로 검색하는 과정을 의미합니다.    
자바스크립트는 변수 참조를 위해 현재 스코프에서 변수를 찾고, 없으면 상위 스코프로 이동하여 변수를 찾습니다. 최상위 스코프는 전역 스코프입니다.   

<br>

### 스코프 체인의 예

```javascript
var globalVariable = "나는 전역 변수입니다.";

function outerFunction() {
    var outerVariable = "나는 외부 함수 변수입니다.";

    function innerFunction() {
        var innerVariable = "나는 내부 함수 변수입니다.";
        console.log(globalVariable); // "나는 전역 변수입니다."
        console.log(outerVariable); // "나는 외부 함수 변수입니다."
        console.log(innerVariable); // "나는 내부 함수 변수입니다."
    }

    innerFunction();
}

outerFunction();
```

위 예제에서 `innerFunction`은 `globalVariable`과 `outerVariable`을 참조할 수 있으며, 이를 통해 스코프 체인을 이해할 수 있습니다.   

<br>

## 결론



| 특징           | 전역 스코프 (Global Scope)                                      | 블록 스코프 (Block Scope)                                         |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------|
| 선언 위치      | 함수나 블록 밖에서 선언                                        | 중괄호 `{}` 내부에서 선언                                        |
| 접근 가능 범위 | 프로그램 전체                                                   | 선언된 블록 내부                                                  |
| 유효 범위      | 프로그램의 모든 부분에서 유효                                   | 선언된 블록 내에서만 유효                                         |
| 변수 키워드    | `var` (전통적인 자바스크립트)                                    | `let`, `const` (ES6 이후)                                         |
| 변수 중복 선언 | 허용 (하지만, 나중에 선언된 변수로 덮어씌워짐)                  | 허용하지 않음 (동일 블록 내에서는 중복 선언 불가)                 |
| 사용 예        | 전역 설정, 전역 상태 관리 등                                    | 루프 변수, 조건문 내 변수 등                                      |
| 변수 초기화    | 프로그램이 시작될 때 초기화                                     | 블록이 실행될 때 초기화                                           |
| 메모리 관리    | 프로그램이 종료될 때까지 유지                                   | 블록이 종료되면 메모리에서 해제                                   |

<br>
<br>

스코프는 변수에 접근할 수 있는 범위를 의미하며, 전역 스코프와 지역 스코프로 나눌 수 있습니다.     

**전역 변수**는 프로그램의 모든 영역에서 접근할 수 있지만, 의도치 않은 변경이나 충돌이 발생할 수 있으므로 주의가 필요합니다.     

반면, **지역 변수**는 특정 코드 블록이나 함수 내부에서만 유효하며, 블록 스코프를 사용하면 더욱 안전하게 변수를 관리할 수 있습니다.     

스코프 체인을 통해 변수를 참조하는 과정을 이해하면, 더욱 효율적이고 안정적인 코드를 작성할 수 있습니다.    

