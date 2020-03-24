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

<br>
