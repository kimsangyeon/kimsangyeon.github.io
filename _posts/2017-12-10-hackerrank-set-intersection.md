---
layout: post
title: "Set .intersection() Operation"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### Set .intersection() Operation

<br>

Input Format

<br>

The first line contains n, the number of students who have subscribed to the English newspaper. <br>
The second line contains n space separated roll numbers of those students. <br>
The third line contains b, the number of students who have subscribed to the French newspaper. <br>
The fourth line contains b space separated roll numbers of those students. <br>

<br><br>

Output Format

<br>

Output the total number of students who have subscriptions to both English and French newspapers.

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
5
~~~

<br><br>

### My code

<br>

```python
n = input();
s = set(map(int, input().split()));
n = input();
print(len(s.intersection(set(map(int, input().split())))))
```

<br>
<br>

[Hacker Rank > Python > set > Set .intersection() Operation ](https://www.hackerrank.com/challenges/py-set-intersection-operation/problem)