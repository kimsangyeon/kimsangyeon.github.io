---
layout: post
title: 'React List Key'
categories: [javascript, react]
image: assets/images/banner/react.png
author: yeon
---

# React List Key

React에서 리스트 랜더링시 key 값을 지정하지 않을 경우 key값 지정에 대한 경고문이 노출된다. <br>

- key는 배열로 생성되는 React Element 생성 구간에서 key를 지정해 주어야한다. <br> (ex: map 내부에서 생성되는 컴포넌트)
- key는 형제 컴포넌트 사이에서만 고유하면 된다.
- key 값을 지정하지 않는 경우 인덱스 값으로 key 값이 지정된다.

<br>

아래와 같이 map으로 React Component를 가지는 배열을 주입하여 랜더링이 가능하다. <br>

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

<br><br>

JSX 내부에 map 함수를 사용하여 결과를 인라인 형태로 처리할 수도 있다. <br>

```jsx
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {
        numbers.map((number) =>
          <ListItem
            key={number.toString()}
            value={number}
          />)
      }
    </ul>
  );
}
```

<br><br>

## 왜 key가 필요한가

React는 재조정알고리즘에서 이전 DOM과 새로 생성된 DOM을 비교하여 차이점이 있는 경우 변경을 생성한다. <br>

```html
<ul>
  <li>first</li>
  <li>second</li>
</ul>
-------------------
<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
```

위와 같은 두개의 리스트가 있다면 마지막으로 새롭게 추가된 `<li>thrid</li>` 를 추가할 것이다. <br>

<br>

하지만 맨위의 자식하나가 추가되는 경우라면? <br>

```html
<ul>
  <li>second</li>
  <li>third</li>
</ul>
-------------------
<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
```

이러한 경우에는 변경사항에 대해 첫번째 자식 변경을 감지하고 리스트 내의 모든 자식을 새롭게 변경한다. <br>

이는 비효율적인 랜더링을 발생 시킬 수 있다. <br>

<br>

여기서  React는 `key`라는 속성을 사용하여 key를 통해 기존 트리와 새롭게 생성된 트리를 검사한다. <br>

```html
<ul>
  <li key="two">second</li>
  <li key="three">third</li>
</ul>
-------------------
<ul>
  <li key="one">first</li>
  <li key="two">second</li>
  <li key="three">third</li>
</ul>
```

`key` 를 검사하여 'two'와 'three' key를 가지는 엘리먼트는 변경사항이 없고 위에 `one' key를 가지는 새로운 엘리먼트를 추가 하는 동작만 수행한다. 리스트 내의 순서가 바뀌는 경우에도 단순히 엘리먼트 위치를 이동시켜주는 것으로 랜더링을 최적화 한다. <br>

<br>

여기서 단순히 인덱스를 key로 사용하였을때 문제를 예상할 수 있다. 리스트를 생성할 당시 인덱스를 사용한다면 1 ,2, 3 과 같은 순서로 key값이 주어질 것이다. <br>

```html
<ul>
  <li key=1>second</li>
  <li key=2>third</li>
</ul>
-------------------
<ul>
  <li key=1>first</li>
  <li key=2>second</li>
  <li key=3>third</li>
</ul>
```

위와 같은 경우 key값으로 리스트의 요소의 변경을 비교하게 된다면 이전 랜더링에서 key 1을 가지는 second와 새롭게 생성된 key 1을 가지는 first와 비교하여 변경되었다 판단하여 새롭게 랜더링을 수행할 것이다. 이러한 동작은 불필요한 랜더링을 유발시켜 성능에 문제를 발생 시킬 수 있다. <br>

<br><br>

[Ref] :

- [React and Key](https://ko.reactjs.org/docs/lists-and-keys.html)
- [Reconciliation List 처리](https://ko.reactjs.org/docs/reconciliation.html#recursing-on-children)
- [Index as a key is an anti-pattern](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)

<br><br><br>