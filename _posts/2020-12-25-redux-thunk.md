---
layout: post
title: 'Redux Thunk'
categories: [javascript, redux]
image: assets/images/banner/redux.png
author: yeon
---

# Redux Thunk

리덕에서는 비동기처리를 위해 여러 미들웨어를 사용한다. `redux-thunk` `redux-saga` `redux-observable` `redux-promise-middleware` 등이 있다. 이중에 `redux-thunk`에 대해 간략히 정리하고자 한다. <br>

<br><br>

## Redux middleware

일단 리덕스 미들웨어는 리덕스에서 액션이 디스패치된 이후에 리듀서에서 상태를 변경하기 전에 추가 작업을 할 수 있도록 도와준다. 
상태를 변경하기전 액션을 취소하거나 콘솔에 액션 혹은 상태값 출력, 그리고 상태값을 변경하여 리듀서에 전달 할 수도 있다. 
다른 것으로는 특정 액션이 발생 하였을때 다른 액션을 발생하게 하거나 함수를 실행 시킬 수 있다.

<br>

일반적으로 미들웨어는 비동기 작업을 처리 할 때 많이 사용되며 API 호출을 위해 사용한다. <br>

<br>

미들웨어는 `redux`의 `applyMiddleware`를 사용하여 `createStore`로 store 생성시 사용한다. <br>

```javascript
import { createStore, applyMiddleware } from 'redux';
import ReduxThunk from './redux-thunk';
import reducer from './reducer';

const store = createStore(reducer, applyMiddleware(ReduxThunk));
```

<br><br>

## Redux thunk

Dan Abramov가 만든 `redux-thunk`는 단순하게 액션이 함수인 경우 내부에서 액션 함수를 만들어주는 역할을 한다.
`redux-thunk`의 코드를 보더라도 아주 간단하게 코드가 작성된 것을 알 수 있다. <br>

```javascript
function createThunkMiddleware(extraArgument) {
  return ({ dispatch, getState }) => (next) => (action) => {
    if (typeof action === 'function') {
      return action(dispatch, getState, extraArgument);
    }

    return next(action);
  };
}

const thunk = createThunkMiddleware();
thunk.withExtraArgument = createThunkMiddleware;

export default thunk;
```

수행된 액션이 function 인 경우 action에 dispatch와 state를 넘겨 수행시켜주는 역할이 전부이다. <br>

<br>

해서 API 액션을 dispatch 할때에 함수가 반환되는 thunk 함수를 만들어 dispatch로 호출하면된다.

```javascript
function getData() {
  return (dispatch) => {
    dispatch({type: 'GET_DATA'});

    fetch('/data', {method: 'GET'}).then(data => {
      dispatch({type: 'GET_DATA_SUCCESS', data});
    }).catch(e => {
      dispatch({type: 'GET_DATA_FAILURE', error: e});
    });
  };
}

// event
dispatch(getData());
```

위와 같이 함수를 리턴하는 getData를 dispatch로 호출하여 `redux-thunk` 미들웨어에서 액션 함수를 호출할 수 있는 형태로 동작하도록 만든다. <br>

<br>

위와 같이 작성된 코드는 `async` `await`을 사용하여 작성도 가능하다. <br>

```javascript
function getData() {
  return async (dispatch) => {
    dispatch({type: 'GET_DATA'});

    const data = await fetch('/data', {method: 'GET'});
    try {
      dispatch({type: 'GET_DATA_SUCCESS', data});
    } catch (e) {
      dispatch({type: 'GET_DATA_FAILURE', error: e});
    }
  };
}

// event
dispatch(getData());
```

<br><br>

[Ref] :

- [redux-thunk](https://github.com/reduxjs/redux-thunk/blob/master/src/index.js)


<br><br><br>