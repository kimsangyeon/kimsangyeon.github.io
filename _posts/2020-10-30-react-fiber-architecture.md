---
layout: post
title: 'React Fiber Architecturee'
categories: [javascript, react]
image: assets/images/banner/react.png
author: yeon
---

# React Fiber Architecture

React Fiber는 React의 핵심 알고리즘이다. React Fiber의 목표는 애니메이션, 레이아웃 등과 같은 영역에 대한 랜더링 성능을 상승시키는데에 있다. 핵심 기능은 증분 랜더링으로 랜더링 작업을 청크로 분할하고 여러 프레임에 분산시키는 기능이다. <br>

<br>

다른 주요 기능으로는 업데이트 중 작업을 일시 중지, 또는 재사용하는 기능과 업데이트에 우선순위를 할당이 있다. <br>

<br><br>

## What is Reconciliation?

### **reconciliation**

React에서 변경해야할 부분을 정하기 위해 Virtual DOM 배후에서 트리 두개를 비교하는 알고리즘이다. React 애플리케이션을 랜더링하게되면 앱을 가리키는 노드 트리가 생성되어 메모리에 저장되어 랜더링에 사용된다.

 앱이 업데이트가 되면 새로운 트리가 생성되고 이전의 트리와 새로운 트리를 비교하여 필요한 작업을 계산하게 된다.


<br>

### Scheduling

React는 랜더링을 위해 작업(ex: setState)을 생성해내며 [scheduling]()은 작업이 수행되어야하는 시기를 결정하는 프로세스이다.

 랜더링시 덜 중요한 백그라운드 작업을 지연 시킬수 있다. 그리고 사용자 상호작용, 백그라운드 작업의 우선순위를 지정하여 프레임 손실을 방지한다.

<br><br>

## What is Fiber?

Fiber의 목표는 React Scheduling을 활용 할 수 있도록 하는 것이다. 작업을 일시중지하고 다시 시작, 작업들의 우선순위 지정, 이전에 완료된 작업을 재사용 그리고 필요하지 않은 작업을 중지한다.

<br><br><br>