---
layout: post
title: "NodeJs Express란?"
categories: [ Javascript, nodejs ]
image: assets/images/banner/nodejs.png
author: yeon
---

# NodeJs Express Server 만들기

<br>

### Express.js란 무엇인가?

<br>

>Express.js는 Node.js의 핵심 모듈인 http와 Connect 컴포넌트를 기반으로 하는 웹 프레임워크다. 그러한 컴포넌트를 미들웨어(middleware)라고 하며, 설정보다는 관례(convention over configuration)와 같은 프레임워크의 철학을 지탱하는 주춧돌에 해당한다.

<br><br>

### Express.js의 작동 방식

<br>

>보통 Express.js에는 메인 파일이라고 하는 진입점이 있다. 메인 파일에서는 다음과 같은 단계를 밟는다. <br>
컨트롤러, 유틸리티, 도우미, 모델과 같은 자체적인 모듈을 비롯한 서드파티 의존 모듈을 인클루드한다.
템플릿 엔진과 해당 템플릿 엔진의 파일 확장자와 같은 Express.js 앱 설정을 구성한다.
오류 핸들러, 정적 파일 폴더, 쿠키 및 기타 파서와 같은 미들웨어를 정의한다.
라우팅을 정의한다.
MongoDB, Redis 또는 MySQL과 같은 데이터베이스에 연결한다.
앱을 구동한다.

<br><br>

### Express 설치 및 기본틀

<br>

express 디렉토리 구조
>express_tutorial <br>
|── package.json <br>
|── public <br>
|──└── css <br>
|──└── style.css <br>
|── router <br>
|──└── main.js <br>
|── server.js <br>
|── views <br>
|──└── about.html <br>
|──└─ index.html <br>

<br><br>



[참고: 위키북스 Express란 무엇인가?](http://wikibook.co.kr/article/what-is-expressjs/)