---
layout: post
title: "Typescript Function" 
categories: [ Angular, Javascript, typescript ]
image: assets/images/banner/typescript/typescript.png
author: yeon
---

# Typescript Function
Typescript 함수는 Javascript 함수와 크게 다르지는 않으며, 파라미터목록, 반환값에 대한 타입 선언 정도가 크게 다른점인 것 같다.

<br><br>

## 함수 타입
```javascript
function getName(firstName: string, lastName: string): string {
  return firstName + " " + lastName;
}
```
firstName, lastName 문자열 파라미터와 리턴값 string 정의

<br><br>

## 화살표 함수 (arrow function)

<br>

```javascript
getName (firstName: string, lastName: string) => {
  return firstName + " " + lastName;
}
```
=> 기호를 사용하여 함수를 간단히 선언 가능.

<br>

```javascript
// 중괄호 생략
getName (firstName: string, lastName: string) => firstName + " " + lastName;

// 파라미터 하나일 경우 () 생략 가능
firstName => return firstName;
```

<br><br>

### 파라미터

<br><br>

#### 선택적 Optional
Javascript에서는 파라미터를 여러개 지정후 필요한 파라미터만 넘겨서 동작이 가능하다.
```javascript
function getName (firstName, lastName) {
  if (firstName && lastName) {
    return firstName + " " + lastName;
    } else {
      return firstName;
    }
}

getName("kim", "sangyeon");
getName("kim");
```

Typescript에서는 이러한 선택적으로 넘길수 있는 파라미터를 ?를 앞에 붙여 표시한다.
```javascript
function getName (firstName: string, ?lastName:string): string {
  if (firstName && lastName) {
    return firstName + " " + lastName;
    } else {
      return firstName;
    }
}

getName("kim", "sangyeon");
getName("kim");
```

<br>

#### 기본 Default
파라미터의 기본 값을 설정가능
```javascript
function printTitle(title: string, author: string="kim") {}
```
기본값이 지정된 파라미터가 마지막에 올경우 선택적 파라미터로 간주.

<br><br>

#### 나머지 파라미터
...(점 3개) 생략부호를 사용하여 나머지 파라미터 정의
```javascript
function Score(name: string, ...score: number[]) {}

let s = new Score("kim", 1, 2, 3, 4);
```

<br><br>

## 함수 오버로딩
이름이 같은 함수를 다른 구현방식으로 정의
```javascript
function getProperty(title: string): string;
function getProperty(id: number): string;
function getProperty(score: number): string;
function getProperty(property: any): string {
    if (typeof === 'string') {

    } else if (typeof === 'number') {

    }

    return 'property';
}
```





<br><br><br>