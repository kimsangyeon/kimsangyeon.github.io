---
layout: post
title: 'Next.js Routing'
categories: [javascript, nextjs]
image: assets/images/banner/nextjs.jpeg
author: yeon
---

# Next.js Routing

Next.js에는 파일시스템 기반의 페이지 라우터가 있다. <br>

<br>

파일이 `pages` 디렉토리에 추가되면 자동으로 페이지 경로로 사용할 수 있다. `pages` 디렉토리 내의 파일은 가장 일반적인 패턴을 정의하는데 사용할 수 있다. <br>

<br><br>

### Index routes

라우터는 index 파일을 디렉토리의 루트로 자동 라우팅한다. <br>

- 파일 경로 → url
- pages / index.js → '/'
- pages/ blog / index.js → '/blog'

<br><br>

### Nested routes

라우터는 중첩 파일을 지원하며 중첩되어있는 폴더 구조를 만들면 파일이 동일한 방식으로 라우팅된다. <br>

- pages / blog / first-post.js → '/blog/first-post'
- pages/ dashboard / settings / username.js → '/dashboard/settings/username'

<br><br>

<br><br><br>