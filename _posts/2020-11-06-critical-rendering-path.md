---
layout: post
title: 'Critical Rendering Path'
categories: [browser]
image: assets/images/banner/web.png
author: yeon
---

# Critical Rendering Path

이전에 브라우저 랜더링에 관련하여 Reflow, Repaint로 정리하여 글을 썼었다. 이번엔 developers google에 정리된 [Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path?hl=ko)를 간단하게 정리해보고자 한다.

<br><br>

# Overview

Critical Rendering Path는 주요 랜더링 경로를 최적화 하는 방법을 정리한 글로 브라우저가 HTML, CSS, Javascript를 사용하여 화면에 랜더링하는 과정을 설명한다.

<br><br>

# Constructing the Object Model

- DOM: Document Object Model
- CSSOM: CSS Object Model

브라우저가 랜더링을 하기위해서는 DOM과 CSSOM 트리가 필요하다.

<br>

해당 트리 객체를 생성하는 순서는 아래와 같다.

- 바이트 → 문자 → 토큰 → 노드 → 객체모델

브라우저가 HTML 원시 바이트를 문자로 변환, 변환된 문자를 [HTML5표준 토큰](https://html.spec.whatwg.org/)으로 변환한다. 그리고 해당 토큰을 속성 및 규칙을 정의하는 노드객체로 변환시키고 생성된 객체들로 트리 데이터 구조로 연결시킨다.

<br><br>

# Render-Tree Construction, Layout, and Paint

브라우저에서 랜더링을 위해서 DOM과 CSSOM 트리를 결합하여 랜더링 트리를 생성한다. 이러한 랜더링 트리는 페인트 프로세스 입력으로 처리되며 랜더링 성능을 위해서는 랜더링 트리를 생성하는 단계들을 최적화하는 것이 중요하다.

<br>

### 단계

- DOM과 CSSOM 트리를 결합하여 랜더링 트리 생성
- 랜더링 트리는 페이지 랜더링에 필요한 노드로 생성
- 객체의 위치와 크기를 계산 (레이아웃)
- 픽셀을 화면에 랜더링 (페인트)

랜더링 트리 생성을 위해 DOM 트리를 탐색하며 표시되지 않을 노드를 생략한다. 스크립트 태그, 메타 태그 등은 출력에 반영되지 않는다. 그리고 CSS를 통해 숨겨지는 노드도 랜더링 트리에서 생략된다. 예로는 display: none;이 있으며 visibility: hidden은 보여지지 않지만 공간을 차지하기 때문에 비어있는 상자형태로 랜더링 하기위해 랜더링 트리에 포함된다. <br>

<br>

랜더링 될 랜더링 트리가 생성되었다면 다음 단계인 레이아웃을 진행한다. 레이아웃은 뷰포트 내에서 노드의 정확한 위치와 크기를 계산하는 단계이다. <br>
레이아웃에서 상대적인 값은 절대적인 픽셀로 변환된다. <br>

<br>

마지막으로는 랜더링 트리를 화면의 실제 픽셀로 변환하는 페인트 단계를 진행하며 이는 '페인팅' 또는 '레스터화'라고 한다. 페인트 단계는 문서가 클스록 작업이 많아지고 단색은 작업이 적게 필요하지만 그림자 효과 같은 작업은 추가 작업이 더 필요하다. <br>

<br>

### 정리

1. HTML 마크업을 처리하고 DOM 트리를 빌드
2. CSS 마크업을 처리하고 CSSOM 트리를 빌드
3. DOM 및 CSSOM을 결합하여 렌더링 트리를 형성
4. 렌더링 트리에서 레이아웃을 실행하여 각 노드의 기하학적 형태를 계산
5. 개별 노드를 화면에 페인트

<br><br>

# Render-Blocking CSS

CSS는 기본적으로 랜더링 차단 리소스로 취급되며 CSSOM 트리가 생성될 때까지는 브라우저는 랜더링하지 않는다. CSS를 간단하게 유지하고 미디어 유형, 미디어 쿼리를 사용하여 랜더링 차단을 간소화 하자. <br>

<br>

랜더링 트리 생성을 위해서는 DOM과 CSSOM이 모두 필요하며 이 둘을 생성해내는 작업이 랜더링 성능에 중요한 영향을 미친다. HTML과 CSS는 둘다 랜더링 차단 리소스이다. <br>

<br>

여기서 만약 CSS가 특정 조건, 페이지 인쇄 또는 대형 모니터 출력하는 특별한 경우에만 필요한 CSS 스타일이라면 필요없는 상황에서는 리소르를 받으며 랜더링을 차단할 필요가 없을 것이다. <br>

이는 CSS **'미디어 유형'**, **'미디어 쿼리'**를 사용하여 해결할 수 있다. <br>

```html
<link href="style.css" rel="stylesheet">
<link href="print.css" rel="stylesheet" media="print">
<link href="other.css" rel="stylesheet" media="(min-width: 40em)">
```

<br>

**미디어 쿼리**는 리소스를 받을 조건을 확인하는데 사용된다. 첫번째의 경우 모든 경우에 적용되어 항상 랜더링을 차단한다. 두번째 스타일시트 선언은 컨텐츠가 인쇄 될때만 적용된다. 따라서 일반적인 경우에는 랜더링을 차단하지 않는다. 세번째의 경우에는 해당 조건이 일치하는 경우에만 랜더링을 차단하며 리소스를 받아온다. <br>

<br>

또 다른 예를 살펴보자. <br>

```html
<link href="style.css"    rel="stylesheet">
<link href="style.css"    rel="stylesheet" media="all">
<link href="portrait.css" rel="stylesheet" media="orientation:portrait">
<link href="print.css"    rel="stylesheet" media="print">
```

<br>

- 첫 번째 선언은 렌더링을 차단하고 모든 조건에서 일치
- 두 번째 선언도 렌더링을 차단합니다. 'all'이 기본 유형이므로 특정 유형을 지정하지 않을 경우 암묵적으로 'all'로 설정된다. 따라서 첫 번째와 두 번째 선언은 사실상 똑같다.
- 세 번째 선언은 페이지가 로드될 때 평가되는 동적 미디어 쿼리를 가진다. portrait.css의 렌더링 차단 여부는 페이지가 로드되는 중에 기기의 방향에 따라 달라질 수 있다.
- 마지막 선언은 페이지가 인쇄될 때만 적용된다. 따라서 페이지가 브라우저에서 처음 로드될 때는 렌더링이 차단되지 않는다.

<br>

### Adding Interactivity with Javascript

자바스크립느는 컨텐츠와 스타일 등 페이지의 모든 측면을 수정 할 수 있다. 이러한 자바스크립트는 DOM 생성을 차단하고 페이지가 랜더링되는 것을 지연 시킬 수 있다. 자바스크립트를 비동기로 설정하고 불필요한 자바스크립트를 제공하는 것으로 랜더링 성능을 올릴 수 있다. <br>

<br>

대부분 자바스크립트를 페이지 맨 아래에 위치시킵니다. 스크립트가 문서에 있는 경우에 HTML 파서는 스크립트 태그를 만나게 되는 경우 DOM 생성을 중지하고 자바스크립트 엔진에 제어 권한을 넘긴다. 그리고 자바스크립트 실행이 완료된 경우에 브라우저는 HTML 파서가 중지된 지점부터 DOM 생성을 재개한다. <br>

<br>

스크립트가 동작할때에 문서내의 요소에 접근하게 되는 경우 해당 참조가 없어 스크립트가 실패하는 경우를 방지하기 위해 스크립트는 맨 아래에 위치시키는 경우가 많다. <br>

<br>

위에서 만약 스크립트가 HTML 파싱 도중 실행되게 된다면 DOM 생성이 차단되고 초기 랜더링이 지연되게 된다.  그리고 스크립트가 DOM 만이아닌 CSSOM 속성도 읽고 수정할 수 있다는 것을 볼때 브라우저가 CSSOM을 다운로드하고 생성하는 작업이 완료 될때까지 스크립트 실행 및 DOM 생성도 지연된다는 것을 알 수 있다. <br>

- 문서에서 스크립트의 위치는 중요하다.
- 브라우저가 스크립트 태그를 만나면 이 스크립트가 실행 종료될 때까지 DOM 생성이 일시 중지된다.
- 자바스크립트는 DOM 및 CSSOM을 쿼리하고 수정할 수 있다.
- 자바스크립트 실행은 CSSOM이 준비될 때까지 일시 중지된다.

<br>

만약 외부 자바스크립트 리소스를 가져오게 되는 경우 해당 리소스를 받아올때까지 브라우저는 HTML 파서의 DOM 생성을 차단하는데 이는 리소스의 크기에 따라 큰 지연으로 이어질 수 있다. <br>

<br>

여기서 HTML 파서가 DOM을 생성하는 것을 중지 시키지 않기위해 스크립트를 비동기로 가져오게 하는 async를 사용할 수 있다. async 키워드를 스크립트 태그에 추가하게 되면 스크립트가 사용 가능해질 때까지 DOM 생성은 차단되지 않아 성능이 크게 향상된다. <br>

<br>

```html
<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <link href="style.css" rel="stylesheet">
    <title>Critical Path: Script Async</title>
  </head>
  <body>
    <p>Hello <span>web performance</span> students!</p>
    <div><img src="awesome-photo.jpg"></div>
    <script src="app.js" async></script>
  </body>
</html>
```

<br><br><br>