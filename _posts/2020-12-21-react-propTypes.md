---
layout: post
title: 'React PropTypes'
categories: [javascript, react]
image: assets/images/banner/react.png
author: yeon
---

# React PropTypes

개발하는 앱이 커질수록 타입 확인을 통하여 미리 많은 버그들을 잡아낼 수 있다. Flow 또는 Typescript를 활용하여 Javascript 타입을 확인 할 수 있다. React에서는 Reqct에 내장된 컴포넌트의 props 타입 확인을 지원하며 prop-types 라이브러리와 함께 props 타입 검사가 가능하다. <br>

<br>

15.5버전 부터는 prop-types 라이브러리를 임포트 해주어 사용해야한다. <br>

```jsx
// Before (15.4 and below)
import React from 'react';

class Component extends React.Component {
  render() {
    return <div>{this.props.text}</div>;
  }
}

Component.propTypes = {
  text: React.PropTypes.string.isRequired,
}

// After (15.5)
import React from 'react';
import PropTypes from 'prop-types';

class Component extends React.Component {
  render() {
    return <div>{this.props.text}</div>;
  }
}

Component.propTypes = {
  text: PropTypes.string.isRequired,
};
```

<br><br>

propTypes로 컴포넌트의 props 타입 검사는 클래스, 함수 컴포넌트 모두 가능하다. <br>

```jsx
// After (15.5)
import React from 'react';
import PropTypes from 'prop-types';

function Component({text}) {
  return <div>{text}</div>;
}

Component.propTypes = {
  text: PropTypes.string.isRequired,
};
```

<br><br>

## Default Props

초기 props 값도 지정이 가능하며 defaultProps를 설정시 초기 값이 정의된다. <br>

```jsx
class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

// props의 초깃값을 정의합니다.
Greeting.defaultProps = {
  name: 'Stranger'
};

// "Hello, Stranger"를 랜더링 합니다.
ReactDOM.render(
  <Greeting />,
  document.getElementById('example')
);
```

<br><br>

## PropTypes

기본적으로 Javascript 타입인 string, number, boolean symbol 등이 지정이 가능하다.  <br>

```jsx
import PropTypes from 'prop-types';

Componenet.propTypes = {
	propString: PropTypes.string,
	propNumber: PropTypes.number,
	propBoolean: PropTypes.bool,
	propSymbol: PropTypes.symbol,
};
```

<br><br>

그리고 객체, 배열, 함수 형태의 타입도 지정이 가능하다. <br>

```jsx
Componenet.propTypes = {
	propObject: PropTypes.object,
	propArray: PropTypes.array,
	propFunction: PropTypes.func,
};
```

<br><br>

 여러 종류 중 하나의 타입이 될 수 있는 경우 oneOfType을 사용하여 정의한다. <br>

```jsx
Component.propTypes = {
	propStringOrNumber: PropTypes.oneOfType([
		PropTypes.string,
		PropTypes.number,
	]),
};
```

<br><br>

특정타입의 배열과 특정타입의 객체의 경우에는 arrayOf, objectOf를 사용하여 정의한다. <br>

```jsx
Component.propTypes = {
	propArrayNumber: PropTypes.arrayOf(PropTypes.number),
	propObjectNumber: PropTypes.objectOf(PropTypes.number),
};
```

<br><br>

특정형태의 객체의 경우 shape으로 정의한다. <br>

```jsx
Component.propTypes = {
	propShape: PropTypes.shape({
		propString: PropTypes.string,
		propNumber: PropTypes.number,
	});
};
```

<br><br>

객체에 대한 properties를 정확하게 검사하기 위해서는 exact를 사용하여 정의하며 이때 객체의 properties가 다른 경우 warning이 발생한다. <br>

```jsx
Component.propTypes = {
	propShape: PropTypes.exact({
		propString: PropTypes.string,
		propNumber: PropTypes.number,
		propBoolean: PropTypes.bool,
		propSymbol: PropTypes.symbol,
	});
};
```

<br><br>

추가 많은 타입 정의들은 공식 홈페이지 [PropTypes](https://ko.reactjs.org/docs/typechecking-with-proptypes.html#proptypes)를 참고하자.

<br><br>

[Ref] :

- [PropTypes와 함께 하는 타입 확인](https://ko.reactjs.org/docs/typechecking-with-proptypes.html)

<br><br><br>