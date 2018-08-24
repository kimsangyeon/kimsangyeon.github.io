---
layout: post
title: "Typescript Type Anotation" 
categories: [ Javascript, typescript ]
image: assets/images/typescript/typescript.png
author: yeon
---

# Typescript Type Anotation
Typescript에서는 Javascript 변수 또는 함수에 타입을 지정할 수 있도록, 타입 정의 구문을 제공함

## Typescript Type
### Number
Javascript에서와 동일한 Number Type
```javascript
let num: number = 1;
let decimal = 1.0;

```

### String
문자열은 UTF-16 형식의 데이터이다.
Javascript에서는 문자열, 캐릭터형을 '', "" 둘다 사용 가능하다.
```javascript
let firstName: string = 'sangyeon';
let templateHMTL: string = '<div>template HTML</div>';
```

Typescript는 $구문을 사용하여 String을 쉽게 합칠 수 있다.
```javascript
let news: string = "MBC";
let num: number = 5;
let title: string = `TOP $num news feed from $news.`

console.log(title);
```
~~~
"TOP 5 news feed from MBC."
~~~

### Boolean
```javascript
let isBool: boolean = false;
```

### Array
배열은 배열안에 담을 데이터 Type을 지정
```javascript
let counts: number[] = [1, 2, 3, 4, 5];
```

### Tuple
배열이지만 다른 Type의 데이터를 담을 수 있다.
```javascript
let tData: [string, number];
tData = ['yeon', 1];
```

### Any
Javascript를 Typescript로 마이그레이션중에 유용하게 사용
any Type으로 지정된 데이터는 타입검사를 하지 않음
```javascript
let anytype: any;
anytype = 1;
anytype = 'yeon';
anytype = [1, 2, 3]''
```

### Void
리턴값이 없는 등에 상황에 반환타입 void 지정
```javascript
function nothingFn(num: number): void {
	console.log(num);
}
```

### Null, undefined
null과 undefined는 모든 Type의 하위집합이라고 한다.
numm, undefined로 지정하는 경우 any Type이 지정된다.
```javascript
let num = 10;
num = 'yeon';
```

### Union types
Typescript에서 한 Type이 아닌 여러 타입을 지정할 수 있도록 해주는 기능을 제공 파이프 기호를 사용하여 여러 타입을 지정
```javascript
let uniontype = string | number;
uniontype = 'yeon';
uniontype = 1;
```



