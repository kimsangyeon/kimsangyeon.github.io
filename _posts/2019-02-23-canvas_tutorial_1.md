---
layout: post
title: "The canvas element" 
categories: [ git, github, canvas ]
image: assets/images/banner/canvas.png
featured: false
author: yeon
---


### The canvas element
HTML5에서 canvas는 그래픽들을 관리하는 컨테이너이다. <br><br>

#### canvas width height
canvas는 처음 width, height를 지정하지 않을 경우 너비 300px, 높이 150px을 기본 값으로 가지게 된다. <br>
css를 사용하여 canvas 너비와 높이를 지정할 수 있지만, 랜더링을 하는동안 이미지는 레이아웃 크기에 맞게 조절되기 때문에
css의 너비와 높이를 고려하지 않을 경우 랜더링이 왜곡되어 보일수 있다. <br><br>

#### canvas 대체 콘텐츠
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

<br>

#### canvas 직사각형 함수
svg와는 다르게 canvas는 직사각형 하나의 원시적인 도형을 그리는 함수만 제공 <br>

- fillRect(x, y, width, height) : 색칠된 직사각형
- strokeRect(x, y, width, height) : 직사각형의 윤곽선
- clearRect(x, y, width, height) : 특정 부분을 지우는 직사각형

canvas에서 x, y는 그리는 시작 좌표 / width, height는 크기 <br>

<br>

#### canvas path 함수
canvas에서 직사각형 이외의 도형들은 path로 그리며, path는 점들의 집합으로 선을 연결하여 도형을 그린다. <br>

1. 경로 생성
2. 그리기 명령
3. 만들어진 경로에 윤곽선 및 채우기

<br>

- beginPath() : 새로운 경로 생성
- moveTo(x, y) : 펜을 x, y 좌표로 이동
- lineTo(x, y) : 현재위치에서 x, y 좌표까지 선 그리기
- closePath() : 현재 경로에서 시작경로로 직선 그리기
- stroke() : 윤관선을 이용하여 도형 그리기
- fill() : 경로의 내부를 채워 도형 그리기

<br>

##### 호 (arc)
- arc(x, y, radius, startAngle, endAngle, anticlockwise) : x, y좌표에 원점을 주고 반지름 r만큼 startAngle에서 시작하여 endAngle에서 끝 나며 anticlockwise 방향으로 진행 (기본 시계방향)
- arcTo(x1, y1, x2, y2, radius) : 두 직선사이 호를 그리고 점들을 직선으로 연결한다.

<br>

> arc에서 각도는 각이아닌 라디안 값 사용 [radians = (Math.PI/180) * degress]

<br>


##### 이차 곡선 (quadratic)
- quadraticCurveTo(cp1x, cp1y, x, y) : cp1x 및 cp1y로 지정된 제어점을 사용하여 현재 펜의 위치에서 x와 y로 지정된 끝점까지 이차 베지어 곡선을 그립니다.

![Quadratic Curve Image]({{ site.baseurl }}/assets/images/quadratic_curve.png)

<br>


##### 베지어 곡선 (bezier)
- bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y) : (cp1x, cp1y) 및 (cp2x, cp2y)로 지정된 제어점을 사용하여 현재 펜 위치에서 x 및 y로 지정된 끝점까지 삼차 베지어 곡선을 그립니다.

![Bezier Curve Image]({{ site.baseurl }}/assets/images/bezier_curve.png)

<br>

#### Path2D 오브젝트
Path2D 객체를 사용하여 드로잉 명령 실행 및 캐시 기록 가능하다. <br>
moveTo, rect, arc, 혹은 quadraticCurveTo 등과 같은 모든 경로 메소드를 사용 가능.

```javascript
function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');

    var rectangle = new Path2D();
    rectangle.rect(10, 10, 50, 50);

    var circle = new Path2D();
    circle.moveTo(125, 35);
    circle.arc(100, 35, 25, 0, 2 * Math.PI);

    ctx.stroke(rectangle);
    ctx.fill(circle);
  }
}
```

<br>

Path2D의 가장 강력한 특징은 SVG path data를 canvas에 재사용 할 수 있게 해준다.

```javascript
var p = new Path2D('M10 10 h 80 v 80 h -80 Z');
```

<br>

<br><br><br>