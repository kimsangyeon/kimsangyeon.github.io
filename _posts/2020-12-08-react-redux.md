---
layout: post
title: 'React-redux'
categories: [javascript, react]
image: assets/images/banner/redux.png
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

첫번째로 설정하는 mapStateToProps는 store가 변경될시 해당 상태를 연결한 컴포넌트의 Props로 전달해 줄 수 있다 store의 상태가 변경되면 첫번째 파라미터 state로 전달 받을 수 있다. <br>

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

# useSelector

`React-redux`에서 상위 컴포넌트에 connect()로 랩핑 하였던 방식의 대안으로 Hooks API를 제공한다.

대신 `React redux Hooks API` 사용을 위해서는 connect와 같이 <Provider>로 구성요소를 랩핑하여 구성요소 전체에서 저장소를 사용할 수 있도록 해야한다.

```jsx
const store = createStore(rootReducer);

ReactDOM.render(
	<Provider store={store}>
		<App />
	</Provider>,
	document.getElementById('root');
);
```

위처럼 설정이 되었다면 해당 구성 요소 내에서 `React redux Hooks API`를 사용하여 저장소에 접근 할 수 있다.

<br><br>

## useSelector()

```jsx
const result: any = useSelector(selector: Function, equalityFn?: Function)
```

selector의 function은 connect에 인자로 사용되는 mapStateToProps와 거의 동일하다. selector의 function은 Redux Store를 구독하고 action이 전달되고 실행될때마다 실행된다. <br>

<br>

`useSelector`에 사용된 selector와 mapState 차이

- selector는 객체뿐 아니라 모든 값을 반환 할 수 있다. selector의 반환값은 useSelector의 반환값으로 사용된다.
- 액션이 전달되면 `useSelector`는 이전 selector 결과 값과 현재 결과 값의 참조 비교를 수행한다. 값이 서로 다른 경우 재랜더링을 수행한다.
- `useSelector`는 참조 동등성으로 검사한다.
- selector의 결과값을 비교할때 참조값을 비교하기 때문에 결과값이 primitive한 리터럴 값이라면 equalityFn 옵션을 넣어 값 비교를 해야한다.

<br>

단일 Component 내에 `useSelector`를 여러번 호출 할 수 있다. useSelector()를 호출할 때 마다 개별 구독이 생성된다. <br>

<br><br>

### Equality Comparisons and Updates

`useSelector`의 selector 함수에서 새로운 객체를 반환하게 되면 얕은 비교로 참조값이 바뀐걸로 판단하여 항상 재랜더링 하게 된다. 기본적으로 `react-redux`에서 제공하는 shallowEqual을 equalityFn 옵션을 설정해준다면 객체의 1 뎁스의 정보들을 비교하여 결과 값의 변화를 감지한다. 하지만 뎁스가 깊은 객체인 경우에는 정확한 비교가 이루어지지 못해 정확한 비교가 이루어지지 못한다. 해서 깊은 비교를 위해 Lodash.isEqual() 이나 immutable.js 같은 비교기능을 사용해야한다. <br>

```jsx
import { shallowEqual, useSelector } from 'react-redux'

// later
const selectedData = useSelector(selectorReturningObject, shallowEqual)
```

<br><br>

### Using memoizing selectors

`useSelector`의 경우 store의 상태가 변경 될때 구독하고 있던 `useSelector`는 결과값 비교를 위해 호출되는데 불필요한 호출을 줄여 성능을 개선하기 위해 `reselect`에서 제공되는 `createSelector`를 사용할 수 있다. <br>

<br>

`createSelector` 사용시 전달되는 인자값을 메모이제이션하여 값을 기억하고 있는다. 그리고 재호출시 기억하고 있던 값과 인자값이 같은 경우 selector가 재계산을 수행하지 않는다. 이는 불필요한 재계산 수행을 줄임으로써 성능 향상에 도움이 된다. <br>

```jsx
import React from 'react'
import { useSelector } from 'react-redux'
import { createSelector } from 'reselect'

const selectNumOfDoneTodos = createSelector(
  state => state.todos,
  todos => todos.filter(todo => todo.isDone).length
)

export const DoneTodosCounter = () => {
  const NumOfDoneTodos = useSelector(selectNumOfDoneTodos)
  return <div>{NumOfDoneTodos}</div>
}

export const App = () => {
  return (
    <>
      <span>Number of done todos:</span>
      <DoneTodosCounter />
    </>
  )
}
```

<br><br>

[Ref] :

- [React and Key](https://ko.reactjs.org/docs/lists-and-keys.html)
- [Reconciliation List 처리](https://ko.reactjs.org/docs/reconciliation.html#recursing-on-children)
- [Index as a key is an anti-pattern](https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318)

<br><br><br>