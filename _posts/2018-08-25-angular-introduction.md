---
layout: post
title: "Angular Introduction" 
categories: [ Javascript, Angular, typescript ]
image: assets/images/banner/angular.png
author: yeon
---

# Angular Introduction
AngularJS는 자바스크립트 기반의 오픈 소스 프론트엔드 웹 애플리케이션 프레임워크의 하나로, 싱글 페이지 애플리케이션 개발 중에 마주치는 여러 문제들을 해결하기 위해 개발되었으며 주로 구글과 개별 커뮤니티, 여러 회사에 의해 유지보수되고 있다. 자바스크립트 구성 요소들은 크로스 플랫폼 모바일 앱을 개발하기 위해 사용되는 프레임워크인 아파치 코도바를 보완한다. [위키백과]


## Angular 란?
### Angular 사용성
- HTML을 쉽게 표현할 수 잇는 구조 지시자를 제공한다.
- 애플리케이션 모델과 UI 사이에 채널을 설정하도록 단방향, 양방향 바인딩 기능 제공한다.
- 빠른 로딩시간으로 랜더링에서의 장점이 있다.
- 모듈화된 디자인으로 재사용성에 용의하다.
- 서버와의 통신을 쉽게하는 인터페이스를 제공한다.
- Javascript, typescript 최신기능을 활용할 수 있다.
- 쉽게 구현이 가능한 프레임워크 제공으로 생산성이 향상된다.

![Anguler Application image](../image/Angular_app.png)


### Angular 아키텍쳐
Angular는 모듈형 애플리케이션을 만들 수 있어 재사용성에 용이하다.
크게는 웹 애플리케이션을 기반으로 모듈과 컴포넌트로 구성되고 서비스 계층이 존재한다.
- HTML: 컴포넌트의 UI를 구성(템플릿), 인라인이나 HTML파일로 정의 할 수 있다.
- 클래스: Typescript로 작성하며 뷰에서 실행되는 메서드와 프로퍼티를 정의한다.
- 메타데이터: 클래스를 컴포넌트로 식별하여 화면에 표시할 수 있도록 제공한다.