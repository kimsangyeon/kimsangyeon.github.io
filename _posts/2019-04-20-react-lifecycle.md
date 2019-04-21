---
layout: post
title: "React Life Cycle" 
categories: [ javascript, react ]
image: assets/images/banner/react.png
featured: false
author: yeon
---


## React Life Cycle
컴포넌트가 브라우저에 나타나고, 사라지고, 업데이트 될때의 과정을 알아보자.

### init Component

> constructor

```javascript
constructor(props) {
    super(props);
}
```

컴포넌트가 새로 만들어질때 호출됨

> componentWillMount

```javascript
componentWillMount() {

}
```
컴포넌트가 화면에 나가기전에 호출되는 API. deprecated도어 v16.3이후부터 UNSAFE_componentWillmount()로 사용됨

> componentDidMount

```javascript
componentDidMount() {
  // 외부 라이브러리 연동: D3, masonry, etc
  // 컴포넌트에서 필요한 데이터 요청: Ajax, GraphQL, etc
  // DOM 에 관련된 작업: 스크롤 설정, 크기 읽어오기 등
}
```

컴포넌트가 화면에 나갔을때 호출되는 API. DOM 속성가져오기 및 변경 작업을 주로 함



<br><br><br>