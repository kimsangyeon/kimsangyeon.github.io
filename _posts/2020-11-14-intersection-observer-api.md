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

```javascript
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


## intersection observer polyfill

- [https://github.com/w3c/IntersectionObserver/tree/master/polyfill](https://github.com/w3c/IntersectionObserver/tree/master/polyfill) <br>

<br>

IntersectionObserver가 있는 경우 해당 Web API사용 아닌경우 IntersectionObserver  polyfill 사용 <br>

<br>

throttle을 사용한 setTimeout으로 100ms 단위로 observe 된다. <br>

```javascript
/**
 * The minimum interval within which the document will be checked for
 * intersection changes.
 */
IntersectionObserver.prototype.THROTTLE_TIMEOUT = 100;
...
function IntersectionObserver(callback, opt_options) {

  ...

  // Binds and throttles `this._checkForIntersections`.
  this._checkForIntersections = throttle(
      this._checkForIntersections.bind(this), this.THROTTLE_TIMEOUT);

...

/**
 * Throttles a function and delays its execution, so it's only called at most
 * once within a given time period.
 * @param {Function} fn The function to throttle.
 * @param {number} timeout The amount of time that must pass before the
 *     function can be called again.
 * @return {Function} The throttled function.
 */
function throttle(fn, timeout) {
  var timer = null;
  return function () {
    if (!timer) {
      timer = setTimeout(function() {
        fn();
        timer = null;
      }, timeout);
    }
  };
}
```

<br><br>

window, document에 resize scroll 이벤트를 설정하여 observe 한다. option this.root가 설정된 경우 root 기준으로 observe <br>

```javascript

addEvent(win, 'resize', callback, true);
addEvent(doc, 'scroll', callback, true);

/**
 * Adds an event handl
er to a DOM node ensuring cross-browser compatibility.
 * @param {Node} node The DOM node to add the event handler to.
 * @param {string} event The event name.
 * @param {Function} fn The event handler to add.
 * @param {boolean} opt_useCapture Optionally adds the even to the capture
 *     phase. Note: this only works in modern browsers.
 */
function addEvent(node, event, fn, opt_useCapture) {
  if (typeof node.addEventListener == 'function') {
    node.addEventListener(event, fn, opt_useCapture || false);
  }
  else if (typeof node.attachEvent == 'function') {
    node.attachEvent('on' + event, fn);
  }
}
```

<br><br>

## Intersection Obeserver 활용

### Photo List 영역 Infinity Scroll로 구현된 경우

<ul> 영역 하위로 <li> 리스트로 이미지가 스크롤시 맨 밑 영역에서 새로운 이미지를 추가 한다. <br>

가장하단에 target으로 삼을 Element를 두고 해당 target 기준으로 이미지를 추가하며 랜더링하도록 한다. <br>

<br>

<ul>은 항상 높이 값을 가지며 이미지를 추가한다. 특정 높이 혹은 이미지 개수에 따라 새로운 <ul>을 생성하며 그 하위로 <li> 다시 infinity Scroll로 갱신하여 영역을 구분한다. 그리고 특정 영역 혹은 높이를 벗어 나는 경우 <ul>의 자식들을 비워줌으로써 페이지의 DOM 개수가 너무 많아 랜더링이 느려지는 현상을 방지한다. (<ul>에서 높이를 유지하기 때문에 스크롤은 유지됨) <br>

<br>

다시 스크롤을 올려 viewport 영역으로 들어올시 역순으로  <li>이미지를 추가하며 랜더링한다. <br>

<br><br>

### img가 나열된 경우 스크롤시 lazy loading

스크롤이 존재하는 영역안에 여러 <img> 가 존재하는 경우 스크롤에 따라 lazy loading을 구현 할 수 있다. <br>

최초 랜더링시 img를 가져올 주소를 data-src와 같은 곳에 설정, img를 target으로 두고 노출여부 isIntersecting 되었을 경우 data-src 주소를 src에 넣어 img가 랜더링되도록 한다. <br>

```html
<!-- 노출전 -->
<img class="lazyImg" src="blank.png" data-src="img.png" />
<img class="lazyImg" src="blank.png" data-src="img.png" />
<img class="lazyImg" src="blank.png" data-src="img.png" />

<!-- 노출후 -->
<img class="lazyImg" src="img.png" data-src="img.png" />
```

<br>

```javascript
const imageObserver = new IntersectionObserver((entries, imgObserver) => {
    entries.forEach((entry) => {
        if(entry.isIntersecting) {
            const lazyImage = entry.target;
            lazyImage.src = lazyImage.dataset.src;
						imageObserver.unobserve(lazyImage);
        }
    })
});

imageObserver.observe(document.querySelectorAll('img.lazyImg'));
```

<br><br>

[ref]:
- [Intersection Observer API](https://developer.mozilla.org/ko/docs/Web/API/Intersection_Observer_API)

<br><br><br>