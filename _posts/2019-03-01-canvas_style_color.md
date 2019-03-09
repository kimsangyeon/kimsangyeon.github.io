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

<br>

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

<br>

##### strokeStyle
여러가지 형태로 style 색상 지정 가능
```javascript
ctx.strokeStyle = "orange";
ctx.strokeStyle = "#FFA500";
ctx.strokeStyle = "rgb(255, 165, 0)";
ctx.strokeStyle = "rgba(255, 165, 0, 1)";
```

반복문을 사용하여 파레트 형태의 색상 나열
```javascript
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  for (var i = 0; i < 6; i++) {
    for (var j = 0; j < 6; j++) {
      ctx.strokeStyle = 'rgb(0, ' + Math.floor(255 - 42.5 * i) + ', ' + 
                       Math.floor(255 - 42.5 * j) + ')';
      ctx.beginPath();
      ctx.arc(12.5 + j * 25, 12.5 + i * 25, 10, 0, Math.PI * 2, true);
      ctx.stroke();
    }
  }
}
}
```

![strokeStyle Image]({{ site.baseurl }}/assets/images/canvas_strokestyle.png)

<br>

##### globalAlpha
윤곽선 또는 채움 스타일에 반투명 설정

<br>

strokeStyle과 fillStyle도 rgba 값으로 투명색 적용 가능
```javascript
// 외곽선과 채움 스타일에 투명 적용

ctx.strokeStyle = 'rgba(255, 0, 0, 0.5)';
ctx.fillStyle = 'rgba(255, 0, 0, 0.5)';
```

global Alpha 예제
```javascript
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');
  // 배경을 그린다
  ctx.fillStyle = '#FD0';
  ctx.fillRect(0, 0, 75, 75);
  ctx.fillStyle = '#6C0';
  ctx.fillRect(75, 0, 75, 75);
  ctx.fillStyle = '#09F';
  ctx.fillRect(0, 75, 75, 75);
  ctx.fillStyle = '#F30';
  ctx.fillRect(75, 75, 75, 75);
  ctx.fillStyle = '#FFF';

  // 투명값을 설정한다
  ctx.globalAlpha = 0.2;

  // 반투명한 원을 그린다
  for (var i = 0; i < 7; i++){
    ctx.beginPath();
    ctx.arc(75, 75, 10 + 10 * i, 0, Math.PI * 2, true);
    ctx.fill();
  }
}
```

![globalaAlpha Image]({{ site.baseurl }}/assets/images/canvas_globalalpha.png)

<br><br><br>