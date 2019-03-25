---
layout: post
title: "The canvas put point part2" 
categories: [ git, github, canvas ]
image: assets/images/banner/canvas.png
featured: false
author: yeon
---


#### canvas put point part2

canvas에 이벤트를 활용하여 간단한 그리기 도구 만들기

<br>

##### canvas addEventListener
mousedown move up을 활용하여 put point

<br>

###### mousedown

```javascript
var isDraw = false;
var fnMouseDown = (e) => {
    isDraw = true;
    putPoint(e);
};

canvas.addEventListener('mousedown', fnMouseDown);
```

mousedown 이벤트에서 isDraw 그리기 시작 변수 true <br>
putPoint 호출하여 그리기

<br>

###### mousemove

```javascript
var putPoint = (e) => {
    if (isDraw) {
        ctx.lineTo(e.clientX, e.clientY);
        ctx.stroke();
        ctx.beginPath();
        ctx.arc(e.clientX, e.clientY, radius, 0, Math.PI * 2);
        ctx.fill();
        ctx.beginPath();
        ctx.moveTo(e.clientX, e.clientY);
    }
};
canvas.addEventListener('mousemove', putPoint);
```

lineTo, arc, moveTo 활용하여 그리기
putPoint mousemove 이벤트 등록

<br>

###### mouseup

```javascript
var fnMouseUp = (e) => {
    isDraw = false;
    ctx.beginPath();
};
```

isDraw 그리기 시작 변수 false <br>
canvas path 초기화

- ctx.beginPath(): 경로 목록을 비워 새 경로를 시작

<br><br><br>