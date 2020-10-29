---
layout: post
title: 'React Render Phase & Commit Phase'
categories: [javascript, react]
image: assets/images/banner/react.png
author: yeon
---

# React Render Phase & Commit Phase

**랜더링 단계 (Render Phase)**에서 Virtual DOM에 커밋 해야하는 변경 사항을 계산, React가 변경 사항을 결정하기위해 이전 랜더링과 현재 DOM을 비교한다. <br>
**커밋 단계 (Commit Phase)**에서는 랜더링 단계에서 결정된 변경 사항을 커밋한다.

<br>

**랜더링 단계**에서는 재조정(reconciler)에서 관리되며 일반적으로 사용되는 legacy mode에서는 스택기반으로 동기적 Render Phase가 수행된다. 이는 React가 Virtual DOM을 생성하는 단계이며 랜더링 할 모양을 결정하는 것입니다. <br>

concurrent mode에서는 비동기로 스택기반에서 fiber architecture로 변경되어 React 앱이 사용자의 장치 기능 및 네트워크 속도에 맞추어 랜더링 단계를 수행한다. <br>

<br>

**커밋 단계**는 랜더링 단계와 다르게 모드에 상관없이 동기적으로 실행. 커밋 단계에서는 콜스택을 비우지 않고 DOM조작을 일괄 처리 후, 콜 스택이 비게되면 브라우저에서 화면을 페인트한다. <br>

<br>

랜더링 단계와 커밋 단계 주요 차이점 중 하나는 랜더링 단계는 여러번 호출 될 수 있지만 커밋 단계는 변경을 위해 한번만 호출된다.
