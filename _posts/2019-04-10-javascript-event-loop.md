---
layout: post
title: "Javascript Event Loop" 
categories: [ javascript ]
image: assets/images/banner/javascript.png
featured: false
author: yeon
---


## Javascript Event Loop

`Javascript Event Loop`는 Javascript Engine의 `Task Queue`의 task들을 관리해주는 역활을 한다.

<br>


### Javascript Engine
`Javascript Engine`은 자바스크립트 코드를 실행하는 인터프리터이며, 
구글에서 개발한 V8을 비롯하여, 애플 사파리 Nitro, 모질라 파이어폭스의 스파이더 몽키 등이 있다고 한다. <br>

Javascript Engine 영역은 크게 세 영역으로 나뉜다.
> Call Stask / Task Queue / Heap

<br>

### Event Loop에서 task 관리

<br>

#### Call stack
`Javascript Engine`은 하나의 스레드에서만 동작하며, 이는 `Call Stack` 역시 하나라는 것이다. 하나의 동작이 완료된 후에 다음 동작을 진행 할 수 있다는 말이다. `Call Stack`에는 하나의 요청만 push 되고 해당 요청의 실행이 끝날시 pop되는 형태이다. <br>


```javascript
function fn1() {
    return "test";
}

function fn2() {
    return fn1();
}

console.log(fn2());

```

해당 Javascript에서 fn2 함수가 호출되며, 해당 요청이 Call Stack에 push, fn2 함수 내부에서 fn1를 호출하며 Call Stack에 push되고 fn1 return시 Call Stack의 fn1이 pop, fn2 return시 Call Stack fn2가 pop되며 하나의 요청이 완료된다. <br>

<br>

#### Heap
Heap은 동적으로 생성된 객체의 메모리 할당이 일어나는 곳이다. Javascript 메모리 모델은 가비지콜렉터를 사용한다고 한다. <br>

<br>

#### Task Queue
Task Queue는 Javascript 런타임 환경에서 자바스크립트가 수행할 Task가 임시로 대기하는 대기 큐이다. <br>
이 대기큐는 Task Queue 혹은 Event Queue라고 부른다. 큐에 대기중인 Task들은 Call Stack이 비워지면 순차적으로 Call Stack으로 들어가 수행된다. <br>

<br>

대게 webApi로 동작하는 setTimeout, setInterval의 callback 함수들이 Task Queue에서 비동기 동작을 수행하기 위해 Call Stack이 비기 까지 대기한다. Promise callback 역시 Task Queue에서 대기하여 비동기 동작을 수행한다.

<br>

```javascript
function fn1() {
    console.log("task1");
    fn2();
}

function fn2() {
    setTimeout(() => {
        console.log("task2");
    }, 0);
    fn3();
}

function fn3() {
    console.log("task3");
}

fn1();
```

<br>

fn1이 실행되며 Call Stack에 push되고 console 수행 "task1"이 콘솔에 찍힌다.<br>
- (Call Stack [fn1] / Task Queue []) 

<br>

fn2가 Call Stack에서 수행되며 push 된다.<br>
- (Call Stack [fn1, fn2] / Task Queue []) 

<br>

setTimeout이 Call Stack에 들어갔다 pop이 되며, setTimeout에 존재하는 Callback 함수가 Task Queue로 들어간다. <br>
- (Call Stack [fn1, fn2] / Task Queue [callback]) 

<br>

이후 fn3이 Call Stack에 push되고 "task3"이 콘솔에 힌다. <br>
- (Call Stack [fn1, fn2, fn3] / Task Queue [callback]) 

<br>

fn3이 동작을 완료하고 반환되며 Call Stack에서 fn3이 pop <br>
- (Call Stack [fn1, fn2] / Task Queue [callback]) 

<br>

fn3을 호출한 fn2도 함수가 완료되고 반환되며 Call Stack에서 pop <br>
- (Call Stack [fn1] / Task Queue [callback]) 

<br>

fn2를 호출한 fn1도 함수가 완료되고 반환되며 Call Stack에서 pop<br>
- (Call Stack [] / Task Queue [callback]) 

<br>

Call Stack이 완전하게 비게되고 Task Queue에 들어갔던 Callback함수가 Call Stack에 들어가 수행된다. <br>
- (Call Stack [callstack] / Task Queue []) 

<br>

"task2"를 콘솔에 찍고 Call Stack에서 pop 된다. <br>
- (Call Stack [] / Task Queue [])

<br>



<br><br><br>