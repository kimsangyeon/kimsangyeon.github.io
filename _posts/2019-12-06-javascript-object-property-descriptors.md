---
layout: post
title: 'Javascript Object Property Descriptors'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Object Property Descriptors

모든 Object는 단순하게 Key, Value 쌍만 존재하는 것이 아니라 속성을 보거나 지정하는데 도움을 주는 속성 설명자가 있습니다. Property의 Attribute의 집합을 속성 설명자라고 합니다.

<br><br>

Javascript Object의 Property Attribute는 총 6개가 존재합니다.

- [[Value]]
- [[Get]]
- [[Set]]
- [[Writable]]
- [[Enumerable]]
- [[Configurable]]

[[]]이중 괄호로 표시되는 Attribute는 ECMA 내부 속성을 표시하며, 이 속성은 JS 프로그래머가 직접 수정하지 못하는 code 입니다. 이 속성을 수정하기 위해서는 내부적으로 제공되는 메소드를 사용해야합니다.

<br><br>

### Object getOwnPropertyDescriptor

Object의 내부 속성을 조회하기 위한 메소드로 [[[Value]], [[Writable]], [[Enumerable]], [[Configurable]]을 조회가능 합니다.

```javascript
const obj = {
  a: 1,
  b: 2,
};

Object.getOwnPropertyDescriptor(obj, 'a');

/*
{
  value: 1,
  writable: true,
  enumerable: true,
  configurable: true
}
*/
```

- [[Value]]: 속성에 저장된 값 (Any)
- [[Writable]]: 값을 덮어 쓸 수 있는지 여부 (Boolea)
- [[Enumerable]]: 속성이 객체속성 노출(for in 루프)에서 유효한지 (Boolean)
- [[Configurable]]: 속성 값 변경에 대한 옵션?처럼 동작, false 인경우 delete로 지울수 없고 속성 접근자로도 수정 할 수 없음

<br>

### Object definedProperty

지정된 객체의 속성을 정의하거나 수정할 수 있는 Object 정적 메소드 입니다. <br>

<br>

ex) MDN

```
Object.defineProperty(obj, prop, descriptor)
```

<br>

- obj: 속성을 정의할 객체.
- prop: 새로 정의하거나 수정하려는 속성의 이름 또는 Symbol.
- descriptor: 새로 정의하거나 수정하려는 속성을 기술하는 객체.

<br>

```javascript
const object1 = {};

Object.defineProperty(object1, 'property1', {
  value: 42,
  writable: false,
});

object1.property1 = 77;
// throws an error in strict mode

console.log(object1.property1);
// expected output: 42
```

writable이 false로 지정되는 경우 값을 수정할 수 없습니다. <br>

<br>

```javascript
const object1 = {};

Object.defineProperty(object1, 'property1', {
  value: 42,
  configurable: false,
});

delete object1.property1;
// false
```

configurable이 false로 지정되는 경우 값을 제거할 수 없습니다. <br>

<br><br>

ref: [Diving Deeper in JavaScripts Objects](https://blog.bitsrc.io/diving-deeper-in-javascripts-objects-318b1e13dc12)

<br><br><br>
