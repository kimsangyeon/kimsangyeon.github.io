---
layout: post
title: "Nodejs Event loop" 
categories: [ javascript, nodejs ]
image: assets/images/banner/javascript.png
featured: false
author: yeon
---

## node js event loop

node js는 이벤트 기반의 플랫폼. <br>
[libuv](https://github.com/libuv/libuv)라는 라이브러리가 이벤트 루프 기능을 제공 <br>

<br>

이벤트 어플리케이션에서 이벤트를 대기하는 메인루프가 있다. <br>
node js event loop는 옵저버 패턴에 의해 작동되며, 이벤트가 감지 되었을때 Callback 함수를 호출한다. <br>
이벤트를 대기하는 함수들이 옵저버 역할을 하며 이벤트를 기다리다가 이벤트가 실행되면 이벤트를 처리하는 함수 실행 <br>

<br>

#### observer pattern

[옵저버 패턴(observer pattern)](https://ko.wikipedia.org/wiki/%EC%98%B5%EC%84%9C%EB%B2%84_%ED%8C%A8%ED%84%B4)은 객체의 상태 변화를 관찰하는 관찰자들, 즉 옵저버들의 목록을 객체에 등록하여 상태 변화가 있을 때마다 메서드 등을 통해 객체가 직접 목록의 각 옵저버에게 통지하도록 하는 디자인 패턴이다. 주로 분산 이벤트 핸들링 시스템을 구현하는 데 사용된다. 발행/구독 모델로 알려져 있기도 하다. <br>

<br>

### Event loop thread

Javascript 실행 스레드는 단 하나이며, 이벤트 루프가 실행되는 스레드이다. <br>
Node js에서 실행되는 사용자 코드는 전부 콜백이며, 이벤트 루프에 의해 수행된다. <br>

<br>

이벤트루프는 round-robin 방식으로 차례차례 돌면서 처리되는 특정 작업들의 단계들로 이루어져있다. <br>
위에서 얘기한 libuv는 윈도우 커널, 리눅스 커널을 추상화해서 만들어졌다. <br>
node js는 libuv 위에서 동작하고 있으며 node js가 뜰때 libuv에는 스레드풀이(워커 스레드4개) 생성된다고한다. <br>

<br>

### 이벤트루프 단계

- timers : setTimeout(), setInterval() 등 타이머 콜백 처리
- I/O callbak: 클로즈, 타이머 등의 다른 콜백을 제외한 거의 모든 콜백을 수행 (http, apiCall, DB read 등등)
- poll: poll 큐에 있는 이벤트, 콜백들을 처리
- check: setImmediate 콜백 호출 수행
- close: on('close' 처리

<br>

<br><br><br>