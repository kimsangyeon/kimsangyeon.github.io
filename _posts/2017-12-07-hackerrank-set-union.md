---
layout: post
title: "Set .union() Operation"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### Set .union() Operation

<br>

Input Format

<br>

The first line contains an integer, n, the number of students who have subscribed to the English newspaper. <br>
The second line contains n space separated roll numbers of those students. <br>
The third line contains b, the number of students who have subscribed to the French newspaper. <br>
The fourth line contains b space separated roll numbers of those students. <br>

<br>

Output Format

<br>

Output the total number of students who have at least one subscription.

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
13
~~~

<br>

### My code

<br>

```python
n = input()
s1 = set(map(int, raw_input().split()))
n = input()
s2 = set(map(int, raw_input().split()))

result = s1.union(s2)

print(len(result))
```

<br>
<br>

[Hacker Rank > Python > set > Set .union() Operation ](https://www.hackerrank.com/challenges/py-set-union/problem)