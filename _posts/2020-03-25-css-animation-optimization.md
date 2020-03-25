---
layout: post
title: 'CSS Animation Optimization'
categories: [javascript]
image: assets/images/banner/css3.png
author: yeon
---

# CSS Animation Optimization

브랜드 배너 이미지 리스트를 Animation을 사용하여 좌우로 랜더링하는 작업을 하였습니다. 이후... CPU가 굉장히 소모되는 문제가 발생... Animation에 대한 DOM 최적화 처리가 미흡했었기 때문이였습니다. 해당 이슈에서 Animation을 잘못 사용하였던 예와 최적화 및 해결 방법에 대해 정리합니다. <br>

<br><br>

## Browser Render Process

브라우저 랜더링에서 중요한 `Reflow`와 `Repaint`에 대한 최적화는 항상 중요합니다. 불필요한 `Reflow`, `Repaint`시 성능이 굉장히 좋지 않기 때문에 작업시 유의가 필요합니다. `Reflow`는 브라우저 DOM Tree를 파싱하고 CSS Style에 맞게 레이아웃을 잡는 과정이라고 할 수 있습니다. 때문에 DOM 추가 및 제거, Style 변경시 `Reflow`가 발생하게 됩니다. 이후에 위치와 크기 그리고 스타일이 계산된 Render Tree(형상 Tree)를 이용하여 실제 픽셀 값을 채워 그리는 과정이 `Repaint`입니다. 

![Render Tree]({{ site.baseurl }}/assets/images/renderTree.png)

<br>

위의 브라우저 랜더링 과정을 본다면 `Reflow` -> `Repaint` 순으로 랜더링이 진행되기 때문에 `Reflow`시에는 `Repaint`가 항상 일어나므로 랜더링 성능을 최적화 하기 위해서는 `Reflow`가 필요하지 않은 동작은 `Repaint`만 실행될 수 있도록 최적화하는 것이 중요합니다. 여기서 하나 더 `Repaint` 동작 이후에 수행하는 것이 있는데 바로 `Composite`입니다.

<br>
