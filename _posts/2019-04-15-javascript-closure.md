---
layout: post
title: "Javascript Closure" 
categories: [ javascript ]
image: assets/images/banner/javascript.png
featured: false
author: yeon
---


## Javascript Closure
클로저란? 클로저는 함수와 함수가 선언된 어휘적 환경의 조합이다.
[참고: MDN Closure](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Closures)

<br>

환경이란 변수들이 포함된 context를 말한다고 한다.

### 클로저 생성
1. 내부함수가 외부함수 변수를 사용할때.
```javascript
function outer() {
    var x = 1;
    function inner() {
        console.log(x); // 1
    }
}
```

2. 익명의 내부함수가 외부함수의 리턴값으로 사용될때.
```javascript
function outer() {
    return function inner() {
        console.log('inner');
    }
}
```


3. 내부함수가 외부함수 실행환경에서 실행될때.
```javascript
function outer() {
    function inner() {
        console.log('inner');
    }

    inner();
}
```

### 스코프 객체 체인 클로저
외부함수의 변수를 사용하는 내부함수가 사용되는 경우, 외부함수가 종료되더라도 내부함수에서 외부함수 변수 사용
```javascript
function outer() {
    var x = 1;
    return function inner() {
        console.log(x);
    }
}

var fn = outer();
fn(); // 1
```

<br><br><br>