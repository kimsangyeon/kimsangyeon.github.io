---
layout: post
title: 'Coroutine Event Loops in Javascript'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Coroutine Event Loops in Javascript

ECMAScript 6 (es6)에는 생성자 및 코루틴을 구현하기위해 yield 키워드가 도입되었습니다. 코루틴은 콜백 함수의 대안으로 이벤트 루프를 구현하는 것이며 좀 더 우아한 로직을 구현할 수 있도록 도와줍니다. <br>

<br><br>

## The Basics

코루틴은 **function\*** 구문으로 표시되는 함수이며 **yield** 키워드를 사용하여 실행중 원하는 위치에서 일지중지 할 수 있는 기능을 제공합니다. **function\*** 함수 실행시 **generator**가 생성되며, 생성된 **generator**의 **next()** 메소드 실행시 **iterator**가 반환됩니다. 반환된 **iterator**의 value는 **yield**에서 일시 중지 된 값이 담겨 반환되며 **iterator**의 마지막값인지 여부를 나타내는 done (boolean)값도 함께 반환됩니다. 코루틴을 다시 실행시 next() 메소드에 값을 할당 할 경우 다음 코루틴에서 할당받은 값을 yield 에서 반환받아 다음 코루틴 로직이 실행됩니다. <br>

<br><br>

### Coroutine Example

간단한 코루틴 예제입니다. <br>

```javascript
function* test() {
  console.log('Hello!');
  const x = yield;
  console.log('First I got: ' + x);
  const y = yield;
  console.log('Then I got: ' + y);
}

const tester = test();

tester.next(); // prints 'Hello!'
tester.next('a cat'); // prints 'First I got: a cat'
tester.next('a dog'); // prints 'Then I got: a dog'
```

<br>

앞서 설명하였든 코루틴을 next() 메소드로 실행하며 다음 코루틴에 사용할 string을 주입하여 다음 코루틴에서 사용해보았습니다. <br>

<br><br>

## The Convenient coroutine Wrapper

코루틴 사용에는 항상 세가지 동작을 수행합니다.

1. function\* 함수를 호출하고 코루틴(generatgor) 객체를 생성합니다.
2. 코루틴에서 next() 메소드를 호출하여 첫번째 yield까지 실행합니다.
3. 다시 실행되는 코루틴에 next(...) 값을 보내 실행합니다.

다음은 코루틴을 wrapper로 감싸 코루틴을 대신 호출해주는 함수를 생성하는 예제입니다. <br>

```javascript
function coroutine(f) {
  const o = f(); // instantiate the coroutine
  o.next(); // execute until the first yield
  return function(x) {
    o.next(x);
  };
}

const test = coroutine(function*() {
  console.log('Hello!');
  const x = yield;
  console.log('First I got: ' + x);
  const y = yield;
  console.log('Then I got: ' + y);
});
// prints 'Hello!'

test('a dog'); // prints 'First I got: a dog'
test('a cat'); // prints 'Then I got: a cat'
```

이전에 생성하였던 예제를 coroutine wrapper로 감싸 코루틴을 보다 쉽게 사용합니다. <br>

<br><br>

## A Coroutine Loop

다음은 무한으로 실행되는 코루틴을 만들어보는 예제입니다. <br>

```javascript
const clock = coroutine(function*() {
  while (true) {
    yield;
    console.log('Tick!');
    yield;
    console.log('Tock!');
  }
});

clock(); // prints 'Tick!'
clock(); // prints 'Tock!'
clock(); // prints 'Tick!'

setInterval(clock, 1000);
```

다음과 같이 코루틴을 사용하여 setInterval로 1초마다 실행시 1초마다 시간을 출력하는 시계도 쉽게 구현이 가능 할 것입니다. <br>

<br><br>

## A Coroutine Event Loop

코루틴을 이벤트의 콜백으로 사용할 수 있습니다. 다음 예는 네모 상자를 드래그하는 예입니다. <br>

1. 상자에서 mousedown 을 기다립니다.
2. mouseown이후 mousemove 이벤트를 처리하고 실제로 상자를 움직입니다.
3. mouseup 이벤트가 발생하기까지 상자가 움직입니다.

<br>

```javascript
   const loop = coroutine(function\*() {
   const event;
   while (event = yield) { // wait for a mousedown
   if (event.type == 'mousedown') {
   while (event = yield) { // process mousemoves until a mouseup
   if (event.type == 'mousemove') move(event);
   if (event.type == 'mouseup') break;
   }
   }
   }
   });
```

yield를 while의 조건으로 설정하여 event를 받아와 다음 코루틴 동작을 수행하도록 합니다. <br>

콜백으로 구현한 이벤트 루프와 비교해봅시다. <br>

```javascript
let dragging = false;
function mousedown(e) {
  dragging = true;
}
function mousemove(e) {
  if (dragging) move(e);
  else {
    // ignore mousemoves
  }
}
function mouseup(e) {
  dragging = false;
}

$('#box').mousedown(mousedown);
$(window)
  .mousemove(mousemove)
  .mouseup(mouseup);
```

두개의 차이점으로는 코루틴을 사용할 경우 코루틴에서는 정지된 상태와 다시 시작 단계가 나눠지므로 해당상태를 기억해야하는 불필요한 변수 할당은 없을 수 있습니다. <br>

<br>

위에서 보았던 시계를 예로 들자면

```javascript
const clock = coroutine(function*() {
  while (true) {
    yield;
    console.log('Tick!');
    yield;
    console.log('Tock!');
  }
});
```

<br>

코루틴의 경우 yield로 정지하고 tick, tock을 순차적으로 실행 <br>

```javascript
let ticking = true;
const clock = function() {
  if (ticking) console.log('Tick!');
  else console.log('Tock!');
  ticking = !ticking;
};
```

일반 함수로 구현하게 되는 경우 ticking에 대한 상태 체크가 필요합니다. <br>

<br><br>

[참고][coroutine event loop in javascript](https://x.st/javascript-coroutines/)

<br><br><br>
