---
layout: post
title: 'Reduce-Reducers'
categories: [javascript, redux, reduce-reducers]
image: assets/images/banner/redux.png
author: yeon
---

# reduceReducers

프로젝트에서 사용중인 reduceReducers에 대해서 정리하고자한다. 해당 모듈은 reduce-reducers 모듈로 중첩없이 reducer를 간단하게 병합시켜주는 역할을 한다. <br>

<br>

reducer의 병합이라고하면 많이들 사용하는 combineReducers가 생각날텐데 두가지의 차이점을 알아보자. <br>

<br>

간단하게 두가지의 차이점은 중첩 상태로 병합하느냐 중첩하지 않고 병합하느냐의 차이로 나뉘어진다. <br>

- combineReducers: 중첩상태로 병합
- reduceReducers: 중첩되지 않게 병합

<br>

```js
// this reducer adds a payload to state.sum
// and tracks total number of operations
function reducerAdd(state, payload) {
  if (!state) state = { sum: 0, totalOperations: 0 }
  if (!payload) return state

  return {
    ...state,
    sum: state.sum + payload,
    totalOperations: state.totalOperations + 1
  }
}

// this reducer multiplies state.product by payload
// and tracks total number of operations
function reducerMult(state, payload) {
  if (!state) state = { product: 1, totalOperations: 0 }
  if (!payload) return state

  // `product` might be undefined because of
  // small caveat in `reduceReducers`, see below
  const prev = state.product || 1

  return {
    ...state,
    product: prev * payload,
    totalOperations: state.totalOperations + 1
  }
}
```

<br><br>

## combineReducers

- combineReducers는 각 상태를 나뉘며 root Reducer를 만들때 유용하다. <br>

<br>

```js
const rootReducer = combineReducers({
  add: reducerAdd,
  mult: reducerMult
})

const initialState = rootReducer(undefined)
/*
 * {
 *   add:  { sum: 0, totalOperations: 0 },
 *   mult: { product: 1, totalOperations: 0 },
 * }
 */

const first = rootReducer(initialState, 4)
/*
 * {
 *   add:  { sum: 4, totalOperations: 1 },
 *   mult: { product: 4, totalOperations: 1 },
 * }
 */
// This isn't interesting, let's look at second call...

const second = rootReducer(first, 4)
/*
 * {
 *   add:  { sum: 8, totalOperations: 2 },
 *   mult: { product: 16, totalOperations: 2 },
 * }
 */
// Now it's obvious, that both reducers get their own
// piece of state to work with
```

<br><br>

## reduceReducers

- reduce-reducers는 동일한 상태에서 동작해야하는 여러 reducer를 연결할때 유용하다. <br>

<br>

```js
const addAndMult = reduceReducers(reducerAdd, reducerMult)

const initial = addAndMult(undefined)
/*
 * {
 *   sum: 0,
 *   totalOperations: 0
 * }
 *
 * First, reducerAdd is called, which gives us initial state { sum: 0 }
 * Second, reducerMult is called, which doesn't have payload, so it
 * just returns state unchanged.
 * That's why there isn't any `product` prop.
 */

const next = addAndMult(initial, 4)
/*
 * {
 *   sum: 4,
 *   product: 4,
 *   totalOperations: 2
 * }
 *
 * First, reducerAdd is called, which changes `sum` = 0 + 4 = 4
 * Second, reducerMult is called, which changes `product` = 1 * 4 = 4
 * Both reducers modify `totalOperations`
 */

const final = addAndMult(next, 4)
/*
 * {
 *   sum: 8,
 *   product: 16,
 *   totalOperations: 4
 * }
 */
```

<br><br>

[Ref]:

- [correct usage of reduce-reducers](https://stackoverflow.com/questions/38652789/correct-usage-of-reduce-reducers/44371190#44371190)

<br><br><br>