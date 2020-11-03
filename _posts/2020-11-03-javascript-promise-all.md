---
layout: post
title: 'Javascript Promise all & allSettled'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Promise all & allSettled

Javascript에서 비동기 작업의 처리를 위해 ES6에서의 **Promise**를 사용한다. **Promise**는 비동기 연산이 종료된 이후 결과값이나 실패를 처리하기 위한 처리기를 연결 할 수 있도록 한다. <br>

<br>

## Promise all

위에 간략히 설명한 **Promise**가 여러개 인 경우 하나로 묶어 비동기 연산 이후 결과 혹은 실패 처리를 할 수 있도록 **Promise.all()** 메서드를 사용한다. <br>
**Promise.all()**은 주어진 **Promise**중 하나라도 거부되는 경우 **reject** 거부 처리된다. <br>

<br><br>

### ex) Promise.all()

```javascript
const promise1 = 10;
const promise2 = Promise.resolve(3);
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'time');
});

Promise.all([promise1, promise2, promise3]).then((v) => {
  console.log(v);
});
// [10, 3, 'time']
```

<br><br>

~~~
Promise.all(iterable);
~~~

**Promise.all**은 순회 가능한 iterable 객체를 받는다. ex) Array

<br>

**Promise.all()**은 위에 설명했듯 하나라도 거부하면, 다른 Promise의 여부와는 상관 없이 거부된다.

<br>

### ex)

```javascript
const promise1 = 10;
const promise2 = Promise.resolve(3);
const promise3 = new Promise((resolve, reject) => {
  setTimeout(reject, 100, 'time');
});

Promise.all([promise1, promise2, promise3]).then((v) => {
  console.log(v);
});

// Error Uncaught (in promise) time
```

<br>

**Promise.all()**은 실패 우선성을 띄기 때문에 실패할 수 있는 동작을 앞에두어 사전처리 할 수 있습니다.

<br><br>