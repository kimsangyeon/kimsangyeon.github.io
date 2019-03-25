---
layout: post
title: "The canvas put point part1" 
categories: [ git, github, canvas ]
image: assets/images/banner/canvas.png
featured: false
author: yeon
---


#### canvas put point part1

canvas에 이벤트를 활용하여 간단한 그리기 도구 만들기

<br>

##### canvas tag

```HTML
<canvas id="canavs"></canvas>
```


##### canvas get context
id canvas를 할당한 tag 생성

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");
```

canvas를 가져와 context 가져오기


##### canvas addEventListener

```javascript
var putpoint = (e) => {

};
canvas.addEventListener('mousedown', putpoint);
```

event를 수행할 pupoint 함수 생성후 canvas에 이벤트 mousedown 등록

##### draw point

```javascript
var radius = 10;
var putpoint = (e) => {
    ctx.beginPath();
    ctx.arc(e.offsetx, e.offsetY radius, 0, Math.PI * 2);
    ctx.fill();
};
```

context arc를 활용하여 좌표에 맞게 원 그리기



<br><br><br>