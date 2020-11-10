---
layout: post
title: 'Redux structure'
categories: [javascript, redux]
image: assets/images/banner/redux.png
author: yeon
---

# Redux Structure

**Redux**는 자바스크립트 앱을 위한 예측 가능한 컨테이너이다. 싱글 페이지 앱이 점점 복잡해지고 그에 따른 많은 상태를 관리하는데 어려움이 생긴다. 상태를 어떻게 업데이트하고 언제 업데이트 할지, 상태가 변경되는 시점 관리등 상태로 인한 복잡도가 증가한다. <br>

<br>

**MVC의 복잡도**의 예로 모델이 다른 모델을 변경하고 모델로 인해 변경된 뷰가 다시 다른 모델을 변경하는 업데이트가 발생한다면 어디서 무엇이 변경되었는지 추적하기가 쉽지 않을 것이다. 이로 인하여 새로운 기능 및 요건들이 추가 될때마다 상태 변경에 따른 사이드 이펙트를 예측하기 어려울 것이다. <br>

<br>

위와 같은 문제를 해결하고자 상태 변화가 일어나는 시점과 흐름에 제약을 두어 상태변화를 예측하기 쉽게 하고자 **Flux**, **Redux**와 같은 상태변화 라이브러리가 만들어졌다. <br>

<br><br>

## Structure

**Redux** 구조는는 크게 액션, 리듀서, 스토어로 나눌수 있다.

<br>

### Action

액션은 앱에서 사용되는 데이터 묶음으로 리듀서에서 사용하게될 상태변경 로직 **type**과 **payload** 데이터를 가지고 있다. 액션은 단순한 자바스크립트 객체로 액션이 가지는 type은 일반 문자열 상수로 정의된다. 앱이 커질 경우 type을 별도로 분리하여 사용할 수도 있다. <br>

```jsx
// actionTypes
const SHOW_ALERT = 'SHOW_ALERT';
```

<br>

액션 생성자에서 action type과 payload 값을 객체(액션) 형태로 반환한다. 액션에는 가능한 작은 데이터를 설정하여 사용되는것이 좋다. <br>

```jsx
// actionCreator
function showAlert(text) {
	return {
		type: SHOW_ALERT,
		text
	};
}
```

<br><br>

이제 실제 액션을 보내기위해서는 **dispatch**를 사용하여 액션을 호출한다. <br>

```jsx
dispatch(showAlert(text));
```

<br><br>

기본 자바스크립트에서는 **store.dispatch**를 통해 액션 호출이 가능하다. <br>

```jsx
const TEXT = '경고';
.addEventListener('click', () => {
	store.dispatch(showAlert(TEXT));
});
```

<br><br>

React를 사용할 경우 store.dispatch 사용도 가능하지만 'react-redux' **connect**를 통한 dispatch 접근으로 액션 호출이 가능하다. <br>

```jsx
import React from 'react';
import { connect } from 'react-redux';
import { showAlert } from '../actions';

const App = ({ dispatch }) => {
	return (
		<div>
			<form onSubmit={e => {
				e.preventDefault();
				dispatch(showAlert('경고'));
			}}>
				<button type="submit">
					show alert
				</button>
			</form>
		</div>
	);
};

export default connect()(App);
```

<br><br>

### Reducer

리듀서에서는 앱의 상태가 어떻게 바뀌는지를 제어합니다. 이전 상태와 액션을 받아서 새로운 상태를 반환하는 순수함수이다. <br>

```jsx
(state, action) => newState
```

<br><br>

리듀서는 상태를 순수하게 유지하는것이 매우 중요하기 때문에 상태를 변경하거나 API 호출, 라우팅 전환과 같은 사이드 이펙트를 일으키면 안된다. 이전 상태는 직접 수정하지 않고 이전상태와 액션을 사용하여 새로운 상태 객체를 생성하여 반환하는 것이 중요하다. <br>

```jsx
function reducer(state = 0, action) {
	switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      return state
  }
}

function todos(state = initialState, action) {
	switch (action.type) {
    case 'ADD_TODO':
			return Object.assign({}, state, {// data});
		default:
			return state;
	}
}
```

<br><br>

위와같이 state는 직접 변경하지 않은채 새로운 상태를 반환하며 객체의 경우 Object assign을 사용하여 새로운 객체를 생성해낸다. Object assign이 아닌 ES7 문법인 전개 연산자인 { ...state, ...newState } 형태로도 가능하다. <br>

<br>

리듀서에 정의된 타입들이 많아질수록 리듀서가 복잡해 질 수 있다. 이를 위해 리듀서를 분리하고 조합도 가능하다. 연관된 상태변경 동작들을 함수 별로 나누고 리덕스에서 제공하는 combineRedueces를 사용하여 합칠 수 있다. <br>

```jsx
- todos.js -

const todos = (state = [], action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return [
        ...state,
        {
          id: action.id,
          text: action.text,
          completed: false
        }
      ];
    default:
      return state;
  }
}

- visibilityFilter.js -

const visibilityFilter = (state = VisibilityFilters.SHOW_ALL, action) => {
  switch (action.type) {
    case 'SET_VISIBILITY_FILTER':
      return action.filter;
    default:
      return state;
  }
}

- index.js -

import { combineReducers } from 'redux'
import todos from './todos'
import visibilityFilter from './visibilityFilter'

export default combineReducers({
  todos,
  visibilityFilter
})
```

<br><br>

### Store

스토어는 상태를 보관하고 있어 상태에 접근 가능하고 액션을 호출하여 상태 수정을 할 수 있다. <br>

- 애플리케이션의 상태를 저장
- `[getState()](https://dobbit.github.io/redux/api/Store.html#getState)`를 통해 상태에 접근
- `[dispatch(action)](https://dobbit.github.io/redux/api/Store.html#dispatch)`를 통해 상태를 수정
- `[subscribe(listener)](https://dobbit.github.io/redux/api/Store.html#subscribe)`를 통해 리스너를 등록

<br>

생성한 리듀서를 스토어에 넘겨주는것으로 스토어를 생성 할 수 있다. <br>
createStore 두번째 인수로 초기 상태도 지정 가능하다. <br>

```jsx
import reducer from './reducers'

const store = createStore(reducer);
```

<br><br>

dispatch를 통해 액션을 보내 상태 수정이 가능하고 subscribe에서 상태가 바뀔때마다 리스너를 등록 할 수 있다. <br>

```jsx
// 구독
const unsubscribe = store.subscribe(() => {
	console.log(store.getState());
});

// 액션
store.dispatch(showAlert('경고'));

// 구독취소
unsubscribe();
```

<br><br>

### Data Flow

리덕스에서 액션, 리듀서, 스토어 구조의 데이터 흐름은 단반향으로 진행된다. 단방향으로 진행되는 데이터 흐름은 앱 내의 모든 데이터가 같은 생명주기 패턴을 따르게 되고, 이는 앱의 상태 변화를 조금 더 예측 가능하기 좋게 한다. <br>

<br><br>

리덕스의 데이터 흐름을 4단계로 나누어보자. <br>

#### **1. store dispatch 를 통해 action을 호출**

```jsx
// action type
const ADD_TODO = 'ADD_TODO';

// action Creator
const addTodo = (todo) => {
	return {
		type: ADD_TODO,
		todo
	};
};

// dispatch
store.dispatch(addTodo(todo));
```

dispatch를 통해 어디서든 액션을 호출 할 수 있다.

<br><br>

#### **2. 리덕스 스토어가 리듀서 함수들을 호출**

스토어는 현재 상태와 액션 두가지를 리듀서에게 넘긴다. <br>

```jsx
const prevState = store.getState();
const action = {
	type: ADD_TODO,
	todo
};

const newState = reducer(prevState, action);
```

<br><br>

#### **3. 리듀서가 이전 상태와 액션으로 새로운 상태를 반환**

```jsx
function reducer(state = initialState, action) {
	switch(action.type) {
		case 'TODO':
			return {
				...state,
				todos: state.todos.concat([action.todo])
			};
		default:
			return state;
	}
}
```

리듀서는 순수함수로 리듀서 안에서 일어나는 계산은 완전 예측 가능하여야한다. 같은입력에 대해서는 항상 같은 결과를 반환해야한다. 때문에 API 호출이나 라우터 전환, new Date(), Math.random() 과 같은 호출은 이루어져서는 안된다. <br>

<br><br>

#### **4. 스토어가 리듀서에서 반환된 결과를 새로운 상태로 저장**

store.subscribe를 통해 새로운 상태를 확인할 수 있으며 상태는 store.getState()로 호출 가능하다. <br>

<br>

스토어에 새로운 상태가 저장된 이후에 새로운 상태가 UI에 반영되게 되며 리액트의 경우 react-redux를 통해 바인딩이 되었다면 해당시점에서 component.setState(newState)가 호출되고 새로운 상태로 리액트 랜더링이 진행된다. <br>

<br><br>

[ref]:
- [Redux Data Flow](https://dobbit.github.io/redux/basics/DataFlow.html)

<br><br><br>