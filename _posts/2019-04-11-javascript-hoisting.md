---
layout: post
title: "Javascript Hoisting" 
categories: [ javascript ]
image: assets/images/banner/javascript.png
featured: false
author: yeon
---


## Javascript Hoisting

Javascript라는 언어의 특색중 하나이며, 현재 ES6 문법에서 제공되는 let, const 사용에 의해 크게 신경쓰지 않고 있지만 중요한 요소중 하나 인 것 같다.

> Hoist
끌어 올린다는 뜻이며, Javascript에서 끌어올려지는 변수를 뜻한다. var로 선언된 변수는 끌어올려지며, 호이스트된다고 한다. 기본적으로 선언과 할당을 분리해서 말하는 것을 뜻한다.

### 변수 호이스팅

```javascript
function fn() {
	console.log(a);  // undefined
	var a = 10;     
	conosole.log(a); // 10
}

fn();
```
일반적인 다른 언어에서는 다음과 같은 실행에서 a를 찾지못해 요류가 발생할 것이다. 하지만 자바스크립트에서는 var a 선언이 함수 최상단으로 호이스트 되며 undefined로 출력된다. 이후 a에 10이 할당되며 다음 console에서 10으로 출력된다.

```javascript
function fn() {
	var a;
	console.log(a);
	a = 10;
	console.log(a);
}
```

### 함수 호이스팅
함수 호이스팅은 함수 선언에 대해서 호이스팅을 수행한다.

```javascript
fn(); // hoist;
function() {
	console.log('hoist');
}
```

하지만 함수를 변수에 할당하는 리터럴 구조에서는 함수가 호이스팅 되지 않는다.

```javascript
fn(); // Error fn is not a function
var fn = function() {
	console.log('hoist');
}
```



<br><br><br>