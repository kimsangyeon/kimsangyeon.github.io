---
layout: post
title: 'Controlled Component'
categories: [javascript, react]
image: assets/images/banner/react.png
author: yeon
---

# Controlled Componenet

## Controlled Component란? 제어 컴포넌트

HTML에서 `<input>`, `<textarea>`, `<select>`와 같은 폼 엘리머트는 일반적으로 사용자의 입력을 기반으로 자신의 state를 관리하고 업데이트한다. <br>
React에서는 변경할 수 있는 state가 일반적으로 컴포넌트 state 속성에 유지되며 setState()에 의해 업데이트된다. <br>

<br>

폼을 랜더링하는 React 컴포넌트는 폼에서 발생하는 사용자 입력값을 제어한다. <br>
React에 의해 값이 제어되는 입력 폼 엘리먼트를 `Controlled Component`라고 한다. <br>

<br>

제어 컴포넌트를 사용하여 `<input>`, `<textarea>`, `<select>`의 값을 항상 React state로 관리한다. <br>
다른 UI 엘리먼트에 값을 전달하거나 다른 이벤트 핸들러에서 값을 재설정 할 수 있다. <br>

<br>

다중입력 제어하기로 엘리먼트에 설정된 name 값에 따라 value 값 state를 변경시켜준다. <br>

```jsx
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    // 주어진 input 태그의 name에 일치하는 state를 업데이트하기 위해
    // ES6의 computed property name 구문을 사용하고 있습니다.
    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}

```

<br><br>

## UnControlled Component 비제어 컴포넌트

`UnControlled Component`는 DOM자체에서 폼 데이터가 다루어진다. <br>
모든 state 업데이트에 대한 이벤트 핸들러를 작성하는 대신 `ref`를 사용하여 DOM에서 폼 값을 가져 올 수 있다. <br>

<br>

비제어 컴포넌트는 DOM에 신뢰가능한 출처를 유지하여 DOM의 value 값을 가져와 사용합니다. <br>

`<input type="checkbox">`와 `<input type="radio">`는 **defaultChecked**를 지원하고 `<select>`와 `<textarea>`는 **defaultValue**를 지원합니다.

```jsx
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

render() {
  return (
    <form onSubmit={this.handleSubmit}>
      <label>
        Name:
        <input
          defaultValue="Bob"
          type="text"
          ref={this.input} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}
```

<br><br>

파일 입력 태그의 경우 프로그래밍 적으로 값을 설정 할 수 없고 사용자가 값을 설정할 수 있기 때문에 항상 비제어 컴포넌트이다. <br>

DOM 노드의 ref를 설정하여 파일에 접근하여 핸들링한다. <br>

```jsx
class FileInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.fileInput = React.createRef();  }
  handleSubmit(event) {
    event.preventDefault();
    alert(`Selected file - ${this.fileInput.current.files[0].name}`);
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Upload file:
          <input type="file" ref={this.fileInput} />
        </label>
        <br />
        <button type="submit">Submit</button>
      </form>
    );
  }
}

ReactDOM.render(
  <FileInput />,
  document.getElementById('root')
);
```

<br><br>

[ref]:
- [React Controlled Component](https://ko.reactjs.org/docs/forms.html)
- [React Uncontrolled Component](https://ko.reactjs.org/docs/uncontrolled-components.html)

<br><br><br>