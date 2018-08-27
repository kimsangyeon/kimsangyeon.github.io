---
layout: post
title: "TypeScript start 01"
categories: [ Javascript, typescript ]
image: assets/images/banner/typescript/typescript.png
author: yeon
---

# TypeScript 란?
타입스크립트는 자바스크립트의 슈퍼셋인 오픈소스 프로그래밍 언어다. 마이크로소프트에서 개발, 유지하고 있으며 엄격한 문법을 지원한다. C#의 리드 아키텍트이자 델파이, 터보 파스칼의 창시자인 Anders Hejlsberg가 개발에 참여한다. 클라이언트 사이드와 서버 사이드를 위한 개발에 사용할 수 있다. 타입스크립트는 자바스크립트 엔진을 사용하면서 커다란 애플리케이션을 개발할 수 있게 설계된 언어다. 위키백과
## TypeScript
- 크로스 플랫폼 언어
- 복잡성을 관리 정적타입 결정 모듈 및 클래스를 사용한 캡슐화 사용자 정의 타입 인터페이스 기능 제공

## Javascript 문제
#### 타입유추 (Type Inference)
Javascript는 동적으로 타입을 결정하여 컴파일 중에 타입 불일치가 발생하여도 오류가 발생하지 않는다.
이는 동일 변수에 문자열 숫자 배열 객체를 할당할 수 있는 Javascript는 런타임 중에 확인을 해야한다는 것이다
```javascript
var num = 1;
num += 1;
console.log(typeof(num)); // number
console.log(num);         // 2

num = 'str';
console.log(typeof(num));  // string
num += 1;                  // str1
```

#### 배열 (Array)
배열 변수가 정의되어있고, 그 변수가 다른 요소로 재할당 되었을 경우 런타임중 오류 발생
```javascript
var score = [1, 2, 3, 4, 5, 6];
console.log(score.slice(2, 4));

score = 10;
console.log(score.slice(2, 4)); // Uncaught TypeError: a.slice is not a function
```

#### 동등비교 (Equality comparision)
'1' 다음과 같이 문자열로 선언된 수일 경우 상수와 비교시 Javascript는 자동으로 문자열을 숫자로 변환하여 비교를 시도한다.
=== 으로 비교시 Javascript는 변수의 타입을 강제로 변환하지 않는다.
```javascript
var num = '1';
console.log(num == 1);  // true
console.log(num === 1); // false
```

#### Null & undefined
Javascript는 null과 undefined를 변수에 할당 할 수 있다.
이러한 변수는 변수에 접근할때 마다 유효성 검사를 해주어야 한다.
'null is not a function, undefined is not a function, Uncaught TypeError: Cannot read property 'a' of null'
Javascript에서는 변수나 함수 또는 null에 접근하지 못하도록 하는 검사방법이 제공되지 않는다.

<br><br><br>
