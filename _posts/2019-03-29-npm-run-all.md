---
layout: post
title: "npm-run-all" 
categories: [ git, npm ]
image: assets/images/banner/npm.png
featured: false
author: yeon
---


#### npm-run-all

병렬 또는 순차적으로 여러 npm 스크립트를 실행하는 CLI 도구.

<br>

##### script 병렬 실행

npm run script 명령으로는 여러개의 npm script를 실핼 할 수 없다.

> npm run build && npm run start

위와 같은 형식으로 npm script 나열

<br>

##### --parallel

npm-run-all을 사용하면 일반적 나열로 script 실행 가능

> npm-run-all -p build start

-p는 병렬 옵션이며 --parallel 이다. 

<br>

 --max-parallel로 최대 병렬 개수 지정 가능.

<br>

<br><br><br>