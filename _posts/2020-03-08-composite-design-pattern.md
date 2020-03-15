---
layout: post
title: 'Composite Pattern'
categories: [design pattern]
image: assets/images/banner/designPattern.png
author: yeon
---

# Composite Pattern

에디터 구현시 사용했던 Element 구조의 형태가 `Composite Pattern`이였다는 것을 알고 구현에 사용했던 design pattern이 어떤 패턴에 해당하는 것인지 알고 구현했다면, 좀 더 좋은 프로그램 구조를 갖출 수 있지 않았을까 아쉬움을 가진채 위키피디아에 정리된 `Composite Pattern`을 다시 정리해 봅니다. <br>

<br><br><br>

## Composite Pattern 이란?

software enginnering에서 `composite pattern`은 partitioning design pattern 입니다. `composite pattern`은 단일 인스턴스가 동일한 유형의 객체로 취급되어 사용되는 객체 그룹입니다. `composite pattern`의 목적은 개체를 트리 구조로 구성하여 계층 구조를 구성하는 것 입니다. <br>

[wikipedia](https://en.wikipedia.org/wiki/Composite_pattern) <br>

<br>

## Composite Pattern 개요

재사용 가능한 객체지향 소프트웨어, 구현과 변경 테스트 및 반복적인 디자인 문제를 해결하기 위한 23가지 GoF design pattern 중 하나 입니다. <br>

<br>

### Composite Pattern으로 어떤것을 해결 할 수 있나?

- 부분 및 전체 개체를 균일하게 처리 할 수 있도록 부분 전체 계층 구조로 나타낼 수 있습니다.
- 부분 전체 계층 구조를 트리 구조로 나타 낼 수 있습니다. (트리 구조를 사용할 경우 전체 구조에 대해서 반복처리에 용이)

<br>

### Composite Pattern의 해결법은?

- Leaf 객체와 Composite 객체의 공동 Component Interface를 정의 합니다.
- Leaf 객체는 Component Interface를 직접 구현, Composite 객체는 하위 Component로 요청을 전달합니다.

<br>

Leaf 객체는 요청을 직접 수행하는 역할을 하고 Composite 객체는 트리 구성요소 아래로 재귀적으로 자식 구성요소로 요청을 전달합니다. 이를 통해 객체를 균일하게 처리하여 쉽게 구현, 변경, 테스트 및 재사용을 할 수 있습니다. <br>

<br><br><br>

## Composite Pattern 사용

객체의 구성과 개별 객체의 차이가 없을때 `composite pattern`을 사용합니다. 프로그래머가 동일한 방식으로 객체를 사용하고 객체를 처리하는 코드가 거의 동일한 경우 선택하여 사용하는 것이 좋습니다. 이 상황에서는 `promitives`와 `composite`를 균일하게 처리하는 것이 복잡성을 줄여줍니다.

<br>

### UML class and object diagram

![composite uml]({{ site.baseurl }}/assets/images/banner/compositeUML.jpg)

<br>

위의 UML 다이어그램을 보면 `Client Class`는 `Leaf`와 `Composite`를 참조하지 않고 공통 `Component Interface`를 참조하여 `Leaf`와 `Composite`를 균일하게 처리합니다. <br>

- `Leaf`는 자식을 가지지 않으며 직접 `Component Interface`를 구현합니다.
- `Composite`는 Component 객체의 컨테이너를 유지하며 자식에게 요청을 전달합니다.

<br>

Sample Object Collaboration 다이어그램에서는 런타임 상호작용을 보여주고 있습니다. `Client Class`에서 최상위 `Composite` 객체에게 요청을 보냅니다. 그리고 최상위 `Composite` 객체는 트리 구조 아래의 모든 하위 구성요소에게 요청을 전달합니다.

<br><br>

![composite uml2]({{ site.baseurl }}/assets/images/banner/compositeUML2.jpg)

<br>

위의 두 디자인은 컨테이너 Component에 자식을 추가/제거 그리고 자식 관련 작업을 정의하고 구현하는 모습입니다.

- Design for uniformity(균일성 설계): 하위 관련 작업은 `Component Interface`에서 정의됩니다. 이를 통해 `Client`는 `Leaf` 및 `Composite`를 균일하게 처리 할 수 ​​있습니다. 그러나 `Client`가 `Leaf`에 대해 자식 관련 작업을 수행 할 수 있기 때문에 형식 안전이 손실됩니다.

- Design for type safety(안전 설계): 자식 관련 작업은 `Composite`에서만 정의됩니다. `Client`는 `Leaf` 및 `Composite`를 다르게 취급해야합니다. `Client`가 `Leaf`에 대해 자식 관련 작업을 수행 할 수 없기 때문에 형식 안전성이 확보됩니다.

**`Composite Pattern`은 안정성보다는 균일성을 중요시 합니다.**

<br><br>

### UML Class Diagram

![composite uml3]({{ site.baseurl }}/assets/images/banner/compositeUML3.png)

<br>

#### Component

- `Composite`를 포함한 모든 Component 추상화
- `Composition`에 대한 Interface 선언
- 재귀 구조에서 Component 상위에 엑세스 하기 위한 Interface를 정의

#### Leaf

- `Composition`의 `Leaf`
- 모든 Component method 구현

#### Composite

- 자식이 있는 `Composite` Component
- 자식 조작 방법 구현

<br><br><br>

## Composite Pattern 예제

타원 또는 여러 그래픽 구성이 될 수 있는 `Graphic Class`를 구현합니다.

<br>

```
Graphic ::= ellipse | GraphicList
GraphicList ::= empty | Graphic GraphicList
```

<br>

#### Javascript

```javascript
/** Component Interface */
class Graphic {
  constructor() {}

  print() {
    throw console.log('Override Print Method');
  }
}

/** Composite */
class CompositeGraphic extends Graphic {
  constructor() {
    super();
    this.GraphicList = [];
  }

  add(graphic) {
    this.GraphicList.push(graphic);
  }

  print() {
    for (let g of this.GraphicList) {
      g.print();
    }
  }
}

/** Leaf */
class Ellipse extends Graphic {
  constructor() {
    super();
  }

  print() {
    console.log('Ellipse');
  }
}

/** Client */
class CompositeDemo {
  run() {
    //Initialize four ellipses
    const ellipse1 = new Ellipse();
    const ellipse2 = new Ellipse();
    const ellipse3 = new Ellipse();
    const ellipse4 = new Ellipse();

    //Creates two composites containing the ellipses
    const graphic2 = new CompositeGraphic();
    graphic2.add(ellipse1);
    graphic2.add(ellipse2);
    graphic2.add(ellipse3);

    const graphic3 = new CompositeGraphic();
    graphic3.add(ellipse4);

    //Create another graphics that contains two graphics
    const graphic1 = new CompositeGraphic();
    graphic1.add(graphic2);
    graphic1.add(graphic3);

    //Prints the complete graphic (Four times the string "Ellipse").
    graphic1.print();
  }
}
```
