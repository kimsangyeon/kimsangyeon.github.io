---
layout: post
title: 'getElementsByClassName querySelectorAll'
categories: [html]
image: assets/images/banner/html.png
author: yeon
---

# getElementsByClassName querySelectorAll

getElementsByClassName, querySelectorAll 두 WebAPI의 간단한 차이점을 정리해 보자면 <br>
반환값이 서로 다르다는점과 querySelector의 경우 selector를 사용하여 여러 조건으로 탐색이 가능하다는 차이가 있겠다. 속도 적인 측면에서는 대략 10만개 Element를 가지는 root 기준으로 className 탐색을 검사하였을때 5ms 정도의 차이로 거의 차이가 나지 않는 것을 확인하였다. <br>

<br>

#### parameters

- getElementsByClassName: className
- querySelectorAll: selectors

<br>

#### return

- getElementsByClassName: HTMLCollection
- querySelectorAll: NodeList

<br><br>

## getElementsByClassName

**getElementsByClassName** 인자값으로 검색할 클래스 혹은 클래스를 띄어쓰기로 구분한 값을 받으며, <br>
반환 값은 실시간으로 업데이트되는 해당 클래스명을 가진 요소 목록의 **HTMLCollection** 이 반환된다. <br>
변수에 해당 HTMLCollection을 반환 받을 경우  Collection 변화에 따라 실시간으로 값이 변하게 된다. <br>

<br>

```html
<ul id="ul">
	<li class="li">1</li>
	<li class="li">2</li>
	<li class="li">3</li>
	<li class="li">4</li>
</ul>
```

```jsx
const ul = document.getElementById('ul');
const classLi = ul.getElementsByClassName('li');

console.log(classLi);
// HTMLCollection(4) [li.li, li.li, li.li, li.li]

const elLi = document.createElement('li');
elLi.className = 'li';
ul.append(elLi);

console.log(classLi);
// HTMLCollection(5) [li.li, li.li, li.li, li.li, li.li]
```

<br><br>

## querySelectorAll

**querySelectorAll**은 셀렉터 그룹에 일치하는 NodeList를 반환한다. 반환된 NodeList는 변하지않는 정적데이터로 셀렉터에 해당하는 그룹이 변경되더라도 변경되지 않는다. <br>

<br>

```html
<ul id="ul">
	<li class="li">1</li>
	<li class="li">2</li>
	<li class="li">3</li>
	<li class="li">4</li>
</ul>
```

```jsx
const ul = document.getElementById('ul');
const queryLi = ul.querySelectorAll('.li');

console.log(queryLi);
// NodeList(4) [li.li, li.li, li.li, li.li]

const elLi = document.createElement('li');
elLi.className = 'li';
ul.append(elLi);

console.log(queryLi);
// NodeList(4) [li.li, li.li, li.li, li.li]
```

<br><br>

## querySelector

**querySelector**는 셀렉터에 해당하는 첫번째 Element를 반환하며 일치하는 요소가 없는 경우 null을 반환한다. <br>
원하는 요소가 단일 요소인 경우 getElementsByclassName, querySelectorAll 보다는 요긴하게 쓰일 수 있다. <br>

<br>

```html
<ul id="ul">
	<li class="li">1</li>
	<li class="li">2</li>
	<li class="li">3</li>
	<li class="li">4</li>
</ul>
```

```jsx
const ul = document.getElementById('ul');
const queryLi = ul.querySelector('.li');

console.log(queryLi);
// <li class="li">1</li>
```
<br><br>

[ref]:
- [Element.getElementsByClassName()](https://developer.mozilla.org/ko/docs/Web/API/Element/getElementsByClassName)
- [Document.querySelectorAll()](https://developer.mozilla.org/ko/docs/Web/API/Document/querySelectorAll)
- [Document.querySelector()](https://developer.mozilla.org/ko/docs/Web/API/Document/querySelector)

<br><br><br>