---
layout: post
title: 'Javascript Object Protecting'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Object Protecting

Javascript Object의 속성 값을 변경하는 것은 너무 쉽습니다. 이를 방지하기 위한 3가지 Object 속성을 보호하는 방법을 정리합니다. <br>

- preventExtensions
- seal
- freeze

위 세가지는 Object 메소드로 Object 속성을 보호하는데 사용합니다. <br>

<br><br>

## Object.preventExtensions

**Object.preventExtensions**는 새로운 속성이 Object에 추가되는 것을 막아줍니다. (객체에 대한 확장을 방지) <br>

<br>

```javascript
const obj = {
  a: 1,
};

Object.preventExtensions(obj);

obj.b = '2';

console.log(obj);
// => {a: 1}
```

위 코드에서 보듯 b 속성을 추가하려고 시도하지만 obj는 preventExtensions에 의해 확장이 방지되므로 b속성은 추가되지 않습니다. <br>
속성 확장에 대한 여부를 확인할려면 **Object.isExtensible**을 사용하여 Boolean 값으로 확인 가능합니다. true 인 경우 확장 가능<br>

```javascript
const obj = {
  a: 1,
};

console.log(Object.isExtensible(obj));
// => true

Object.preventExtensions(obj);

console.log(Object.isExtensible(obj));
// => false
```

<br><br>

## Object.seal

**Object.seal**은 preventExtensions보다는 조금 더 강하게 Object 속성을 보호 할 수 있도록 도와줍니다. <br>
preventExtensions의 경우 Object의 확장에 대해서만 방지해주기 때문에 delete로 속성 제거는 가능합니다. <br>

```javascript
const obj1 = {
  a: 1,
};

Object.preventExtensions(obj1);

delete obj1.a;

consoe.log(obj1);
// => {}

const obj2 = {
  a: 1,
};

Object.seal(obj2);

delete obj2.a;

console.log(obj2);
// => {a: 1}
```

<br>

seal은 Object의 속성 제거도 방지하여 속성 확장, 제거를 하지 못하도록 보호해줍니다. 대신 속성에 대한 값 변경은 가능합니다. <br>

```javascript
const obj = {
  a: 1,
};

Object.seal(obj);

obj.a = 2;

console.log(obj);
// => {a: 2}
```

<br>

seal에 대한 여부는 **Object.isSealed**를 사용하여 알 수 있습니다. <br>

```javascript
const obj = {
  a: 1,
};

console.log(Object.isSealed(obj));
// => false

Object.seal(obj);

console.log(Object.isSealed(obj));
// => true
```

<br><br>

## Object.freeze

**Object.freeze**는 Object를 가장 강력하게 보호해 줍니다. Object의 속성 수정, 확장, 제거 모두 보호해주기 때문에 Object를 읽기 전용으로만 사용이 가능하도록 보호합니다. <br>
Object.freeze는 Object.seal을 내부적으로 사용하여 Object 보호를 1차적으로 한 후 수정에 대한 보호가 추가된 형태라고 합니다. <br>
Object freeze 여부는 **Object.isFrozen**으로 가능합니다.

```javascript
const obj = {
  a: 1,
};

console.log(Object.isExtensible(obj));
// => false
console.log(Object.isSealed(obj));
// => false
console.log(Object.isFrozen(obj));
// => false

Object.freeze(obj);

delete obj.a;
// not work

obj.a = 2;
// not work

obj.b = 2;
// not work

console.log(Object.isExtensible(obj));
// => false
console.log(Object.isSealed(obj));
// => true
console.log(Object.isFrozen(obj));
// => true
```

<br><br>

ref: [Diving Deeper in JavaScripts Objects](https://blog.bitsrc.io/diving-deeper-in-javascripts-objects-318b1e13dc12)

<br><br><br>
