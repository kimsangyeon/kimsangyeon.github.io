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

브라우저 랜더링에서 중요한 `Reflow`와 `Repaint`에 대한 최적화는 항상 중요합니다. 불필요한 `Reflow`, `Repaint`시 성능이 굉장히 좋지 않기 때문에 작업시 유의가 필요합니다. <br>

<br>

### Reflow Repaint

`Reflow`는 브라우저 DOM Tree를 파싱하고 CSS Style에 맞게 레이아웃을 잡는 과정이라고 할 수 있습니다. 때문에 DOM 추가 및 제거, Style 변경시 `Reflow`가 발생하게 됩니다. 이후에 위치와 크기 그리고 스타일이 계산된 Render Tree(형상 Tree)를 이용하여 실제 픽셀 값을 채워 그리는 과정이 `Repaint`입니다.

![Render Tree]({{ site.baseurl }}/assets/images/renderTree.png)

<br><br>

### Composite

위의 브라우저 랜더링 과정을 본다면 `Reflow` -> `Repaint` 순으로 랜더링이 진행되기 때문에 `Reflow`시에는 `Repaint`가 항상 일어나므로 랜더링 성능을 최적화 하기 위해서는 `Reflow`가 필요하지 않은 동작은 `Repaint`만 실행될 수 있도록 최적화하는 것이 중요합니다. 여기서 하나 더 `Repaint` 동작 이후에 수행하는 것이 있는데 바로 `Composite`입니다. <br>

<br>

`Composite`는 HTML과 CSS로 생성된 구역인 Layer 별로 `Repaint`하는 작업으로 한장의 bitmap으로 만드는 과정입니다. 해서 `Repaint`과정을 나눈 `Composite`만 수행하는 랜더링으로 최적화를 한다면 브라우저 랜더링을 좀 더 효율적으로 할 수 있습니다. 이는 Style을 적용할때 유의가 필요한데 이는 [CssTriggers](https://csstriggers.com/)에 정의된 Style을 참고하여 사용하면 될 것 같습니다. <br>

<br><br>

## CSS Animation

위에서 보았던 브라우저 랜더링 과정을 참고하여 CSS Animation을 구현한다고 생각해봅시다. <br>

<br>

첫째로 Animaion은 동적으로 계속해서 움직이며 랜더링이 이루어지기 때문에 해당 Layer를 분리시키는 것이 좋습니다. Layer를 분리 시키지 않을시에 Animation이 설정된 DOM이 랜더링되며 아래 혹은 위 DOM Layout에 영향을 미친다면? Animation이 움직이는 Frame마다 `Reflow`가 일어나게 될테고 이는 최악의 퍼포먼스를 초례하게 될 것입니다. <br>

<br>

둘째로는 Animation이 설정된 DOM이 다른 DOM에 영향을 미치지 않도록 처리하였을때, 사용된 속성이 left, top 혹은 width, height라고 했을때 해당 DOM에 영향을 받는 범위에서 `Reflow` -> `Repaint`가 일어나게 될 것입니다. 여기서 `Reflow`가 일어나지 않는 속성을 사용하여 `Repaint`가 일어나게 한다면 **Better**, 더 나아가 `Composite`만 수행하게 한다면? **Best**일 것입니다. Animation 동작은 보통 위치를 움직인다거나 혹은 크기를 변경하는 동작이 많은데 이때 width, height를 통한 크기변경과 left, top 등을 이용하여 위치를 이동시키는 것이 아닌 **transform** 속성을 사용한다면 특정 브라우저 랜더링 엔진에서는 `Composite`만 수행하므로 랜더링을 보다 효율적으로 할 수 있을 것입니다. <br>

![Composite Transform]({{ site.baseurl }}/assets/images/composite-transform.png)

위의 이미지를 보면 랜더링엔진 `Blink`와 `Gecko`에 한에서 `Composite`만으로 랜더링하는 것을 볼 수 있습니다. 그리고 해당 내용을 본다면 "`transform`을 변경해도 지오메트리 변경이나 페인팅이 트리거되지 않으므로 매우 좋습니다. 이는 GPU의 도움으로 컴포지터 스레드에서 작업을 수행 할 수 있음을 의미합니다."라고 명시되어 있습니다. <br>

<br><br>

## requestAnimationFrame

Animation 동작에서 브라우저에서 최적화된 애니매이션 동작을 위해 `requestAnimationFrame`을 사용하였습니다. `requestAnimationFrame`은 브라우저에게 수행하기를 원하는 애니메이션을 알리고 다음 리페인트가 진행되기 전에 해당 애니메이션을 업데이트하는 함수를 호출하게 합니다. 이 메소드는 리페인트 이전에 실행할 콜백을 인자로 받습니다. 사용되는 콜백의 회수는 보통 1초에 60회로 수행되어 브래우저에서 효율적으로 애니매이션 함수를 호출하여 사용하도록 도와줍니다. <br>

<br>

해당 `requestAnimationFrame`이 나오기 전에는 `setInterval`을 초당 60 프레임 호출을 목표로 동작을 수행하도록 구성하였습니다. <br>

```javascript
setInterval(() => {
  // animation
  ...
}, 1000 / 60);
```

그렇다면 위 처럼 `setInterval`을 사용하는 것과 `requestAnimationFrame`을 사용하는 것은 별반 다르지 않을까? 할 수 있지만 `requestAnimationFrame`이 가지는 장점들이 있습니다.

- 각 브라우저에 최적화되어 애니매이션이 좀 더 안정적이고 부드럽게 진행
- 비활성 탭에 애니매이션은 중지되어 CPU 메모리를 사용하지 않음
- 배터리 수명에 좀 더 이점을 가짐

<br>

### requestAnimationFrame Example

`requestAnimationFrame`은 재귀 호출로 수행되며 인자로 실행될 애니메이션 동작을 가지는 콜백 함수를 받습니다.

<br>

```javascript
const start = null;
const element = document.getElementById('SomeElementYouWantToAnimate');
element.style.position = 'absolute';

function step(timestamp) {
  if (!start) start = timestamp;
  const progress = timestamp - start;
  element.style.left = `${Math.min(progress / 10, 200)}px`;
  if (progress < 2000) {
    window.requestAnimationFrame(step);
  }
}

window.requestAnimationFrame(step);
```

<br><br><br>

참고: [MDN window.requestAnimationFrame()](https://developer.mozilla.org/ko/docs/Web/API/Window/requestAnimationFrame)

<br><br><br>
