---
layout: post
title: "Javascript Object Accessor Properties"
categories: [ javascript ]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Object Accessor Properties

- MDN -
속성 접근자는 점 또는 괄호 표기법으로 객체의 속성에 접근할 수 있도록 해줍니다. <br>
객체는 속성의 이름을 키로 사용하는 연관 배열(다른 이름으로는 맵, 딕셔너리, 해시, 룩업 테이블)로 생각할 수 있습니다. 보통 객체의 속성을 메서드와 구별해서 말하곤 하지만, 서로의 차이는 관례에 불과합니다. 메서드는 호출할 수 있는 속성일 뿐으로, 속성의 값이 Function을 가리키는 참조라면 그 속성을 메서드라고 합니다.

<br><br>

## Accessor Properties
Javascript 속성 접근 자는 getter, setter로 지정하여 사용되는 것이 일반적이라고 할 수 있을 것 같습니다. Javascript에서도 두 함수 get, set function을 활용하여 속성 지정자를 설정 할 수 있습니다.

<br>

Object에서 Key, Value를 활용한 방식과 비교
```javascript
const obj = {
  key: 'key'
};

obj.key;
// => 'key'
```

Object 내부에 지정된 메소드에 get 지정
```javascript
const obj = {
  get key() {
    return 'key';
  }
};

obj.key;
// => 'key'
```
여기서 유의점은 속성 접근자를 사용한 메소드에는 괄호를 지정할 필요가 없습니다. **obj.key() // X** <br>
또한 setter가 지정되지 않았기 때문에 **obj.key = 'new Key'; // X** 와 같이 값을 변경하는 것도 이루어지지 않습니다.
속성 지정자로 사용된 속성을 'private' 속성으로 _key와 같이 지정후 getter, setter를 지정하여 사용합니다.

<br>

Object 내부 'private' 속성 지정
```javascript
const obj = {
  _key: 'key',
  get key() {
    return _key;
  },
  set key(key) {
    this._key = key;
  }
};
```

<br>

속성 지정자를 활용하여 값 설정 및 원하는 값으로 손쉽게 변경하여 가져오도록 활동 가능

```javascript
const binary = {
  _value: 0,
  get value() {
    return this._value.toString(2);
  },
  set value(value) {
    this._value = value;
  }
};

binary.value = 5;
binary.value;
// => 101
```
10진수 수를 받아 이진수로 변경하여 가져오는 Object

<br><br>

Javascript info: [Object Accessor Properties](https://javascript.info/property-accessors) <br>
ref: [Diving Deeper in JavaScripts Objects](https://blog.bitsrc.io/diving-deeper-in-javascripts-objects-318b1e13dc12)

<br><br><br> 