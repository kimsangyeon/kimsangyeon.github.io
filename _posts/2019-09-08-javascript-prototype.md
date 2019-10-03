---
layout: post
title: "Javascript Prototype"
categories: [ javascript ]
image: assets/images/banner/javascript.png
author: yeon
---

# Prototype

- MDN -
ES2015부터 class 키워드를 지원하기 시작했으나, 문법적인 양념일 뿐이며 자바스크립트는 여전히 프로토타입 기반의 언어다.
상속 관점에서 자바스크립트의 유일한 생성자는 객체뿐이다. 각각의 객체는 [[Prototype]]이라는 은닉(private) 속성을 가지는데 자신의 프로토타입이 되는 다른 객체를 가리킨다. 그 객체의 프로토타입 또한 프로토타입을 가지고 있고 이것이 반복되다, 결국 null을 프로토타입으로 가지는 오브젝트에서 끝난다. null은 더 이상의 프로토타입이 없다고 정의되며, 프로토타입 체인의 종점 역할을 한다. <br>

<br><br>

Javascript는 Prototype을 사용하여 객체를 생성해내는 Prototype 기반 언어입니다.
Javascript에서는 Prototype을 이용하여 객체지향적인 프로그래밍을 할 수 있도록 도와줍니다. <br>

<br>

Prototype은 두가지로 해석되며, 객체를 참조하는 prototype 속성과 객체의 속성을 참조하는 proto 속성이 있습니다.
Javascript에서 함수를 정의하게되면 함수는 Prototype 객체를 참조하게 됩니다. <br>

```javascript
function Phone() {}

Phone.ptototype // {constructor: f}
Phone.ptototype.constructor // f Person() {}
```

<br>

Phone이라는 함수는 Prototype 객체를 참조하게 되고 Prototype 객체 멤버인 constructor 속성이 Phone 함수를 참조하게 됩니다.
여기서 하나 더 나아가 Prototype 객체의 proto는 모든 객체의 원형이 되는 Object 입니다. <br>

```javascript
Phone.prototype.__proto__ // {constructor: f, __defineGetter__: f ....
Phone.prototype.__proto__.constructor // f Object() { [native code] }
```

<br><br>

모든 객체는 Prototype 객체에 접근 할 수 있으며 동적으로 메소드와 인스턴스를 추가할 수 있습니다.

```javascript
const myPhone = new Phone();
myPhone.number = '010';

Phone.prototype.getNumber = function() {
	return number;
};

console.log(myPhone,getNumber()); // '010'
```

<br><br>

함수의 멤버로 존재하는 prototype 속성은 prototype 객체를 참조하는 멤버이며, __proto__ 속성은 객체의 원형이되는 prototype 객체를 참조하는 숨겨진 링크입니다. <br>

위와같이 prototype으로 메소드를 선언시 해당 함수를 사용하여 생성된 객체는 해당 메소드를 사용할 수 있습니다. <br>

```javascript
Phone.prototype.getNumber = function() {
   return number;
}

const phone1 = new Phone();
const phone2 = new Phone();

phone1.number = '010';
phone2.number = '020';

console.log(phone1.getNumber()); // '010';
console.log(phone2.getNumber()); // '020';
```

<br>

유의점은 prototype 객체에 메소드를 추가하여야 함수로 생성된 객체들이 같은 메소드를 사용할 수 있게됩니다. 즉 공통으로 참조하는 멤버가 됩니다. 함수로 생성된 객체에 메소드를 선언 할 경우 해당 객체에서만 사용이 가능합니다. <br>

```javascript
const phone1 = new Phone();
const phone2 = new Phone();

phone2.getName = function() {
   return 'super';
};

console.log(phone1.getName()); // Uncaught TypeError: phone1.getName is not a function;
console.log(phone2.getName()); // 'super';
```

<br>

위와같은 형태는 class에서 사용하는 상속 받아 오버라이딩 하는 형태와 비슷하다고 할 수 있겠습니다.

<br><br>

## 상속

코드를 재사용하는 방법, 재활용은 Java 등에서 class 상속을 통해 중복되는 코드를 상속받아 재사용할 수 있습니다.
Javascript에서는 Prototype을 사용하여 코드를 재사용하는 방법이 있습니다. <br>

<br>

Prototype으로 코드 재사용하는 방법은 두가지로 분류되며 **classical** 방식과 **prototypal** 방식이 있습니다. <br>

<br><br>

### Classical
classical 방식으로는 여러 방법이 있지만 Prototype 객체를 참조하는 방법만 정리하겠습니다.
생성한 자식함수의 Prototype 속성을 부모함수의 Prototype 속성을 참조하는 방식으로 객체를 생성시 부모함수의 Prototype에 지정한 멤버를 사용할 수 있습니다. <br>

<br>

```javascript
function Phone(number) {
   this.number = number;
}

Phone.prototype.getNumber = function() {
   return this.number;
}

function Iphone(number) {
   this.number = number;
}

Iphone.prototype = Phone.prototype;

let myPhone = new Iphone("010");
console.log(myPhone.getNumber()); // "010"
```

하지만 이 방법은 자식함수가 부모함수의 Prototype을 참조하는 것이기 때문에 자식함수의 Prototype에 멤버를 추가하는것은 부모함수 Prototype 멤버가 추가되는 것이기 때문에 유의가 필요합니다.
해서 자식함수에 멤버 추가시 자식함수의 this에 멤버를 추가하여 사용하여야 합니다. <br>

<br>

```javascript
function Phone(number) {
   this.number = number;
   this.getName = function() {
      console.log("Phone");
   };
}

Phone.prototype.getNumber = function() {
   return this.number;
}

function Iphone(number) {
   this.number = number;
   this.getName = function() {
      console.log("IPhone");
   };
}

Iphone.prototype = Phone.prototype;

let myPhone = new Iphone("010");
console.log(myPhone.getNumber()); // "010"
console.log(myPhone.getName()); // "Iphone"
```

<br><br>

### Prototypal
Prototypal 방식은 간단하게 Object.create()를 사용하며 새로운 객체 생성시 첫번째 인자로 Prototype을 참조할 부모 객체를 넣어주면 됩니다. <br>

<br>

```javascript
function Phone(number) {
   this.number = number;
}

Phone.prototype.getNumber = function() {
   return this.number;
}

let myPhone = Object.create(Phone.prototype);
myPhone.number = "010";
console.log(myPhone.getNumber()); // "010"
```

<br>

위 방식으로 myPhone 생성시 myPhone은 Phone의 prototype을 참조하여 멤버 사용이 가능합니다. <br>

<br>

MDN: [Object.create](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

<br><br><br> 