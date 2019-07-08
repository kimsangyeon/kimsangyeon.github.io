---
layout: post
title: "Reflow Repaint"
categories: [ browser, performance, repaint, reflow ]
image: assets/images/banner/web.png
author: yeon
---

## Reflow Repaint

브라우저 랜더링 성능 개선을 위해서 중요한 **Repaint**와 **Reflow**에 관한 개념 정리를 해본다. <br>

<br>


### Reflow

DOM Element 들의 위치 크기를 재계산하는 과정을 말하며, 이는 하위 상위 DOM Element에 영향을 끼치기 때문에 문서의 일부 혹은 문서 전체를 다시 랜더링한다. 그리고 **Reflow**가 끝난 후 새롭게 생성된 랜더 트리를 다시 그리는 과정이 바로 **Repaint** 이다. <br>

<br><br>


### Repaint

레이아웃에 영향을 주지 않는 속성이 변경되었을 경우 발생하는 현상이며, 레이아웃이 변경되지 않기 때문에 **Reflow**는 일어나지 않고 **Repaint**만 일어난다.
- visibility, outline, opacity, background-color 등

<br>

**Repaint**의 경우 가시성 스타일을 변경하는 경우 엔진이 모든 요소를 검색하여 표시 내용과 표시 대상을 결정해야 하므로 성능 측면에서 비용이 많이 든다고 한다. <br>

<br>


#### Reflow 최적화
- 스타일 변경시 최대한 끝에 위치한 DOM 노드를 병경해 주어야 한다.

- 인라인 스타일을 최대한 사용하지 마라.
스타일 속성 변경시 리플로우가 발생
<br>

- 애니메이션의 경우 position fixed, absolute로 전체노드와 분리시킨 후 사용하라.

-테이블로 페이지 레이아웃을 잡지마라.. 테이블은 모두 로드되고 계산된 후에 랜더링됨

- CSS JS 표현식을 피하라. 문서 일부 혹은 전체가 Reflow 될 때마다 재계산이 일어남
- CSS 하위 셀렉터를 최소화, 규칙이 적을수록 리플로우가 빠르다.
- display:none; 숨겨진 엘리먼트는 변경시 리페인트나 리플로우를 일으키지 않는다.
- 스타일 변경시 클래스 혹은 cssText를 사용하여 1번의 리플로우만 발생시키도록 한다.
- Dom Fragment를 사용하여 Element를 추가한다. 노드가 추가 될때마다 리플로우가 일어나는 것을 최소화해준다.
- 캐쉬를 활용한 Reflow 최소화
offset, scrollTop 등 계산된 스타일 정보를 요청할때마다 정확한 정보를 주기위해 변경된 내용을 다시 적용 한다고 한다.
해당 값들을 변수에 할당하여 요청 횟수를 줄여 Reflow 비용을 줄인다.

<br><br>


<br><br><br>