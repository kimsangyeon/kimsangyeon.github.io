---
layout: post
title: "The canvas gradient" 
categories: [ git, github, canvas ]
image: assets/images/banner/canvas.png
featured: false
author: yeon
---


#### gradient
다른 그래픽 프로그램들과 마찬가지로, 선형 및 원형의 그레이디언트를 사용할 수 있습니다. 다음 메소드 중 하나를 사용하여 CanvasGradient 객체를 생성합니다. 그런 다음 이 객체를 fillStyle 또는 strokeStyle 속성에 할당 할 수 있습니다. <br>

- createLinearGradient(x1, y1, x2, y2): 시작점 좌표를 (x1, y1)로 하고, 종료점 좌표를 (x2, y2)로 하는 선형 그라디언트 오브젝트를 생성합니다.
- createRadialGradient(x1, y1, r1, x2, y2, r2): 반지름이 r1이고 좌표 (x1, y1)을 중심으로 하는 원과, 반지름이 r2이고 좌표 (x2, y2)를 중심으로 하는 원을 사용하여 그라디언트가 생성됩니다.

<br>

##### createLinearGradient

```javascript
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  // 그레이디언트를 생성한다
  var lingrad = ctx.createLinearGradient(0, 0, 0, 150);
  lingrad.addColorStop(0, '#00ABEB');
  lingrad.addColorStop(0.5, '#fff');
  lingrad.addColorStop(0.5, '#26C000');
  lingrad.addColorStop(1, '#fff');

  var lingrad2 = ctx.createLinearGradient(0, 50, 0, 95);
  lingrad2.addColorStop(0.5, '#000');
  lingrad2.addColorStop(1, 'rgba(0, 0, 0, 0)');

  // 외곽선과 채움 스타일에 그레이디언트를 적용한다
  ctx.fillStyle = lingrad;
  ctx.strokeStyle = lingrad2;
  
  // 도형을 그린다
  ctx.fillRect(10, 10, 130, 130);
  ctx.strokeRect(50, 50, 50, 50);

}
```

![linear gradient Image]({{ site.baseurl }}/assets/images/canvas_lineargradient.png)

<br>

##### createRadialGradient

```javascript
function draw() {
  var ctx = document.getElementById('canvas').getContext('2d');

  // 그라디언트를 생성한다
  var radgrad = ctx.createRadialGradient(45,45,10,52,50,30);
  radgrad.addColorStop(0, '#A7D30C');
  radgrad.addColorStop(0.9, '#019F62');
  radgrad.addColorStop(1, 'rgba(1,159,98,0)');
  
  var radgrad2 = ctx.createRadialGradient(105,105,20,112,120,50);
  radgrad2.addColorStop(0, '#FF5F98');
  radgrad2.addColorStop(0.75, '#FF0188');
  radgrad2.addColorStop(1, 'rgba(255,1,136,0)');

  var radgrad3 = ctx.createRadialGradient(95,15,15,102,20,40);
  radgrad3.addColorStop(0, '#00C9FF');
  radgrad3.addColorStop(0.8, '#00B5E2');
  radgrad3.addColorStop(1, 'rgba(0,201,255,0)');

  var radgrad4 = ctx.createRadialGradient(0,150,50,0,140,90);
  radgrad4.addColorStop(0, '#F4F201');
  radgrad4.addColorStop(0.8, '#E4C700');
  radgrad4.addColorStop(1, 'rgba(228,199,0,0)');
  
  // 도형을 그린다
  ctx.fillStyle = radgrad4;
  ctx.fillRect(0,0,150,150);
  ctx.fillStyle = radgrad3;
  ctx.fillRect(0,0,150,150);
  ctx.fillStyle = radgrad2;
  ctx.fillRect(0,0,150,150);
  ctx.fillStyle = radgrad;
  ctx.fillRect(0,0,150,150);
}
```

![radial gradient Image]({{ site.baseurl }}/assets/images/canvas_radialgradient.png)

<br><br><br>