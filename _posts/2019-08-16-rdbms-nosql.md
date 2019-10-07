---
layout: post
title: "RDBMS NOSQL 차이"
categories: [ sql, nosql, database ]
image: assets/images/banner/sqlnosql.png
author: yeon
---

# RDBMS NOSQL 차이
데이터베이스에서 크게 두가지로 나뉘는 관계형 데이터베이스와 No SQL에 대해 간략히 정리해봅니다. <br>

<br>

데이터 베이스를 잘몰라 NOSQL이 처음에는 No SQL이라고 생각을 하였다... <br>
NO SQL은 Not Only SQL로 관계형 데이터베이스가 아닌 데이터 베이스로 이해하는 것이 좋을 것 같습니다. 그래서 Not Only 혹은 Non relational Database라고도 부른다고 합니다.

<br><br>

## RDBMS
SQL은 Structured Query Language의 약자로 데이터베이스에서 사용하는 쿼리 언어 입니다. SQL을 사용하여 RDBMS에서 데이터를 검색, 저장, 수정, 삭제 등이 가능합니다. RDBMS는 Relational Database Management System으로 말 그대로 관계형 데이터베이스 관리 시스템입니다. RDBMS는 정해져있는 데이터 스키마에 따라 데이터베이스 테이블에 저장되며, 관계를 통한 테이블간 연결을 통해 사용됩니다. 이 때문에 RDBMS는 데이터 관리를 효율적으로 하기위해 구조화가 굉장히 중요합니다. <br>

<br><br>

### RDBMS 장점
RDBMS 장점으로는 정해진 스키마에 따라 데이터를 저장하여야 하기 때문에 명확한 데이터 구조를 보장합니다. 그리고 각 데이터에 맞게 테이블을 나누어 데이터 중복을 피해 데이터 공간을 절약 할 수 있습니다. <br>

<br>

### RDBMS 단점
RDBMS 단점으로는 Oracle 같은 시스템을 사용하게 될 경우 비용적으로 부담이 될 수 있습니다. 그리고 RDBMS 관계로 인한 시스템 복잡도를 고려하여 구조화를 해야합니다. 시스템이 복잡해 질수록 Query문이 복잡해지고 성능이 저하됩니다. 또한 수평적확장이 어려워 수직적 확장을 대부분 하기 때문에 한계에 직면할 수 있습니다. <br>

<br><br>

## NOSQL
NOSQL은 위에 설명했듯 Not Only SQL, Non relational Database라고 부른다고 합니다. NOSQL은 관계형 데이터베이스와 반대되는 방식을 사용하여 스키마와 관계라는 개념이 없습니다. RDBMS에서는 스키마에 맞추어 데이터를 관리하여야 하지만 NOSQL은 스키마가 없어 좀 더 자유롭게 데이터를 관리할 수 있습니다. NOSQL에서 테이블과 같은 개념으로 컬렉션이라는 형태로 데이터를 관리합니다.

<br><br>

### NOSQL 장점
NOSQL 장점으로는 정해진 스키마에 따라 저장해야하는 RDBMS 보다 자유롭게 데이터를 추가가 가능합니다. 이는 복잡한 테이블간의 관계를 형성하는 형태의 구조를 신경쓰지 않아도 됩니다. 예로는 조인 등 복잡한 SQL구문으로 인한 문제가 있겠습니다. NOSQL에서는 필요한 데이터가 보통 하나의 컬렉션에 있으며, 이는 자주 변경되지 않는 데이터에 큰 장점이 있다고 합니다. 그리고 다른 장점으로는 수평적 확장이 어려운 RDBMS보다는 수평적 확장이 쉽다는 점 입니다. <br>

<br>

### RDBMS 단점
NOSQL 단점으로는 자유롭게 데이터가 추가가 가능하기 때문에 컬렉션에 중복된 데이터가 저장이 가능합니다. 데이터 업데이트시 중복되어 저장되어있는 데이터를 똑같이 관리(업데이트)해 주어야 합니다.


<br><br><br> 