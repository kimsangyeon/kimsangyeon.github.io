---
layout: post
title: 'Javascript Async Function'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Async Function

`async function` 선언은 AsyncFunction객체를 반환하는 하나의 비동기 함수를 정의합니다. 비동기 함수는 이벤트 루프를 통해 비동기적으로 작동하는 함수로, 암시적으로 Promise를 사용하여 결과를 반환합니다. 그러나 비동기 함수를 사용하는 코드의 구문과 구조는, 표준 동기 함수를 사용하는것과 많이 비슷합니다. <br>
또한 async function expression을 사용해서 async function을 선언할 수 있습니다. <br>

MDN: [Javascript Async Function](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/async_function) <br>

<br><br>

## Async Function 사용

비동기적인 로직을 `async function`을 사용하여 동기적으로 보이도록 직관적인 프로그래밍을 할 수 있습니다. `Promise`를 사용한 비동기 처리 방식이 있지만 `async function` 안쪽에서 비동기 로직을 `await`을 사용하여 제어하는 형태는 직관적인 코드 구성으로 직관적으로 코드를 해석할 수 있도록 도와줍니다. <br>

<br>

### Promise Example

```javascript
function getData() {
  axios.get('http://www.test.com/get/data').then(res => {
    console.log(res);
  });
}
```

위의 간단한 예로 본다면 `Promise`를 사용하여 data를 받아와 callback 함수에서 받아온 response를 출력하고 있습니다. 간단한 예제로 봤을땐 그리 복잡해 보이지 않지만 여러 코드에 해당 형태의 코드가 섞여있고 callback 함수에서 받아온 데이터를 제어하는 형태는 한 뎁스를 더 고려하여 코드를 리딩하여야합니다. 또한 then chain이 여러번 반복되고 catch, finally 까지 추가된다면? 또는 해당형태가 중첩되는 경우 가독성이 현저히 떨어지게 됩니다.

<br>

### Async Await Example

```javascript
async function getData() {
  const res = await axios.get('http://www.test.com/get/data');
  console.log(res);
}
```

위는 `async await`을 사용하여 data를 받아와 response를 출력하는 형태입니다. `Promise`를 사용하여 callback을 사용한 형태와 비교하였을때 같은 레벨에서 response를 출력하는 형태로 훨씬 더 간단하게 비동기 처리가 가능합니다. <br>

<br>

### Generator Example

```javascript
function* getData() {
  const res = yield axios.get('http://www.test.com/get/data');
  console.log(res);
}
```

위에서 보았던 `async await`과 비교했을때 거의 같은 것을 볼 수 있습니다.
