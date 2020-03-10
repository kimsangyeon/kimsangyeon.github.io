---
layout: post
title: 'Javascript Optional Chaining'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Optional Chaining

존재하지 않는 값에 대해 접근할 경우 발생하는 에러 <br> `Uncaught ReferenceError: obj is not defined` <br>
한번쯤?은 Javascript 코드를 짜며 본적이 있을 것입니다. 존재하지 않는 객체, 참조에 대해 값을 요구하는 경우 발생합니다. 이를 방지하기 위해 객체가 존재하는지에 대한 예외처리는 필수적으로 이루어져야 합니다. 값에 대한 `null || undefine` 체크를 위해 if 혹은 lodash의 isNil과 값은 검사 구문들이 들어갑니다. 값에 대한 검사는 필수이지만 이러한 코드가 많아질 수록 코드 가독성은 떨어집니다. 이를 위해 Javascript `Optional Chaining` 문법이 나왔습니다. 이는 2019.12.12 stage 3 Draft 되어 추후 표준으로 들어갈 것으로 생각됩니다. <br><br>

현재 `Optional Chaining`은 `@babel/plugin-proposal-optional-chaining`을 추가하여 사용이 가능합니다. <br>

<br>

The optional chaining operator ?. permits reading the value of a property located deep within a chain of connected objects without having to expressly validate that each reference in the chain is valid. The ?. operator functions similarly to the . chaining operator, except that instead of causing an error if a reference is nullish (null or undefined), the expression short-circuits with a return value of undefined. When used with function calls, it returns undefined if the given function does not exist. [[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)] <br>

<br><br>

## Optional Chaining

문법은 삼항연산자와 언뜻 비슷하면서도 조금 더 간결해졌습니다. <br>

# Syntax

```javascript
obj?.prop;
obj?.[expr];
arr?.[index];
func?.(args);
```

위와 같이 ? 를 사용하여 프로퍼티 존재 유무를 체크 하는 형태로 코드 작성이 가능해집니다. 값이 없는 경우 undefined가 반환되고 함수인 경우 undefined, null이 아닌경우 실행 시킵니다. <br>
위 예제를 삼항연산자로 구현할 경우

```javascript
!!obj ? obj.prop : undefined;
!!obj ? obj[expr] : undefined;
!!arr ? arr[index] : undefined;
!!func ? func(args) : undefined;
```

조금 더 정확한 검사를 위해서는 typeof 혹은 hasOwnProperty를 활용하여 검사도 가능합니다. <br>

```javascript
typeof obj === 'object' ? obj.hasOwnProperty('prop') ? obj.prop : undefined;

typeof obj === 'object' ? obj.hasOwnProperty('expr') ? obj[expr] : undefined;

typeof arr === 'object' ? arr[index] : undefined;
Array.isArray(arr) ? arr[index] : undefined;

typeof func === 'function' ? func(args) : undefined;
```

<br>

조금씩 조건이 추가되는 것이지만 `Optional Chaining`의 경우가 조금 더 가독성이 좋다는 것을 느낄 수 있습니다. `Optional Chaining`의 경우도 깊이가 깊어지는 경우 ? 연산이 많아 지기는 하지만 삼항연산자에 비해서는 짧고 간결하게 작성이 가능합니다.

<br>

```javascript
const obj = {
  prop: {
    hello: {
      world: {
        fn: function() {
          console.log('hello world!');
        }
      }
    }
  }
};

obj?.prop?.hello?.word?.fn?.fn(); // => hello world!
obj ? obj.prop ? obj.prop.hello ? obj.prop.hello.world ? obj.prop.hello.world.fn ? obj.prop.hello.world.fn() : undefined;
```

위 코드를 봐도 삼항연산자보다는 `Optional Chaining`이 훨씬 간결하게 코드 작성이 가능한 것을 볼 수 있습니다.

<br><br><br>
