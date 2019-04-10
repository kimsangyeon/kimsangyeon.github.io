---
layout: post
title: "Javascript Event Loop" 
categories: [ javascript ]
image: assets/images/banner/javascrpit.png
featured: false
author: yeon
---


## Javascript Event Loop

Javascript Event Loop는 Javascript Engine의 Task Queue task들을 관리해주는 역활을 한다.

<br>


### Javascript Engine
Javascript Engine은 자바스크립트 코드를 실행하는 인터프리터 이며, 
구글에서 개발한 V8을 비롯하여, 애플 사파리 Nitro, 모질라 파이어폭스의 스파이더 몽키 등이 있다고 한다. <br>

Javascript Engine 영역은 크게 세 영역으로 나뉜다.
> Call Stask / Task Queue / Heap

<br>

### Event Loop에서 task 관리
#### Call stack
Javascript Engine은 하나의 스레드에서만 동작하며, 이는 Call Stack 역시 하나. 하나의 동작이 완료된 후에 다음 동작을 진행 할 수 있다는 말이다. Call Stack에는 하나의 요청만 push 되고 해당 요청의 실행이 끝날시 pop되는 형태이다.


```javascript
function fn1() {
    return "test";
}

function fn2() {
    return fn1();
}

console.log(fn2());

```

해당 Javascript에서 fn2 함수가 호출되며, 해당 요청이 Call Stack에 push, fn2 함수 내부에서 fn1를 호출하며 Call Stack에 push되고 fn1 return시 Call Stack의 fn1이 pop, fn2 return시 Call Stack fn2가 pop되며 하나의 요청이 완료된다.

#### Heap
Heap은 동적으로 생성된 객체가 메모리 할당이 일어나는 곳이다. Javascript 메모리 모델은 가비지콜렉터를 사용한다고 한다.

#### Task Queue
Task Queue는 Javascript 런타임 환경에서 자바스크립트가 수행할 Task가 임시로 대기하는 대기 큐이다. 
이 대기큐는 Task Queue 혹은 Event Queue라고 부른다. 큐에 대기중인 Task들은 Call Stack이 비워지면 순차적으로 Call Stack으로 들어가 수행된다.

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

fn1이 실행되며 Call Stack에서 수행 "task1"이 콘솔에 찍히며 pop. <br>
fn2가 Call Stack에서 수행되며 pop. <br>
setTimeout이 Call Stack에 들어갔다 pop이 되며, setTimeout에 존재하는 Callback 함수가 Task Queue로 들어간다. <br>
이후 fn3이 Call Stack에 들어가 수행되며 task3이 콘솔에 찍히며 pop. <br>
Call Stack에 수행 Task가 존재하지 않아 Task Queue에 들어갔던 Callback함수가 Call Stack에 들어가 수행되며 "task2"를 콘솔에 찍고 Call Stack에서 pop 된다.



<br><br><br>