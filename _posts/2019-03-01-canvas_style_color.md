---
layout: post
title: "The canvas style color" 
categories: [ git, github, canvas ]
image: assets/images/banner/canvas.png
featured: false
author: yeon
---


### The canvas style color
canvas 도형에 색 및 스타일을 적용하는 방법 <br>

#### canvas color
캔버스 도형에 색적용을 위해 context fillStyle, strokeStyle을 사용하여 색을 지정할 수 있다. <br>

- ctx.fillStyle = color
- ctx.strokeStyle = color

<br>

##### fillStyle
여러가지 형태로 style 색상 지정 가능
```javascript
ctx.fillStyle = "orange";
ctx.fillStyle = "#FFA500";
ctx.fillStyle = "rgb(255, 165, 0)";
ctx.fillStyle = "rgba(255, 165, 0, 1)";
```

<br>

반복문을 사용하여 파레트 형태의 색상 나열
```javascript
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  for (var i = 0; i < 6; i++){
    for (var j = 0; j < 6; j++){
      ctx.fillStyle = 'rgb(' + Math.floor(255 - 42.5 * i) + ', ' +
                       Math.floor(255 - 42.5 * j) + ', 0)';
      ctx.fillRect(j*25,i*25,25,25);
    }
  }
}
```

![fillStyle Image]({{ site.baseurl }}/assets/images/canvas_fillstyle.png)

<br><br><br>