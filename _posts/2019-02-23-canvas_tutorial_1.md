---
layout: post
title: "The <canvas> element" 
categories: [ git, github, canvas ]
image: assets/images/banner/canvas.png
featured: false
author: yeon
---


### The <canvas> element
HTML5에서 canvas는 그래픽들을 관리하는 컨테이너이다.<br><br>

#### <canvas> width height
canvas는 처음 width, height를 지정하지 않을 경우 너비 300px, 높이 150px을 기본 값으로 가지게 된다.<br>
css를 사용하여 canvas 너비와 높이를 지정할 수 있지만, 랜더링을 하는동안 이미지는 레이아웃 크기에 맞게 조절되기 때문에
css의 너비와 높이를 고려하지 않을 경우 랜더링이 왜곡되어 보일수 있다.<br><br>

#### <canvas> 대체 콘텐츠
canvas는 IE9 이하 버전 등 오래된 브라우저에서 지원하지 않기 때문에 대체 콘텐츠가 필요하다. <br>
```html
<canvas id="stockGraph" width="150" height="150">
  current stock price: $3.15 +0.15
</canvas>

<canvas id="clock" width="150" height="150">
  <img src="images/clock.png" width="150" height="150" alt=""/>
</canvas>
```

<br>
canvas는 img와 달리 대체 콘텐츠 표시를 위해서 (</canvas>) 닫는 태그를 필요로 한다.




<br><br><br>