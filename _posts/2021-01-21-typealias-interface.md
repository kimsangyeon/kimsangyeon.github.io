---
layout: post
title: 'type alias & interface'
categories: [javascript, typescript]
image: assets/images/banner/typescript/typescript.png
author: yeon
---

# type alias 

타입 별칭이라고도 하며 인터페이스와 비슷하게 보이기도 하다. 작성해야 하는 타입을 `type` 으로 지정하여 다른 이름으로 지정할 수 있다. 만들어진 타입 별칭은 실제로 타입을 만드는 것이 아닌 참조 값으로 사용하는 것이다.

두개 이상의 타입으로 타입이 겹쳐질 수 있는 상황에 사용하는 표현을 유니온 타입이라고 한다. `|` 구문을 사용하여 표기하며 두개 이상의 타입 표현이 가능하다.

<br><br>

### Union Type

```tsx
let person: string | number;

person = 'man';
person = 1;
```

<br><br>

### Tuple

튜플은 Javascript에는 없는 집합으로 불변한 순서가 있는 객체의 집합이다. Typescript에서는 배열에 지정된 타입에 따른 튜플 타입이 적용된다. <br>

```tsx
let pserson: [string, number] = ['yeon', 1];
```

<br><br>

### Type Alias

타입 별칭으로 위에서 선언했던 유니온 타입과 튜플을 지정해보자. <br>

```tsx
// Union
type StringOrNumber = string | number;

let person: StringOrNumber;

person = 'man';
person = 1;

// Tuple
type PersonTuple = [string, number];

let person: PersonTuple = ['yeon', 1];
```

<br><br>

### type assertions

타입을 지정해주는 것으로는 `type alias` 말고도 `type assertions`도 있다. 이는 컴파일러에게 타입을 알려주는 역할을 한다. (타입을 실제로 형변환 해주는 것이 아니다) <br>

사용시 지정하는 타입은 명시적으로 타입을 지정해주는 값이기 때문에 명확해야한다. <br>

변수 as 강제할 타입 <br>

\<강제할타입\> 변수 <br>

<br>

```tsx
let someValue: any = "this is string";

let strLength: number = (<string>someValue).length;
let strLength: number = (someValue as string).length;
```

<br><br>

# interface

타입스크립트 `interface`로 여러가지 타입을 가지는 프로퍼티로 이루어진 새로운 타입을 정의 할 수 있다. <br>

<br>

인터페이스로 선언된 프로퍼티나 메소드는 구현을 강제화하여 일관성을 유지할 수 있도록 해준다. ES6 Javascript에서는 `interface` 를 지원하지 않지만 Typescript에서 지원한다. <br>

<br>

`interface` 는 프로퍼티와 메소드를 가지지만 인스턴스화 할 수 없다는 점에서 `class` 와 다르고 메소드는 모두 추상메소드이다. `abstract class` 와 다른점은 `abstract` 키워드를 사용하지 않는다는 점이다. <br>

<br>

`interface` 는 변수의 타입으로도 사양이 가능하며 변수는 해당 타입에 맞게 값을 가져야한다. <br>

```tsx
interface Todo {
	id: number;
	content: string;
	completed: boolean;
}

let todo: Todo;

todo = { id: 1, content: 'typescript', completed; false};
```

<br><br>

`interface` 를 사용하여 파라미터 타입 선언도 가능하며 함수에 객체를 전달할 때 복잡한 매개변수 체크가 줄어든다. <br>

```tsx
interface Todo {
	id: number;
	content: string;
	completed: boolean;
}

let todos: Todo[] = [];

function setTodo(todo: Todo) {
	todos = [...todos, todo];
}

const newTodo: Todo = { id: 1, content: 'typescript', completed: true};
addTodo(newTodo);
```

<br><br>

### implements

`interface` 를 구현하기 위해 클래스에 `implements` 를 사용하여 구현한다. `interface` 에 명시된 프로퍼티 메소드 구현을 강제화한다. <br>

```tsx
interface Animal {
	name: string;
	getName(): string;
}

class Dog implements Animal {
	name: string = 'puppy';
	getName(): {
		return this.name;
	}
}
```

<br><br>

위와 같은 형태로 `implements` 의 사용은 `type alisas` 형태로도 선언이 가능하다. <br>

```tsx
type Car = {
  type: string;
}

class SuperCar implements Car {
  type: string = 'Super';
}
```

<br><br>

상속구조에서 `interface` 가 클래스의 타입의 확장이라면 클래스를 상속받아 선언한다. 클래스의 `private` 와 `proteced`  멤버도 모두 상속 받으며 클래스의 확장으로 생성 할 수 있다. <br>

```tsx
class Car {
	private type: string;
}

interface SuperCar extends Car {
	run(): void;
}
```

<br><br>

`interface` 에 대한 확장도 `type alias` 로도 가능하다. <br>

```tsx
type Car = {
  type: string;
}

interface SuperCar extends Car {
	run(): void;
}
```

<br>

위와같은 사용법 외에 제네릭 등 여러가지 방법으로 `interface` 와 `type alias` 사용이 가능하다. <br>

둘의 차이점으로는 `interface` 는 선언 병합이 가능하지만 `type alias` 는 병합되지 않는다. <br>

예로 외부 라이브러리 등을 사용하였을때 동일한 이름의 `interface` 이 존재하는 경우 컴파일 시점에 합치는 것을 선언 병합이라고 한다. <br>

<br><br>

- interface

```tsx
interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}

const bear = getBear() 
bear.name
bear.honey
```

<br><br>

- type alias

```tsx
type Animal = {
  name: string
}

type Bear = Animal & { 
  honey: Boolean 
}

const bear = getBear();
bear.name;
bear.honey;

type Window = {
  title: string
}

type Window = {
  ts: import("typescript")
}

// Error: Duplicate identifier 'Window'.
```

<br>

Typescript 팀에서도 확장성이 열려있는 `interface` 사용을 권장하고 `type alias` 는 `Union Type` 이나 `Tuple` 과 같은곳에 적절히 사용하는 것을 권장한다고 합니다. <br>

<br><br>

[Ref]:

- [typescript handbook interface vs type alias](https://www.typescriptlang.org/docs/handbook/advanced-types.html#interfaces-vs-type-aliases)
- [poiemaweb typescript: interface](https://poiemaweb.com/typescript-interface)
- [typescript kr : interface](https://typescript-kr.github.io/pages/interfaces.html)


<br><br><br>