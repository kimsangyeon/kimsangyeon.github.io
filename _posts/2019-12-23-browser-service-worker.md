---
layout: post
title: 'Service Worker'
categories: [javascript, browser]
image: assets/images/banner/web.png
author: yeon
---

# Service Worker

사용자에게 주기적으로 Push 알람을 노출시켜 광고성 효과를 노리는 작업이 필요하여 `Service Worker`에 대해 공부하게 되었고 정리하게 되었습니다. 이미 Google Developers에 정리가 너무 잘되어있어 한번 더 짚어 본다는 느낌으로 정리하였습니다. <br>

<br>

`Service worker`는 기본적으로 웹 응용 프로그램, 브라우저 및 네트워크 (사용 가능한 경우) 사이에있는 프록시 서버의 역할을 합니다. 라고 MDN에 아무 명확하게 설명이 되어있었습니다. 프록시 서버 역할로 `Service Worker`는 클라이언트와 서버 사이에서 요청을 가로채어 데이터를 제어하는 역할을 하고 있습니다. 그리고 오프라인 환경을 제어 할 수 있도록 지원하는 역할도 하고 있습니다. <br>
제공되는 기능을 보자면 `ServiceWorker`는 브라우저가 백그라운드에서 실행하는 스크립트로, 웹페이지와는 별개로 작동하며, 웹페이지 또는 사용자 상호작용이 필요하지 않은 기능을 제어합니다. 현재 푸시 알림 및 백그라운드 동기화와 같은 기능은 이미 제공되고 있습니다. <br>

<br>

<br><br><br>
