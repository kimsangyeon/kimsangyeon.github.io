---
layout: post
title: 'Private Properties in Javascript'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Private Properties in Javascript

Javascript에서 숨기고 싶은 `Private Properties`를 가지고 싶을 때가 있습니다. Javascript에서 Private 한 Member를 가지는 방법을 몇가지 정리해 봅니다. <br>

<br><br><br>

## Unprotected Senario

아래는 Properties가 보호되지 못하는 경우를 살펴 보도록 구성된 코드입니다. 생성된 객체의 Member에 쉽게 접근하여 제거가 가능한 것을 보실 수 있습니다.

```javscript
const Person = (function () {
  function Person(name) {
    this.name = name;
  }

  Person.prototype.getName = function () {
    return this.name;
  };

  return Person;
}());

const p = new Person('Yeon');
console.log(p.getName()); // Yeon

delete p.name;

console.log(p.getName()); // undefined

```

다음과 같이 생성된 객체의 Member가 손쉽게 지워진다면 코드상에서 존재하지 않는 Member에 접근하게 되는 경우가 생길 수 있고 오류를 유발 할 수도 있을 것입니다.<br>

<br><br>

## Naming Convention

숨긴다고 하기엔 부족하지만 개발자들끼리 약속하여 Private 한 Memeber로 사용하고 싶은 이름 앞에 ' _ '를 붙여 외부에서 사용하는 것을 약속하는 형태가 있습니다. 해당 방법은 간단하지만 약속이 잘 지켜지는지... 그리고 외부에서 손쉽게 Member에 접근이 가능하기 때문에 조금은 허술한 방법이라 추천드리지 않습니다. <br>

<br><br>

## Using Closure

`Closure`를 이용하여 Member를 감추어 외부에서 접근 할 수 없도록 하는 방법입니다. 내부 `Closure`에 포함된 Member는 Private하게 사용하기는 좋지만 `Closure`를 사용할 경우 객체 생성시마다 해당 인스턴스를 위한 `Closure`를 생성해야 하므로 메모리 누수 등의 문제점이 있어 사용시 유의가 필요합니다.

```javascript
const Person = (function() {
  function Person(name) {
    this.getName = function() {
      return name;
    };
  }
  
  return Person;
}());

const p = new Person('Yeon');
console.log(p.getName()); // Yeon

delete p.name;

console.log(p.getName()); // Yeon
```

<br><br>

## Using Symbol

다음 방법은 ES6 `Symbol`을 사용하여 Member를 Private하게 숨길 수 있습니다. `Symbol`을 객체의 키 값으로 사용하여 Member를 맵핑 할 경우 해당 `Symbol`을 통해서만 Member에 접근이 가능하도록 하는 방법입니다. <br>

```javascript
const Person = (function() {
  const nameSymbol = Symbol();
  function Person(name) {
    this[nameSymbol] = name;
  }

  Person.prototype.getName = function() {
    return this[nameSymbol];
  }

  return Person;
}());

const p = new Person('Yeon');
console.log(p.getName()); // Yeon

delete p.name;

console.log(p.getName()); // Yeon
```

위의 방법으로 `Symbol`을 이용한 Member 접근으로 Private하게 Member를 만들수 있었습니다. 하지만 해당 방법은 `Symbol`이 노출될 경우 Member에게 접근 할 수 있습니다. `Object.getOwnPropertySymbols`를 사용하는 경우 객체의 Symbol을 가져와 Symbol로 맵핑된 Member에 접근할 수 있게 됩니다.

```javascript
const Person = (function() {
  const nameSymbol = Symbol();
  function Person(name) {
    this[nameSymbol] = name;
  }

  Person.prototype.getName = function() {
    return this[nameSymbol];
  }

  return Person;
}());

const p = new Person('Yeon');
console.log(p.getName()); // Yeon

const pSymbol = Object.getOwnPropertySymbols(p)[0];

delete p[pSymbol];

console.log(p.getName()); // undefined
```

이렇게 `Symbol`을 알 수 있다면 Member에 접근 할 수 있게 되버리므로 완벽한 Private 한 Member로는 보장 받지 못합니다. <br>

<br><br>

## Using WeakMap

마지막으로 가장 강력하게 Private 한 Member를 만들 수 있는 방법은 `WeakMap`을 사용하는 방법이 있습니다.

```javascript
const Person = (function() {
  const private = new WeakMap();
  function Person(name) {
    const privateProperties = {
      name: name
    };
    private.set(this, privateProperties);
  }

  Person.prototype.getName = function() {
    return private.get(this).name;
  };

  return Person;
}());

const p = new Person('Yeon');
console.log(p.getName()); // Yeon

delete p.name;

console.log(p.getName()); // Yeon
```

<br>

추가로 `WeakMap`을 사용할 경우 얻을 수 있는 이점으로는 <br>
Javascript에서 Map -> Key Value 형태의 Object에서의 구성인 경우 Key로 사용되던 Object가 메모리에서 사라질 경우 값에 대한 Key의 역할이 불필요해집니다. 그래서 Key에 해당하는 내용을 제거해주는 작업이 필요합니다. 하지만 `WeakMap`을 사용할 경우 메모리에서 사라진 Key에 대한 삭제가 자동으로 이루어집니다.

<br>

<br><br><br>
