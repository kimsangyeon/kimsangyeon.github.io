---
layout: post
title: "Module UMD (Univeral Module Definition)" 
categories: [ Javascript, UMD, Module ]
image: assets/images/banner/javascript.png
author: yeon
---

# Module UMD (Univeral Module Definition)
오픈소스 lodash 공부중, The Lodash library exported as a UMD module. 보고 umd에 대해 정리


<br>

#### UMD, 만능 모듈 정의

<br>

UMD 모듈은 클라이언트, 서버 또는 다른 곳에 있는 모든 곳에서 작동할 수 있는 모듈이라고 한다. <br>
RequireJS와의 호환성을 제공하며, CommonJS 호환성 처리를 위해 AMD를 기본으로 사용한다고 한다. <br>
- UMD 포맷은 브라우저와 Node.js에서 둘 다 사용될 수 있다.
<br><br>

##### 간략 CommonJS, AMD
CommonJS는 Javascript만이 아닌 브라우저를 포함하여, 서버사이드, 데스트톱까지 사용가능한 범용적 지원을 합니다. <br>
AMD는 브라우저 내에서의 실행이 중점이었고, CommonJS와 합의점을 찾지 못하고 독립적을 분리 되었다고 한다. <br>

<br><br>

위와 같은 상황으로 두 스타일을 모두 지원하는 일반, 보편적인 패턴에 대한 작업이 이루어진것이 UMD라고 한다.
- AMD, CommonJS와 호환가능

<br><br><br>