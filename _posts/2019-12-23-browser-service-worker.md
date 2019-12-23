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

<br>

제공되는 기능을 보자면 `ServiceWorker`는 브라우저가 백그라운드에서 실행하는 스크립트로, 웹페이지와는 별개로 작동하며, 웹페이지 또는 사용자 상호작용이 필요하지 않은 기능을 제어합니다. 현재 푸시 알림 및 백그라운드 동기화와 같은 기능은 이미 제공되고 있습니다. <br>

<br>

`Service Worker`는 작업자 컨텍스트(Worker Context)에서 실행 되기 때문에 DOM에 직접 접근 할 수 없습니다. 대신 `postMessage`를 사용하여 전달된 메시지에 응답하는 방식으로 페이지와 통신이 가능하며, 페이지에서 DOM에 접근하여 조작 할 수 있습니다. 그리고 완전 비동기로 설계되어 있어 동기식 [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) 및 [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API)와 같은 API를 서비스 작업자 내부에서 사용할 수 없습니다. <br>

<br>

보안상의 이유로 `Service Worker`는 HTTPS를 통해서만 실행되어 네트워크 요청에 대한 중간 공격을 예방 할 수 있습니다. <br>

<br>

`Service Worker`는 일반적으로 응답을 기다렸다가 성공 또는 실패 조치를 취하기 때문에 [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)를 많이 사용합니다.

<br><br>

## Service Worker 수명주기

1. Download
2. Install
3. Activate

<br>

### Download

`Service Worker`는 제어 페이지에 접근시 즉시 다운로드가 됩니다. 그 후 24 시간마다 다운로드가되며 다운로드 한 파일이 기존의 `Service Worker`와 다른경우 (바이트 단위로 비교) 페이지의 첫 번째 `Service Worker`와 만난 경우 설치가 시도 됩니다. <br>

<br>

`.register()`를 호출하면 `Service Worker`가 다운로드됩니다. 만약 스크립트를 다운로드하지 못하거나 실행중 로류가 발생하는 경우 register promise가 거부되고 `Service Worker`가 삭제 됩니다. <br>
- Chrome의 DevTools의 `Application`탭 Service Worker 섹션에서 오류 확인이 가능

<br>

### Install

`install` 이벤트는 `Service Worker`가 받는 첫 번째 이벤트이며 최초 한번만 발생합니다. `Service Worker`는 `install`과 `activate`는 시간이 걸리는 작업이기 때문에 promise를 반환하는 `waitUntil`을 제공합니다. promise가 성공적으로 resolved 될 때까지 `Service Worker`에 이벤트들이 전달되지 않습니다. <br>

<br>

### Activate

`Service Worker`가 설치 완료된 후 `activate`될 때까지 featch 및 push 이벤트는 수신되지 않습니다. 해당 이벤트 수신 및 `Service Worker` 동작을 위해서는 페이지를 새로고침하여야 합니다. `Service Worker`가 활성화된 이후에 메모리 절약을 위해 종료되거나, 페이지에서 네트워크 요청 메시지가 생성될때 fetch 및 message 이벤트를 처리합니다. <br>

<br>

Download, Install, Activate 예시로 [Service Worker Life Cycle](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle?hl=ko)에 이미지 불러오기 예시를 참고 할 수 있습니다. <br>

<br>

```html
<!DOCTYPE html>
An image will appear here in 3 seconds:
<script>
  navigator.serviceWorker.register('/sw.js')
    .then(reg => console.log('SW registered!', reg))
    .catch(err => console.log('Boo!', err));

  setTimeout(() => {
    const img = new Image();
    img.src = '/dog.svg';
    document.body.appendChild(img);
  }, 3000);
</script>
```

dog.svg가 설정된 이미지를 `Service Worker`를 등록 후 3초 후에 불러옵니다.

<br>

그리고 `sw.js`

```javascript
self.addEventListener('install', event => {
  console.log('V1 installing…');

  // cache a cat SVG
  event.waitUntil(
    caches.open('static-v1').then(cache => cache.add('/cat.svg'))
  );
});

self.addEventListener('activate', event => {
  console.log('V1 now ready to handle fetches!');
});

self.addEventListener('fetch', event => {
  const url = new URL(event.request.url);

  // serve the cat SVG from the cache if the request is
  // same-origin and the path is '/dog.svg'
  if (url.origin == location.origin && url.pathname == '/dog.svg') {
    event.respondWith(caches.match('/cat.svg'));
  }
});
```

`Service Worker`에서 cat.svg를 캐시하여 제공하지만 처음 페이지를 로딩시 dog.svg가 그려집니다. 새로고침시 `Service Worker activate`되며 cat.svg가 표시됩니다.

<br><br><br>
