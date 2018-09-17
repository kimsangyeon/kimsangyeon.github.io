---
layout: post
title: "Typescript Iterator" 
categories: [ Javascript, typescript ]
image: assets/images/banner/typescript/typescript.png
author: yeon
---

# Iterator
반복자(iterator)는 객체 지향적 프로그래밍에서 배열이나 그와 유사한 자료 구조의 내부의 요소를 순회(traversing)하는 객체이다. [위키백과]

## Javascript Iterator
Javascript의 문자열 Symbol.iterator 프로퍼티가 존재.
for ... of 에서 객체에 대해 루프를 돌며 출력
```javascript
	let aStr = "javascript iterator";
	for (let c of aStr) {
		console.log(c);
	}
	
```

Symbol.iterator 프로퍼티를 명시적으로 사용
```javascript
	let aStr = "javascript iterator";
	let iter = aStr[Symbol.iterator]();
	console.log(iter.next().value);
```
next 함수는 done과 value 두 값을 가진 객체 반환.


## Typescript Iterator
Typescript에서 문자열 또는 배열의 정의
```javascript
	interface IteratorResult<T> {
		done: boolean;
		value; T;
	}

	interface Iterator<T> {
		next(value?: any): IteratorResult<T>;
		return?(value?: any): IteratorResult<T>;
		throw?(e?: any): IteratorResult<T>;
	}

	interface Iterable<T> {
		[Symbol.iterator](): Iterator<T>;
	}

	interface IterableIterator<T> extends Iterator<T> {
		[Symbol.iterator()]: IterableIterator<T>;
	}

	interface Array<T> {
		[Symbol.iterator](): IterableIterator<T>;
	}

	entries(): IterableIterator<[number, T]>;
```



<br><br><br>