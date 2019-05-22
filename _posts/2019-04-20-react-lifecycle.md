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

<br>

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
컴포넌트가 화면에 나가기전에 호출되는 API. deprecated되어 v16.3이후부터 UNSAFE_componentWillmount()로 사용됨

> componentDidMount

```javascript
componentDidMount() {
  // 외부 라이브러리 연동: D3, masonry, etc
  // 컴포넌트에서 필요한 데이터 요청: Ajax, GraphQL, etc
  // DOM 에 관련된 작업: 스크롤 설정, 크기 읽어오기 등
}
```

컴포넌트가 화면에 나갔을때 호출되는 API. DOM 속성가져오기 및 변경 작업을 주로 함 <br>

<br>

### update Component

<br>

#### componentWillReceiveProps

```javascript
componentWillReceiveProps(nextProps) {
  // this.props 는 아직 바뀌지 않은 상태
}
```

컴포넌트가 새로운 props를 받았을때 호출되는 API. deprecated되어 v16.3이후부터 UNSAFE_componentWillReceiveProps()로 사용됨 <br>

<br>

#### getDerivedStateFromProps

```javascript
static getDerivedStateFromProps(nextProps, prevState) {
  // 여기서는 setState 를 하는 것이 아니라
  // 특정 props 가 바뀔 때 설정하고 설정하고 싶은 state 값을 리턴하는 형태로
  // 사용됩니다.
  /*
    if (nextProps.value !== prevState.value) {
        return { value: nextProps.value };
    }
    return null; // null 을 리턴하면 따로 업데이트 할 것은 없다라는 의미
  */
}
```
v16.3이후 생긴 컴포넌트 API. props로 받아온 값을 state로 동기화 시켜줘야할때 사용. <br>


<br>

#### shouldComponentUpdate

```javascript
shouldComponentUpdate(nextProps, nextState) {
  // return false 하면 업데이트를 안함
  // return this.props.checked !== nextProps.checked
  return true;
}
```

render 전에 호출되는 컴포넌트 API이며, 리랜더링 최적화에 도움을 준다. 리액트는 변화된 부분을 감지하기위해 virtual DOM에 한번 랜더링을 하여 비교후에 변경된 사항들을 랜더링한다. virtual DOM에 랜더링되는 자원을 최적화하기위해 이 API를 사용하여 prop이 변경이 없는 경우에 false를 리턴하여 랜더링 하지 않게 한다. 기본값은 true 리턴. <br>

<br>

#### componentWillUpdate

```javascript
componentWillUpdate(nextProps, nextState) {

}
```

shouldComponentUpdate에서 true를 리턴한 경우 호출되는 API. 애니메이션 초기화, 이벤트리스너 제거등에 사용된다고 한다. 
deprecated되어 v16.3이후부터 getSnapshotBeforeUpdate()로 대체하여 사용한다. <br>

<br>

#### getSnapshotBeforeUpdate

```javascript
getSnapshotBeforeUpdate(prevProps, prevState) {

}
```

render 직후 DOM변화가 일어나기 전에 호출되는 API. 여기서 리턴되는 값은 componentDidMount 세번째 인자값인 snapshot 값으로 받아 처리 가능하다. <br>

1. render()
2. getSnapshotBeforeUpdate()
3. 실제 DOM 에 변화 발생
4. componentDidUpdate

<br><br>

#### componentDidMount

```javascript
componentDidUpdate(prevProps, prevState, snapshot) {

}
```

render 이후에 호출되는 API이며, 이 시점에선 props와 state가 바뀌어 있다. 파라미터를 통해 이전의 값인 prevProps 와 prevState 를 조회 할 수 있고, getSnapshotBeforeUpdate에서 리턴된 세번째 인자인 snapshot 값을 받을 수 있다. <br>

<br>

### remove Component

<br>

#### componentWillUnMount

```javascript
componentWillUnmount() {
  // 이벤트, setTimeout, 외부 라이브러리 인스턴스 제거
}
```

컴포넌트가 필요하지 않게 되었을때 호출하는 API. 이벤트제거와 setTimeout clear 혹은 외부 라이브러리 제거 등에 사용된다. <br>

<br>

### error Component

<br>

#### ComponentDidCatch

```javascript
componentDidCatch(error, info) {
  this.setState({
    error: true
  });
}
```

render에서 에러 발생시 호출되는 API. 위의 예제처럼 에러 발생시 state error true로 설정하여, render에서 에러 처리 가능. 컴포넌트 자신의 render 함수 에러는 잡지 못하지만, 내부 자식 컴포넌트에서 발생하는 에러는 잡을 수 있다고 한다. <br>

<br>

```javascript
componentDidCatch(error, info) {
    this.setState({
      error: true
    });
  }
  
  render() {
    if (this.state.error) return (<h1>에러발생!</h1>);

    return (
```

render 예외처리

<br><br><br>