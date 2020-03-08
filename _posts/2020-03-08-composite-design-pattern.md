---
layout: post
title: 'Composite Pattern'
categories: [design pattern]
image: assets/images/banner/designPattern.png
author: yeon
---

# Composite Pattern

에디터 구현시 사용했던 Element 구조의 형태가 `Composite Pattern`이였다는 것을 알고 구현에 사용했던 design pattern이 어떤 패턴에 해당하는 것인지 알고 구현했다면, 좀 더 좋은 프로그램 구조를 갖출 수 있지 않았을까 아쉬움을 가진채 위키피디아에 정리된 `Composite Pattern`을 다시 정리해 봅니다. <br>

<br><br>

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

Leaft 객체는 요청을 직접 수행하는 역할을 하고 Composite 객체는 트리 구성요소 아래로 재귀적으로 자식 구성요소로 요청을 전달합니다. 이를 통해 객체를 균일하게 처리하여 쉽게 구현, 변경, 테스트 및 재사용을 할 수 있습니다. <br>

<br>
