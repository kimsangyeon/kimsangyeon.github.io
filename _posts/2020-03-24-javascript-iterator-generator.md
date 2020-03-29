---
layout: post
title: 'Javascript Iterator Generator'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Iterator Generator

Javascript에서는 for 루프, map() filter() 등 컬렉션을 반복할 수 있는 많은 방법들을 제공합니다. 여기서 `반복기(iterator)` 및 `생성기(generator)`는 반복 개념을 핵심 언어 내로 바로 가져와 for...of 루프의 동작(behavior)을 사용자 정의하는 메커니즘을 제공합니다. [참고 MDN]

<br><br>

## Iterator

Javascript에서 `Iterator`(반복자)는 두개의 속성 **value**, **done**을 반환하는 **next()** 메소드를 사용하여 Iterator Protocol 혹은 Iterator 패턴을 구현합니다. `Iterator` 시퀀스의 마지막 값이 반환 되었다면 **done** 값은 true가 됩니다. <br>
`Iterator`를 생성하면 **next()** 메소드를 호출하여 명시적 반복동작을 할 수 있으며, **next()**를 통한 반복은 일반적으로 한번씩 반복할 수 있기 때문에 반복자를 소모시킨다고 할 수 있습니다. 마지막 값이 호출된 이후에는 앞서 설명하였듯 **{done: true}** 가 반환됩니다. <br>

<br>

Javascript에서 가장 일반적인 `Iterator`는 배열이지만 모든 `Iterator`가 배열로 표현될 수는 없습니다. 이는 배열은 완전히 할당되어야 하지만 `Iterator`는 필요한 만큼 소모되며, 무제한 시퀀으로 표현될 수 있기 때문입니다. [ ex) 0 ~ Infinity ] <br>

<br><br>

### Iterator Example

다음 예제는 start에서 end까지 step만큼 증가하는 반복시퀀스를 가진 반복자를 만드는 예제입니다.

```javascript
function makeRangeIterator(start = 0, end = Infinity, step = 1) {
  let prevIndex;
  let nextIndex = start;

  const rangeIterator = {
    next: function() {
      let result;

      if (nextIndex > end) {
        return { done: true };
      }

      result = { value: nextIndex, done: nextIndex === end };
      prevIndex = nextIndex;
      nextIndex += step;

      return result;
    },
  };

  return rangeIterator;
}
```

<br>

`Iterator`를 사용하는 예로

```javascript
const it = makeRangeIterator(1, 4);

let result = it.next();
while (!result.done) {
  console.log(result.value); // 1 2 3
  result = it.next();
}

console.log('Iterated over sequence of size: ', result.value);
```

<br><br>

## Generator

`Iterator`는 유용하게 만들어 사용할 수 있지만 생성할때 유의가 필요합니다. `Iterator` 내부에 사용되는 상태를 유지하고 관리하는 로직을 고려하여야합니다. `Generator`는 이러한 상태 관리에 도움을 주는 `iterative algorithm`을 정의 할 수 있도록 도와줍니다. <br>

<br>

`Generator`는 **function\***문법을 사용하여 작성됩니다. 그리고 `Generator` 함수가 최초로 호출될때 함수 내부의 코드는 실행되지 않고 생성자라고 불리는 생성자 타입을 반환합니다. <br>

<br>

### Generator Example

`Generator` 실행으로 반환된 생성자의 **next()** 메소드를 호출하면 생성자 함수는 **yield** 키워드를 만날때까지 실행됩니다.

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

위에서 작성하였던 `Iterator` 코드와 해당 예제는 동일하지만 `Generator`를 사용하는 것이 조금 더 간결하고 가독성이 좋은 것을 보실 수 있습니다.

<br><br>

![generator]({{ site.baseurl }}/assets/images/generator.png)

<br>

위에서 보듯 `Generator`실행 후 반환된 iter는 `Generator` prototype을 가집니다. 그리고 해당 prototype은 **f [Symbol(Symbol.iterator)]()** function을 가진 prototype을 보실 수 있습니다.

<br><br><br>
