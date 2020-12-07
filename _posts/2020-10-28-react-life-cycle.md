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

**랜더링 단계**는 재조정(reconciler)에서 관리된다. 일반적으로 사용되는 legacy mode에서는 스택기반으로 동기적 Render Phase가 수행된다. 이는 React가 Virtual DOM을 생성하는 단계이며 랜더링 할 모양을 결정하는 것이다. <br>

concurrent mode에서는 비동기로 스택기반에서 fiber architecture로 변경되어 React 앱이 사용자의 장치 기능 및 네트워크 속도에 맞추어 랜더링 단계를 수행한다. <br>

<br>

**커밋 단계**는 랜더링 단계와 다르게 모드에 상관없이 동기적으로 실행. 커밋 단계에서는 콜스택을 비우지 않고 DOM조작을 일괄 처리 후, 콜 스택이 비게되면 브라우저에서 화면을 페인트한다. <br>

<br>

랜더링 단계와 커밋 단계 주요 차이점 중 하나는 랜더링 단계는 여러번 호출 될 수 있지만 커밋 단계는 변경을 위해 한번만 호출된다. <br>

<br><br>

![React Life Cycle]({{ site.baseurl }}/assets/images/react-life-cycle.jpeg)

<br>

**Mounting**
Component가 생성될때 한번 실행된다. <br>

**Updating**
Component가 변경 될 때마다 실행된다. <br>

**Unmounting**
Component가 제거되려고 할때 한번 실행된다. <br>

**Render Phase**
변경 사항을 계산하는데 사용되며 사용자가 원할 경우 중단 할 수 있다. 이 단계가 중단되면 DOM 업데이트를 수행하지 않는다. <br>

**Pre Commit Phase**
VDOM에 대한 변경 사항이 실제 DOM에 적용되기 전에 읽을 수 있는 단계이다. <br>

**Commit Phase**
변경 사항이 적용되고 side effect가 실행되는 단계이다. <br>

<br>

Virtual DOM은 더블 버퍼링 형태로 랜더링 단계 (Render Phase)에서 진행중인 work in progress와 커밋 단계 (Commit Phase)를 지나온 current tree로 관리된다. 둘은 fiberNode로 생성되어 alternate로 참조한다. <br>

<br><br>


![React Fiber]({{ site.baseurl }}/assets/images/react-fiber.png)

<br>

React는 위와같이 두개의 버퍼 구조를 사용하여 업데이트를 수행한다. 업데이트가 진행중인 work in progress는 업데이트 중 중지, 폐기 될 수 있으며 current를 복제하여 새로운 work in progress를 생성한다. <br>

<br>

React Fiber는 재조정 알고리즘(Reconciler Algorithm)이며, 이전 Tree를 새로운 Tree와 비교하여 수정된 항목을 찾는 알고리즘이다. (v16. 이전에는 Stack Reconciler 였다고 한다.) <br>
- 중지 가능한 작업을 청크로 분할
- 진행중인 작업의 우선순위 지정, 리베이스 및 재사용 가능

<br>

**Fiber는 7가지로 작업 우선순위를 지정**

- NoWork
- SynchronousPriority
- TaskPriority
- AnimationPriority
- HighPriority
- LowPriority
- OffscreenPriority


<br><br>

[ref]: 
- [React 톺아보기 - 02. Intro](https://kimsangyeon.github.io/javascript/2020/04/02/javascript-coroutine-event-loop.html)
- [Understanding React Fiber Architecture](https://dzone.com/articles/understanding-of-react-fiber-architecture)
- [[React] 리액트를 처음부터 배워보자. — 03. React 의 Update 스케줄링 과정](https://medium.com/react-native-seoul/react-%EB%A6%AC%EC%95%A1%ED%8A%B8%EB%A5%BC-%EC%B2%98%EC%9D%8C%EB%B6%80%ED%84%B0-%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90-03-react-%EC%9D%98-reconciliation-%EA%B3%BC%EC%A0%95-2e6fb59c0c2d)

<br><br><br>
