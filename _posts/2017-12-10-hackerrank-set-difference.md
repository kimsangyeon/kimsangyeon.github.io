---
layout: post
title: "Set .difference() Operation"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### Set .difference() Operation

<br>

Input Format

<br>

The first line contains the number of students who have subscribed to the English newspaper. <br>
The second line contains the space separated list of student roll numbers who have subscribed to the English newspaper. <br>
The third line contains the number of students who have subscribed to the French newspaper. <br>
The fourth line contains the space separated list of student roll numbers who have subscribed to the French newspaper. <br>

<br><br>

Output Format

<br>

Output the total number of students who are subscribed to the English newspaper only.

<br>

> Sample Input
~~~
9
1 2 3 4 5 6 7 8 9
9
10 1 2 3 11 21 55 6 8
~~~

<br>

> Sample Output
~~~
4
~~~

<br><br>

### My code

<br>

```python
n = input();
s = set(map(int, input().split()));
n = input();
print(len(s.difference(set(map(int, input().split())))))
```

<br>
<br>

[Hacker Rank > Python > set > Set .difference() Operation ](https://www.hackerrank.com/challenges/py-set-difference-operation/problem)