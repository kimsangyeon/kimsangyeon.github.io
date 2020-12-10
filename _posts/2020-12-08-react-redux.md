---
layout: post
title: 'React List Key'
categories: [javascript, react]
image: assets/images/banner/react.png
author: yeon
---

# React-redux

React 에서 Redux를 사용할 수 있도록 도와주는 라이브러리로 Redux의 상태를 React View로 전달해주는 역할을 한다. <br>

<br>

### <Provider>

Provider 컴포넌트를 사용하여 사용할 앱 하위로 redux store를 연결하여 사용할 수 있도록 해준다. <br>

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import { Provider } from 'react-redux'

import { App } from './App'
import createStore from './createReduxStore'

const store = createStore()

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

Provider로 사용할 store를 지정하게 되면 App 컴포넌트에서 store에 접근 할 수 있게된다. <br>

<br><br>

### connect

react-redux에서 제공하는  connect()함수는 React 구성 요소를 Redux 저장소에 연결한다. <br>

```jsx
function connect(mapStateToProps?, mapDispatchToProps?, mergeProps?, options?)
```

<br>

#### mapStateToProps

천번째로 설정하는 mapStateToProps는 store가 변경될시 해당 상태를 연결한 컴포넌트의 Props로 전달해 줄 수 있다 store의 상태가 변경되면 첫번째 파라미터 state로 전달 받을 수 있다. <br>

```jsx
const mapStateToProps = state => ({ todos: state.todos })
```

<br>

두번째 파라미터로 전달되는 ownProps는 컨테이너 컴포넌트에 설정된 props로 해당 props 값을 이용하여 state의 상태를 결정 및 사용할 수 있다.

```jsx
const mapStateToProps = (state, ownProps) => ({
  todo: state.todos[ownProps.id]
})
```

mapStateToProps 반환 값은 설정된 컴포넌트의 props로 사용될 수 있다. <br>

<br>

#### mapDispatchToProps

connect의 두번째 인자로 설정되는 mpaDispatchToProps는 Redux의 store를 변경 할 수 있는 dispatch를 제공한다. <br>

```jsx
const mapDispatchToProps = dispatch => {
  return {
    // dispatching plain actions
    increment: () => dispatch({ type: 'INCREMENT' }),
    decrement: () => dispatch({ type: 'DECREMENT' }),
    reset: () => dispatch({ type: 'RESET' })
  }
}
```

<br>

mapDispatchToProps는 Redux의 dispatch를 첫번째 인자로 받아 action을 호출 할 수 있게 해준다. <br>

```jsx
// binds on component re-rendering
<button onClick={() => this.props.toggleTodo(this.props.todoId)} />

// binds on `props` change
const mapDispatchToProps = (dispatch, ownProps) => {
  toggleTodo: () => dispatch(toggleTodo(ownProps.todoId))
}
```

props로 반환된 dispatch 액션을 수행하여 store의 상태 변경을 할 수 있다.

<br>

#### mergeProps

connect의 세번째 파라미터 mergeProps는 실제로 컴포넌트가 가지게될 props값인데 실질적으로는 잘 사용되지 않으며 설정하지 않을시 상위 컴포넌트에서 받은 props, 그리고 mapStateToProps, mapDispatchToProps에서 반환된 값인 { ...ownProps, ...stateProps, ...dispatchProps } 값으로 지정된다.

<br><br>

[Ref] :

- [React and Key](https://ko.reactjs.org/docs/lists-and-keys.html)
- [Reconciliation List 처리](https://ko.reactjs.org/docs/reconciliation.html#recursing-on-children)
- [Index as a key is an anti-pattern](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)

<br><br><br>