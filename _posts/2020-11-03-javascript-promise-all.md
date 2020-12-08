---
layout: post
title: 'Javascript Promise all & allSettled & race'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Promise all & allSettled & race

Javascript에서 비동기 작업의 처리를 위해 ES6에서의 **Promise**를 사용한다. **Promise**는 비동기 연산이 종료된 이후 결과값이나 실패를 처리하기 위한 처리기를 연결 할 수 있도록 한다. <br>

<br>

## Promise all

위에 간략히 설명한 **Promise**가 여러개 인 경우 하나로 묶어 비동기 연산 이후 결과 혹은 실패 처리를 할 수 있도록 **Promise.all** 메서드를 사용한다. <br>
**Promise.all**은 주어진 **Promise**중 하나라도 거부되는 경우 **reject** 거부 처리된다. <br>

<br><br>

### ex1) Promise.all

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

**Promise.all**은 위에 설명했듯 하나라도 거부하면, 다른 Promise의 여부와는 상관 없이 거부된다.

<br>

### ex2) Promise.all

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

**Promise.all**은 실패 우선성을 띄기 때문에 실패할 수 있는 동작을 앞에두어 사전처리 할 수 있다.

<br><br>

### promise.all의 비동기성

**promise.all**의 실행을 호출 스택 비우기 전과 비우고 난 이후를 비교해보자

```javascript
const promiseList = [Promise.resolve(1), Promise.resolve(2)];
const p = Promise.all(promiseList);

// 실행 즉시 p
console.log(p);

// 호출 스택 이후 p
setTimeout(() => {
  console.log('the stack is now empty');
  console.log(p);
});


// Log
// Promise {<pending>}
// the stack is now empty
// Promise {<fulfilled>: Array(2)}
```

호출스택 이후에 pending에서 fulfilled 상태가 된 것을 확인할 수 있다.
해당 비동기성은 실패한 동작에서도 동일하다.

```javascript
const promiseList = [Promise.resolve(1), Promise.reject(2)];
const p = Promise.all(promiseList);

// 실행 즉시 p
console.log(p);

// 호출 스택 이후 p
setTimeout(() => {
  console.log('the stack is now empty');
  console.log(p);
});


// Log
// Promise {<pending>}
// the stack is now empty
// Promise {<rejected>: 2}
```

<br><br>

### Promise.all Polyfill

```javascript
Promise.all = function ( promises ) {
  return new Promise( function ( fulfil, reject ) {
    var result = [], pending, i, processPromise;

    if ( !promises.length ) {
      fulfil( result );
      return;
    }

    processPromise = function ( i ) {
      promises[i].then( function ( value ) {
        result[i] = value;

        if ( !--pending ) {
          fulfil( result );
        }
      }, reject );
    };

    pending = i = promises.length;
    while ( i-- ) {
      processPromise( i );
    }
  });
};
```

<br><br>

## Promise allSettled

**Promise.all**의 경우에는 하나라도 실패시 실패로 간주되어 처리된다. 이를 개선(?)한 성공과 실패를 나누어 처리하도록 해주는 allSettled가 있다.

<br>

**Promise.allSettled**는 reject으로 수행되는 처리가 있더라도 모든 promise 과정을 수행하여 성공과 실패를 나누어 결과를 반환한다.

<br>

이전에 사용하였던 **ex2) Promise.all** 예제를 보았을때 promise 중 reject 결과가 있는 경우 promise 반환값 상태값은 rejected로 처리된다. 여기서 해당 예제를 **Promise.allSettled**를 사용하여 확인하자.

```javascript
const promiseList = [Promise.resolve(1), Promise.reject(2)];
const p = Promise.allSettled(promiseList);

// 실행 즉시 p
console.log(p);

// 호출 스택 이후 p
setTimeout(() => {
  console.log('the stack is now empty');
  console.log(p);
});


// Log
// Promise {<pending>}
// the stack is now empty
// Promise {<fulfilled>: Array(2)}
// [[PromiseResult]]: Array(2)
//    0: {status: "fulfilled", value: 1}
//    1: {status: "rejected", reason: 2}
```

**Promise.allSettled**를 사용할 경우 reject 되더라도 iterable로 전달받은 Promise를 모두 수행하며, 결과로는 fulfilled와 rejected 상태값을 모두 가진 결과를 가진다.

<br><br>

## Promise.allSettled Polyfill

```javascript
Promise.allSettled = Promise.allSettled || ((promises) => Promise.all(promises.map(p => p
  .then(v => ({
    status: 'fulfilled',
    value: v,
  }))
  .catch(e => ({
    status: 'rejected',
    reason: e,
  }))
)));
```

<br><br>

## Promise.race
`Promise.race`는 all, allSettled와는 다르게 모든 Promise에 대한 결과를 반환하지 않는다. `Promise.race`는 수행되는 Promise 중 가장 빠르게 수행되는 결과만을 반환한다.

<br>

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(resolve, 200, 'time1');
});
const promise2 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'time2');
});
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 10, 'time3');
});

Promise.race([promise1, promise2, promise3]).then((v) => {
  console.log(v);
});
// time3
```
위 같은 경우 가장 빨리 수행되는 'time3'이 반환된다.


<br><br>


[ref]:
- [Promise.allSettled()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled)
- [Promise.all()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

<br><br><br>