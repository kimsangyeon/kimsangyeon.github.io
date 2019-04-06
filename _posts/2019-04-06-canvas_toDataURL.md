---
layout: post
title: "The canvas toDataURL" 
categories: [ git, github, canvas ]
image: assets/images/banner/canvas.png
featured: false
author: yeon
---


## canvas toDataURL

canvas의 이미지 표현을 포함하는 data url을 가져옴

<br>

### canvas. toDataURL ( type , encoderOptions );
#### parameter
두 인자 모두 선택옵션
- type: 이미지 형식을 나타내며, 기본적으로 data:image/png
- encoderOptions: 0/1 사이 숫자로 이미지 품질 값으로 사용되며 기본 값은 0.92

<br>

#### return
return 받은 data:image/png 값은 이미지 태그 등 src로 사용가능

```javascript
const dataUrl = canvas.toDataURL();
const elImage = `<img src=${dataUrl}/>`;
```

<br><br><br>