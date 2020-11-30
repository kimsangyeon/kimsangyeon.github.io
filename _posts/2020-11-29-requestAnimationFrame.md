---
layout: post
title: 'requestAnimationFrame'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# requestAnimationFrame

**requestAnimationFrame**은 브라우저에게 다음에 수행할 애니메이션을 알려 브라우저 리페인트가 좀 더 원활하게 동작할 수 있게 한다. <br>
해당 메소드는 다음으로 실행할 메소드를 콜백인자로 받으며 연속된 애니메이션을 수행하기 위해서는 해당 메소드 내부에서 재귀 호출이 필요하다. <br>

<br>

화면이 새로운 애니메이션을 업데이트할 준비가 될때마다 메소드를 호출하는 것이 좋다. <br>
일반적으로 콜백의 수는 보통 1초에 60회인 60fps를 선호한다.(대략 16ms에 1번) **requestAnimationFrame**은 호출시 디스플레이 주사율에 맞추어 수행되며 해당 호출은 백그라운드 탭이나 hidden iframe에서는 실행을 중단하여 성능과 배터리 수명향상에 도움을 준다. <br>

<br>

```jsx
window.requestAnimationFrame(callback);
```

<br><br>

#### parameter

callback : 다음 리페인트때 애니메이션을 수행할 함수 <br>
callback 함수가 실행될 시점에는 performance.now()에 의해 반환되는 값과 유사한 DOMHighResTimeStamp 단일 인자가 전달된다. <br>

<br>

- [ ]  DOMHighResTimeStamp

double 밀리 세컨드 시간 값이며 개별 시점 또는 시간 간격을 계산할때 사용할 수 있다. <br>
시간의 시작은 문서의 수명의 시작으로 간주되는 표준 시간이다. <br>
(해당값은 performance.now() 값으로도 구할 수 있다.) <br>

<br>

#### return

고유한 id 값이 반환되며 이 값으로 window.cancelAnimationFrame()을 호출하여 콜백 요청을 취소할 수 있다. <br>

<br><br>

## example

```jsx
let start = null;
let element = document.getElementById('test');
element.style.position = 'absolute';

function step(timeStamp) {
	if (!start) start = timeStamp;
	const progress = timestamp - start;
	element.style.left = Math.min(progress / 10, 2000) + 'px';
	if (progress < 2000) {
		window.requestAnimationFrame(step);
	}
}

window.requestAnimationFrame(step);
```

<br><br>

### requestAnimationFrame Polyfill

현재시간에서 지난 시간을 계산하여 callback의 인자로 DOMHighResTimeStamp를 넘겨주고 setTimeout을 16ms 안으로 실행되도록 한다. 계산시 16ms 보다 시간이 경과한 경우 setTimeout ms를 0으로 설정한다.<br>

```jsx
(function() {
    var lastTime = 0;
    var vendors = ['ms', 'moz', 'webkit', 'o'];
    for(var x = 0; x < vendors.length && !window.requestAnimationFrame; ++x) {
        window.requestAnimationFrame = window[vendors[x]+'RequestAnimationFrame'];
        window.cancelAnimationFrame = window[vendors[x]+'CancelAnimationFrame'] 
                                   || window[vendors[x]+'CancelRequestAnimationFrame'];
    }
 
    if (!window.requestAnimationFrame)
        window.requestAnimationFrame = function(callback, element) {
            var currTime = new Date().getTime();
            var timeToCall = Math.max(0, 16 - (currTime - lastTime));
            var id = window.setTimeout(function() { callback(currTime + timeToCall); }, 
              timeToCall);
            lastTime = currTime + timeToCall;
            return id;
        };
 
    if (!window.cancelAnimationFrame)
        window.cancelAnimationFrame = function(id) {
            clearTimeout(id);
        };
}());
```

<br><br><br>

[ref]:
- [window.requestAnimationFrame()](https://developer.mozilla.org/ko/docs/Web/API/Window/requestAnimationFrame)
- [requestAnimationFrame polyfill rAf.js](https://gist.github.com/paulirish/1579671)

<br><br><br>