---
layout: post
title: "Iterator Generator"
categories: [ javascript ]
image: assets/images/banner/javascript.png
author: yeon
---

Javascript 

## Iterator
> 반복자

배열이나 그와 유사한 자료구조의 내부의요소를 순회하는 객체, 시퀀스를 정의하고 종료시 잠재적으로 반환값을 정의하는 객체라고 한다. <br>
기본적으로 value, done 값을 반환하는 next() 메소드를 가지며, 값을 나타내는 value와 마지막 값을 확인하는 done이 있다. <br>
done이 true인 경우 done과 함께 value값을 반환한다. <br>

<br>

iterator객체는 생성후에 next()를 반복적으로 호출하며 순회할 수 있다. <br>

<br>

ex)

```javascript
function makeRangeIterator(start = 0, end = Infinity, step = 1) {
    var nextIndex = start;
    var n = 0;
    
    var rangeIterator = {
       next: function() {
           var result;
           if (nextIndex < end) {
               result = { value: nextIndex, done: false }
           } else if (nextIndex == end) {
               result = { value: n, done: true }
           } else {
               result = { done: true };
           nextIndex += step;
           n++;
           return result;
       }
    };
    return rangeIterator;
}
```

<br><br>

## generator
> 생성자

반복자를 생성할때 명시적으로 상태를 유지할 필요가 있다. 생성자는 이에 대한 대안을 제공한다. <br>
생성자는 function* 문법을 사용하여 작성되며 생성자라 불리는 반복자 타입을 반환한다. <br>
생성자 함수는 next()메소드로 값을 소비하며 yield키워드를 만날때까지 실행한다. <br>

<br>

```javascript
function* makeRangeIterator(start = 0, end = Infinity, step = 1) {
    let n = 0;
    for (let i = start; i < end; i += step) {
        n++;
        yield i;
    }
    return n;
}
```

<br>

#### function*
function* 선언 (끝에 별표가 있는 function keyword) 은 generator function 을 정의하는데, 이 함수는 Generator 객체를 반환합니다. <br>

<br>

```javascript
function* gen() { 
  yield 1;
  yield 2;
  yield 3;
}

var g = gen(); // "Generator { }"
```
<br>

#### method

<br>

- Generator.prototype.next(): yield표현을 통해 yield된 값을 반환
- Generator.prototype.return(): 주어진 값을 반환하고 생성기를 종료
- Generator.prototype.throw(): 생성기로 에러를 throw


<br>

<br><br><br>