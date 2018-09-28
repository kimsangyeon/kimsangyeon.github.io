---
layout: post
title: "Angular Test" 
categories: [ Angular, Javascript, typescript ]
image: assets/images/banner/angular.png
author: yeon
---

# Angular Test
Angular CLI에서 애플리케이션 테스트 설정으로 자스민(Jasmine)과 카르마(Karma) 기본 도구를 사용해보자.

<br><br>

## Jasmine
Jasmine은 테스크 케이스를 작성, 관리하는 여러 기능을 제공하는 테스트 프레임 워크이다.
- describe : 테스트 집합 컨테이너
- beforeEach : 테스트 케이스 실행전 준비 설정 작업을 주로 수행
- it : 실질적으로 테스트 코드 작성 부분
- expect : 테스트 케이스 유효성을 검사 (assert)
- toBe : assert에서 기대하는 값
- toContain : 반환값에 기대 값이 포함되어있는지 확인
- toBeLessThen, toBeGreaterThan : 값의 범위 확인

<br><br>

## Karma
Karma는 테스트 케이스를 실행하고 결과를 보여주는 역할을 한다. 실질적으로 브라우저를 실행하여 테스트 케이스를 실행하는 도구.

<br><br><br>

## Jasmine & Karma 설치
~~~
npm i -g karma-cli
npm i -D jasmine-core
~~~
karma CLI와 jasmine-core 설치

<br><br><br>

### Karma CLI 의존성 설치
~~~
npm i karma karma-chrome-launcher karma-jasmine -D
~~~
-D : devDependencies 설치

<br><br><br>

### Jasmine 타이핑
테스트 케이스도 typescript로 작성하기 위해 필요.
~~~
npm i @types/jasmine
~~~



<br><br><br>