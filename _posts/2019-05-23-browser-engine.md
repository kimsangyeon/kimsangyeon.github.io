---
layout: post
title: "Browser Engine" 
categories: [ javascript, nodejs ]
image: assets/images/banner/web.png
featured: false
author: yeon
---

## Browser Engine

브라우저 엔진(browser engine)은 주된 모든 웹 브라우저의 핵심이 되는 소프트웨어 구성 요소이다. 브라우저 엔진의 역할은 HTML 문서와 기타 자원의 웹 페이지를 사용자의 장치에 상호작용적인 시각 표현으로 변환시키는 것이다. <br>

<br>

### 웹 랜더링 엔진의 사용

브라우저에서 랜더링 엔진이 HTML 문서를 파싱하고, DOM(Document Object Model)로 변환한다. <br>
이후 CSS 스타일과 함께 파싱하여  Render Tree를 생성, Render Tree 생성 후 화면에 노드들을 배치,
UI backend Layer를 이용해 배치된 노드들을 그린다. <br>

1. HTML 파싱 (DOM 생성)
2. Render Tree 생성 (CSS 스타일과 함께 파싱하여 생성)
3. Render Tree 배치 (노드 배치)
4. Render Tree 랜더링

<br>

#### 랜더링 엔진

**Webkit**은 애플에서 개발한 웹 랜더링 엔진이다. Safari Chrome 브라우저 안드로이드 기기용 브라우저 등에서 Webkit 랜더링 엔진을 사용
하지만 현재 구글은 Chrome(28버전)부터는 Webkit이 아닌 Blink라는 새로운 웹 랜더링 엔진을 사용중 <br>

<br>

**Blink** 랜더링 엔진은 Webkit에 포킹된 랜더링 엔진이라고 한다. 구글 크롬 버전 28+, 오페라 브라우저 15+, 비발디 브라우저, 웨일 브라우저[6] 안드로이드 4.4+의 웹뷰 및 Qt 웹엔진에서 사용중이다. <br>

<br>

**Gecko** 넷스케이프 커뮤니케이션스 개발, 2003년부터 모질라 재단이 관리하고있으며, 파이어폭스에서 사용중인 랜더링 엔진 <br>

<br>

**Trident** 마이크로소프트 윈도 버전의 인터넷 익스플로러가 채용하고 있는 레이아웃 엔진의 이름이다. <br>
마이크로소프트 엣지 브라우저에서 트라이던트는 EdgeHTML로 대체되었다. <br>

<br>

- 웹키트(Webkit): KHTML에서 파생된 레이아웃 엔진으로 사파리 등이 탑재하고 있다.
- 블링크(Blink): 웹키트에서 파생된 레이아웃 엔진으로 크롬, 오페라 등이 이를 탑재하고 있다.
- 게코(Gecko): 모질라 재단에서 만든 레이아웃 엔진으로 파이어폭스, 모질라 선더버드, 시몽키 등이 이를 탑재하고 있다.
- 트라이던트(Trident): 마이크로소프트의 레이아웃 엔진으로 인터넷 익스플로러, 아웃룩 익스프레스, 마이크로소프트 아웃룩, 그리고 윈앰프, 리얼플레이어의 미니 브라우저 등이 이를 탑재하고 있다.
- 프레스토(Presto): 오페라 소프트웨어의 사유 엔진으로 오페라가 탑재하고 있다. 오페라 15부터는 블링크로 교체되었다.
KHTML KDE의 컨커러가 탑재하고 있다.
- 태즈먼(Tasman): 마이크로소프트의 레이아웃 엔진으로 맥용 인터넷 익스플로러가 탑재하고 있다.

<br>

<br><br><br>