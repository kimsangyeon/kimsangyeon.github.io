---
layout: post
title: "Typescript Class" 
categories: [ Angular, Javascript, typescript ]
image: assets/images/banner/typescript/typescript.png
author: yeon
---

# Typescript Class
Class는 Javascript도 객체지향적으로 프로그램이 가능하게 도와준다.
- 상속
- 다형성
- 캡슐화
- 추상화

<br>

## Class 정의
Javascript ES6에서 class 사용가능
다른 언어 class처럼 관련된 프로퍼티와 메서드로 구성된 논리적 컨테이너라고 한다.
```javascript
class Computer {
  public name: string;
  public price: number;
  public id: number;

  getInformation(): string {
    return `name: ${name}, price ${price}`;
  }
}

let com = new Computer();
com.name = 'super';
com.price = 100;
com.id = 1024;
```

class 객체는 new 키워드를 사용하여 선언하며, . 를 사용하여 public 프로퍼티, 메소드에 접근한다.

<br><br>

## 생성자
constructor를 사용하여 생성자를 정의하며, 필요한 파라미터를 받을 수 있도록 정의한다.
```javascript
class Computer {
  public name: string;
  public price: number;
  public id: number;

  constructor(name: string, price: number, id: number) {
    this.name = name;
    this.price = price;
    this.id = id;
  }

  getInformation(): string {
    return `name: ${name}, price ${price}`;
  }
}

let com = new Computer('super', 100, 1024);
```

짧게 생성자 및 프로퍼티를 생성하기위해 생성자에 public 키워드를 넣어 선언 가능
```javascript
class Computer {
  constructor(public name: string, public price: number, public id: number) {
    this.name = name;
    this.price = price;
    this.id = id;
  }

  getInformation(): string {
    return `name: ${name}, price ${price}`;
  }
}
```

<br><br>

## 정적 프로퍼티
정적 프로퍼티는 static을 사용하여 정의하며 클래스 객체를 통해 참조한다.
```javascript
class Computer {
  static maker: string = "yeon";
}

let maker = Computer.maker;
```

<br><br>

## 추상 클래스 (abstract)
추상 클래스는 정의한 메서드를 구현할 필요가 없는 클래스이다.
```javascript
abstract class Computer {
  constructor(public name: string, public price: number, public id: number) {
    this.name = name;
    this.price = price;
    this.id = id;
  }

  abstract getInformation(): string;
}
```

<br>

하위 클래스를 만들어 추상 메소드에 동작을 정의
```javascript
class typescript extends Computer {
  getInformation(): string {
    return `name: ${name}, price ${price}`;
  }
}
```

<br><br>

## 인터페이스 (interface)
인터페이스는 Javascript에는 없는 개념이며, 프로퍼티와 메서드의 모음으로 정의만 할분 동작정의 구현이 없다.
```javascript
interface Computer {
  name: string;
  price: number;
  id: number;
  select?: string;

  getInformation(): string;
}
```
물음표를 사용하여 선택적 프로퍼티도 정의 가능

<br>

### 덕 타이핑 (duck typing)
명시적으로 해당 타입으로 표시할 필요가 없는 타입
```javascript
interface Icomputer {
  name: string;
  price: number;
  id: number;
  select?: string;

  getInformation(): string;
}

class Computer {
  name: string;
  price: number;
  id: number;

  getInformation(): string {
    return `name: ${name}, price: ${price}`;
  }
}

function setComputer(computer: Icomputer) {}

let ms = new Computer;
setComputer(ms);
```
Interface를 파라미터로 가지는 setComputer 메소드에서 따로 Computer타입을 지정하지 않아도 Computer 타입 객체를 파라미터로 전달 가능.




<br><br><br>