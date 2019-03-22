---
layout: post
title: "The canvas shadow" 
categories: [ git, github, canvas ]
image: assets/images/banner/canvas.png
featured: false
author: yeon
---


#### shadow
canvas에서 제공하는 그림자 속성을 사용하여 그림자 그리기 <br>

<br>

shadowOffsetX = float
- 그림자가 객체에서 연장되어야 하는 수평거리 (기본값: 0)

shadowOffsetY = float
- 그림자가 객체에서 연장되어야 하는 수직거리 (기본값: 0)

shadowBlur = float
- 흐림(blur) 효과의 크기 (기본값: 0)

shadowColor = color
- 그림자 효과의 색상 (기본값: black)

<br>

```javascript
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  ctx.shadowOffsetX = 2;
  ctx.shadowOffsetY = 2;
  ctx.shadowBlur = 2;
  ctx.shadowColor = "rgba(0, 0, 0, 0.5)";
 
  ctx.font = "20px Times New Roman";
  ctx.fillStyle = "Black";
  ctx.fillText("Sample String", 5, 30);
}
```

![shadow Image]({{ site.baseurl }}/assets/images/canvas_shadow.png)

<br>

<br><br><br>