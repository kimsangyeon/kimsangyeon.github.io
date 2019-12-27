---
layout: post
title: 'Javascript Shallow Copy & Deep Copy'
categories: [javascript]
image: assets/images/banner/javascript.png
author: yeon
---

# Javascript Shallow Copy & Deep Copy

Javascript 코딩중 깊은 복사를 하지 않아 의도치 않은 객체 속성 변경을 겪은적이 있을 것입니다. 흔히 얕은 복사라고 하는 Shallow Copy와 깊은 복사 Deep Copy에 대해 정리해봅니다. <br>

<br>

## 얕은 복사 (Shallow Copy)

흔히 얕은 복사는 값을 복사하는 경우에 많이 사용되고 객체의 경우 한 depth의 깊이만 존재하는 경우 사용됩니다.

```javascript
  let a = 1;
  let b = a;

  a = 2;

  console.log(b);
  // => 1
```
b는 a의 **값**을 복사 하는 얕은 복사로 a값이 변경 되어도 b는 a의 이전 값을 복사한 값을 유지합니다. <br>

<br>

```javascript
   let a = {i: 1};
   let b = Object.assign({}, a);

   a.i = 2;
   
   console.log(b.i);
   // => 1
```
**Object assign**을 활용한 객체 얕은 복사이며 a의 한 depth인 i의 값을 b Object로 얕은 복사하는 예시입니다. i에 대한 값을 복사하여 a.i 값을 변경하여도 b.i의 값은 변경되지 않습니다. <br>

<br>

만약 depth가 두단계인 객체를 복사하는 경우 어떻게 될까요? <br>

<br>

```javascript
  let a = {
    i: 1,
    j: {
      k: 2
    }
  };
  let b = Object.assign({}, a);

  a.j.k = 3;
  
  console.log(b.j.k);
  // => 3
```

Object assign은 얕은 복사이기 때문에 두단계 depth인 a.j.k의 값을 변경시 b.j.k 값도 변경된 것을 볼 수 있습니다. 엄밀히 말하면 b.j.k 값도 변경된 것이 아니라 a.j 값을 b.j가 같은 reference를 참조하고 있기 때문이라고 할 수 있습니다. 이러한 현상은 Javascript 코딩중 발생 할 수 있으며, 객체를 복제하여 사용할때 원치않게 객체 안의 속성 값이 변경되는 문제를 발생시킬 수 있습니다. 이를 방지하기위해 객체 복제는 깊은 복사(deep copy)를 하여 사용합니다. <br>

<br><br>

## 깊은 복사 (Deep Copy)

깊은 복사는 reference 참조가 되지 않도록 모든 값을 depth에 상관없이 모두 복제하여야 합니다. 이는 객체가 클수록 큰 리소스를 사용할 수 있어 상황에 맞게 적절하게 잘 사용하야야 합니다. <br>

<br>

깊은 복사를 하는 방법은 여러 방법이 있으며 세가지 정도를 정리해봅니다.

1. JSON을 사용하여 복사
2. loop recursive를 활용한 복사
3. library를 사용

<br><br>

### JSON을 사용하여 복사

JSON을 사용하면 손쉽게 복사가 가능합니다.

```javascript
  let a = {
    i: 1,
    ...
  };

  let b = JSON.parse(JSON.stringify(a));
```

**JSON.parse**와 **JSON.stringify**를 사용하여 손쉽게 깊은 복사가 가능합니다. 하지만 이 방법은 객체안 속성중 function인 경우 정상적으로 복사가 되지 않습니다.

<br>

```javascript
  let a = {
    b:{
      c: function() {console.log("c");}
    }
  };

  let d = JSON.parse(JSON.stringify(a));
  
  console.log(d.b.c);
  // => undefined
```

<br>

위와 같이 JSON.stringify의 경우 function을 undefined로 처리하기 때문에 사용에 유의하여야합니다. <br>

<br>

### loop recursive를 활용한 복사

객체를 루프를 활용한 재귀로 깊은 복사가 가능합니다.

```javascript
let copyObject = (obj) => {
  if (obj === null || obj === undefined || typeof(obj) !== 'object') {
    return obj;
  }

  let copyObj = {};
  for (key in obj) {
    copyObj[key] = copyObject(obj[key]);
  }

  return copyObj
};
```

위의 형태로 복사시 object type이 아닌경우의 값으로 모두 복제가 이루어져 깊은 복사가 이루어집니다. 루프, 재귀를 통한 복사이기 떄문에 객체가 클수록 리소스를 많이 사용합니다. <br>

<br>

### library를 사용

library를 사용하여 깊은 복사를 하는 것이 가장 쉽고, 어느정도의 안정성을 보장 받을 수 있어 개인적으로는 library를 통한 깊은 복사가 좋지 않을까 생각합니다. <br>
[jQuery $.extend](https://api.jquery.com/jquery.extend/)를 사용한 깊은 복사와 lodash의 [Lodash _.cloneDeep](https://lodash.com/docs/#cloneDeep)을 활용한 깊은 복사가 있습니다.

```javascript
// jQuery
let copyObject= = $.extend(true, {}, obj);

// lodash
let copyObject= = _.cloneDeep(true, {}, obj);
```


<br><br><br>