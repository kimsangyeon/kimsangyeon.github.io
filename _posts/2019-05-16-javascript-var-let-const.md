---
layout: post
title: "Javascript var let const" 
categories: [ javascript ]
image: assets/images/banner/javascript.png
featured: false
author: yeon
---


## Javascript var let const
Javascript 선언식인 var let const를 정리해본다.

<br>

### 선언방식
var는 일반적으로 Javascript에서 사용하던 선언, ES6이후 let const 선언방식이 등장 <br>
var는 함수 단위 스코프를 가지며, let과 const는 블록단위 스코프를 가진다. <br>

<br>

var let const에 관한 호이스팅에 헷갈림을 정리하였다. var let const 모두 호이스팅이 되지만, 선언과 초기화에 나눔이 다르다.
var는 호이스팅이되며 선언과 동시에 호이스팅이 되지만, let const는 호이스팅후 선언은 되지만 초기화는 되지 않는다.

#### var hoisting

```javascript
console.log(a);

var a = 'javascript';
```
다음 코드를 실행시 undefined가 출력. var는 호이스팅되며 선언, 초기화를 수행하였기 때문

<br>

#### let const hoisting

```javascript
console.log(a);

let a = 'javascript'; // const a = 'javascript';
```

let, const 의 경우 호이스팅후 선언만 이루어지고 초기화가 되지 않았기 때문에

~~~
Uncaught ReferenceError: Cannot access 'a' before initialization
~~~

다음과 같은 에러를 출력한다.

<br>

#### TDZ Temporal Dead Zone
TDZ는 변수가 선언은 되었지만 초기화되지 않은 영역을 말하며, let과 const 호이스팅스 TDZ가 생성되어 선언만 이루어진다.


<br>

#### var scope

```javascript
(function() {
    if (true) {
        var a = 'kim';
    }
    console.log(a);
})();
console.log(a);
```
다음 코드를 실행시 var는 함수 스코프이기 때문에 함수 안쪽 console에서 'kim'을 출력한다. <br>
하지만 함수 바깥쪽 console에서는 ReferenceError를 출력한다.

<br>

#### let const scope

```javascript
(function() {
    if (true) {
        let a = 'kim';  // const a = 'kim';
    }
    console.log(a);
})();
console.log(a);
```
다음 코드를 실행시 let const은 블록 스코프이기 때문에 함수 안쪽 console에서 ReferenceError를 출력한다. <br>

<br>


<br><br><br>