---
layout: post
title: 'React Component State'
categories: [javascript, react]
image: assets/images/banner/react.png
author: yeon
---

# React Component State

`React` 에서 State는 컴포넌트의 상태 값을 가리킨다. `setState` 를 통해 상태 값 변경이 가능하고 상태 값이 변경되면 컴포넌트는 리랜더링 된다. <br>

<br>

## State & Props

State는 컴포넌트의 상태 값으로 컴포넌트 내부에서 관리되는 값이다. Props는 Properties의 줄임말로 함수의 매개변수와 같이 컴포넌트로 전달되는 값이다. State가 하위컴포넌트로 전달되고 하위컴포넌트는 이 값을 Props로 받게 된다. <br>

<br><br>

## State 일괄처리

컴포넌트에서 state를 변경하기위해 `setState`를 사용할 때 `setState`가 여러 번 호출된다면? 랜더링이 계속 일어나는가?.. 이 답은 아니다. `setState`에 새롭게 설정할 상태 값인 객체를 전달하게 되는 경우 마지막으로 설정된 State로 랜더링이 된다. <br>

```jsx
incrementCount() {
  // 주의: 이 코드는 예상대로 동작하지 *않을 것*입니다.
  this.setState({count: this.state.count + 1});
}

handleSomething() {
  // `this.state.count`가 0에서 시작한다고 해봅시다.
  this.incrementCount();
  this.incrementCount();
  this.incrementCount();
  // React가 컴포넌트를 리렌더링할 때 `this.state.count`는 3이 될 것 같은 예상과 달리 1이 됩니다.

  // 이것은 `incrementCount()` 함수가 `this.state.count`에서 값을 읽어 오는데
  // React는 컴포넌트가 리렌더링될 때까지 `this.state.count`를 갱신하지 않기 때문입니다.
  // 그러므로 `incrementCount()`는 매번 `this.state.count`의 값을 0으로 읽은 뒤에 이 값을 1로 설정합니다.

  // 이 문제의 해결 방법은 아래에 설명되어 있습니다.
}
```

`setState`호출할 때마다 리랜더링 되지 않아 this.state 값이 갱신되지 않기 때문에 this.state.count 값은 1이 된다. <br>

<br>

위의 문제점 해결은 `setState`에 함수를 전달하는 방법으로 해결이 가능하다. `setState`에 전달되는 함수는 이전 상태 값 state에 접근 할 수 있고 `setState` 호출은 일괄처리되며 이전에 있었던 문제가 해결된다. <br>

```jsx
incrementCount() {
  this.setState((state) => {
    // 중요: 값을 업데이트할 때 `this.state` 대신 `state` 값을 읽어옵니다.
    return {count: state.count + 1}
  });
}

handleSomething() {
  // `this.state.count`가 0에서 시작한다고 해봅시다.
  this.incrementCount();
  this.incrementCount();
  this.incrementCount();

  // 지금 `this.state.count` 값을 읽어 보면 이 값은 여전히 0일 것입니다.
  // 하지만 React가 컴포넌트를 리렌더링하게 되면 이 값은 3이 됩니다.
}
```

`setState`에 partialState 인자가 object, function인 경우 `updater.enqueueSetState`로 설정한다. <br>

<br>

#### react/src/ReactBaseClasses.js

```jsx
Component.prototype.setState = function(partialState, callback) {
  invariant(
    typeof partialState === 'object' ||
      typeof partialState === 'function' ||
      partialState == null,
    'setState(...): takes an object of state variables to update or a ' +
      'function which returns an object of state variables.',
  );
  this.updater.enqueueSetState(this, partialState, callback, 'setState');
};
```

`classComponentUpdater`를 거쳐 `enqueueUpdate`로 update 정보가 설정 <br>

<br>

#### react-reconciler/src/ReactFiberClassComponenet.js

```jsx
const classComponentUpdater = {
  isMounted,
  enqueueSetState(inst, payload, callback) {
    const fiber = getInstance(inst);
    const eventTime = requestEventTime();
    const lane = requestUpdateLane(fiber);

    const update = createUpdate(eventTime, lane);
    update.payload = payload;
    if (callback !== undefined && callback !== null) {
      if (__DEV__) {
        warnOnInvalidCallback(callback, 'setState');
      }
      update.callback = callback;
    }

    enqueueUpdate(fiber, update);
    scheduleUpdateOnFiber(fiber, lane, eventTime);

    ...
  },
```

payload가 function인 경우 이전 state로 설정하여 호출하는 것을 볼 수 있다. <br>

<br>

#### react-reconciler/src/ReactUpdateQueue.js

```jsx
function getStateFromUpdate<State>(
  workInProgress: Fiber,
  queue: UpdateQueue<State>,
  update: Update<State>,
  prevState: State,
  nextProps: any,
  instance: any,
): any {
  switch (update.tag) {
    case ReplaceState: {
      const payload = update.payload;
      if (typeof payload === 'function') {
        // Updater function
        if (__DEV__) {
          enterDisallowedContextReadInDEV();
        }
        const nextState = payload.call(instance, prevState, nextProps);
        
				...
    }
```

위의 예시는 `React Class Component` 인 상황에 해당되며 `Functional Component Hook`인 `useState`의 경우에는 `ReactFiberHooks.js`를 참고하여야 한다. <br>

<br><br>

[Ref] :

- [컴포넌트 State](https://ko.reactjs.org/docs/faq-state.html)

<br><br><br>