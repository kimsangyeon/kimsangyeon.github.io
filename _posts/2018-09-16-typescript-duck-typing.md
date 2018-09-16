---
layout: post
title: "Typescript Duck typing" 
categories: [ Javascript, typescript ]
image: assets/images/banner/typescript/typescript.png
author: yeon
---

# Typescript Duck typing
컴퓨터 프로그래밍에서 Duck typing은 Duck Test와 같은 응용 프로그램입니다. "어떤새가 오리와 같이 걷고 오리처럼 꽥꽥거리는 소리를 낸다면, 그 새는 오리라고 불릴 것이다."- 명제를 통해 대상을 확인하는 과정. 객체의 적합성은 객체 자체의 유형보다는 특정 메소드 및 속성의 존재에 의해 결정 됩니다.

```javascript
interface IDuck {
	walk: string;
	sound: string;

	formatData(): void;
}

class Duck {
	walk: string;
	sound: string;

	formatData(): void {}
}


function duckCage (duck: IDuck) {}

let donald = new Duck();
duckCage(donald);
```

Duck typing의 예로, 인터페이스 IDuck과 동일한 프로퍼티와 메소드를 가진 Duck 클래스.
Duck 클래스를 IDuck 인터페이스 타입으로 선언하지 않았지만, duckCage에서 받은 메개변수에서 Duck 객체를 IDuck으로 허용


<br><br><br>