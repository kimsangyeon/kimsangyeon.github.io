---
layout: post
title: "Typescript Acynchoronous" 
categories: [ Javascript, typescript ]
image: assets/images/banner/typescript/typescript.png
author: yeon
---

# Typescript Acynchoronous
Javascript는 단일 스레드로 동작하여, 하나의 스레드로 모든 작업을 수행한다면 시간이 많이 소요되는 작업이 있을 경우 오랜시간을 기다려야하는 문제가 발생할 수 있다. 최근 Javascript 새로운 버전이 나올떄마다 비동기적인 코드를 작성할 수 있는 여러 방법들이 나고있다. Typescript 또한 비동기 코드를 쉽게 작성하고 관리할 수 있도록 코드작성을 제공한다.

<br><br><br>

## Typescript Callback Function
Typescript에서도 콜백 함수를 작성 할 수 있도록 제공

```javascript
	function doCallback(name: string, callback: (apps: App[], status: string) => void): void {
		let response: App[];

		callback(response, "Success");
	}
```

<br><br>

### Callback Interface
콜백함수 인터페이스를 작성하여 간결하게 작성 가능

```javascript
	interface ICallback {
		(apps: App[], status: string): void;
	}

	function doCallback(name: string, callback: ICallback): void {
		let response: App[];

		callback(response, "Success");
	}
```


## Typescript Promise
ES2015 이후 제공되는 프로미스를 사용하여 비동기 코드 작성이 가능하다.
- 프로미스를 사용하기 위해서는 tsconfig.json : target 옵션을 ES2015로 설정

```javascript
	let p: Promise<App[]> = new Promise((resolve, reject) => {
		if (status === "Success") {
			resolve(result);
		} else {
			reject(error);
		}
	});
```

Promise 객체가 만들어지고, 성공시 resolve 호출, 실패시 reject을 호출한다.
변수 p 타입은 Promise 객체이며 제네릭 App 배열 타입이다. 즉, 프로미스 성공시 App 배열 타입 결과가 반환된다.

<br><br>

### Promise chaining
프로미스는 then과 catch를 사용하여 코드를 보기 쉽게 작성하는 chaining 가능

```javascript
	let p: Promise<App[]> = new Promise((resolve, reject) => {
		if (status === "Success") {
			resolve(result);
		} else {
			reject(error);
		}
	});

	p.then(apps => () {
		...
	}).catch(error => console.log(error));
```
프로미스 성공시 then 콜백 함수가 실행, 실패시 catch 콜백 함수가 실행된다.


<br><br>

### Async-await
Typescript 1.7.x 버전에서 async-await 기능이 컴파일러 버전 ES2015에서 사용할 수 있도록 도입, 2.x 버전에서 ES5와 ES3 Javascript 버전에서도 지원하도록 변경.

```javascript
	async function doAsyncFunction() {
		console.log('doAsyncFunction 시작');

		await doAwaitFunction();

		console.log('doAsyncFunction 끝');
		return "완료";
	}

	function doAwaitFunction() {
		console.log("doAwaitFunction 호출");
	}

	console.log("Async 함수 호출");
	let a = doAsyncFunction().then(result => console.log(result));
	console.log("Async 할수 완료");

```
~~~
Async 함수 호출
doAsyncFunction 시작
doAwaitFunction 호출
Async 할수 완료
doAsyncFunction 끝
완료
~~~

async 함수가 프로미스 위에서 빌드되어 결국은 프로미스를 반환함.
async 접두어를 붙여 함수 내부에 병렬로 수행되는 부분이 있음을 표시.
await 키워드로 병렬 수행 구간을 표시한다.


<br><br><br>