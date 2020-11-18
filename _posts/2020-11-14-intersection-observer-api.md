---
layout: post
title: 'Intersection Observer API'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Intersection Observer API

#### Draft, 31 May 2019

Intersection Observer API는 타겟 요소와 상위 요소 또는 viewport 사이의 intersection 내의 변화를 비동기적으로 관찰하는 방법이다. <br>

- 페이지가 스크롤 되는 도중에 발생하는 이미지나 다른 컨텐츠의 지연 로딩.
- 스크롤 시에, 더 많은 컨텐츠가 로드 및 렌더링되어 사용자가 페이지를 이동하지 않아도 되게 하는 infinite-scroll 을 구현.
- 광고 수익을 계산하기 위한 용도로 광고의 가시성 보고.
- 사용자에게 결과가 표시되는 여부에 따라 작업이나 애니메이션을 수행할 지 여부를 결정.

<br><br>

# Intersection Observer API

IntersectionObserver를 사용시 특정 element 비동기로 observe 가능 <br>

```jsx
let options = {
  root: document.querySelector('#scrollArea'),
  rootMargin: '0px',
  threshold: 1.0
}

let observer = new IntersectionObserver(callback, options);

let target = document.querySelector('#listItem');
observer.observe(target);
```

<br><br>

intersection observer를 생성하기 위해서는 생성자 호출 시 콜백 함수를 제공해야 한다. 이 콜백 함수는 threshold가 한 방향 혹은 다른 방향으로 교차할 때 실행된다. <br>

<br>

`threshold: 1.0` 은 대상 요소가 `root` 에 지정된 요소 내에서 100% 보여질 때 콜백이 호출될 것을 의미한다. <br>

<br><br>

## Intersection observer 설정

**IntersectionObserver**` 생성자에 전달되는 `options` 객체는 observer 콜백이 호출되는 상황을 조작할 수 있습니다. 이는 아래와 같은 필드를 가진다. <br>

<br>

**`root`** 대상 객체의 가시성을 확인할 때 사용되는 뷰포트 요소이다. 이는 대상 객체의 조상 요소여야 한다. 기본값은 브라우저 뷰포트이며, `root` 값이 `null` 이거나 지정되지 않을 때 기본값으로 설정된다. <br>

<br>

**`rootMargin`** root 가 가진 여백입니다. 이 속성의 값은 CSS의 **margin**` 속성과 유사하다. e.g. "`10px 20px 30px 40px"` (top, right, bottom, left). 이 값은 퍼센티지가 될 수 있다. 이것은 root 요소의 각 측면의 bounding box를 수축시키거나 증가시키며, 교차성을 계산하기 전에 적용된다. 기본값은 0이다. <br>

<br>

**`threshold`** observer의 콜백이 실행될 대상 요소의 가시성 퍼센티지를 나타내는 단일 숫자 혹은 숫자 배열이다. 만일 50%만큼 요소가 보여졌을 때를 탐지하고 싶다면, 값을 `0.5`로 설정하면 된다. 혹은 25% 단위로 요소의 가시성이 변경될 때마다 콜백이 실행되게 하고 싶다면 `[0, 0.25, 0.5, 0.75, 1]`과 같은 배열을 설정.기본값은 `0`이며(이는 요소가 1픽셀이라도 보이자 마자 콜백이 실행됨을 의미한다). `1.0`은 요소의 모든 픽셀이 화면에 노출되기 전에는 콜백을 실행시키지 않음을 의미한다.

<br><br>

<br><br><br>