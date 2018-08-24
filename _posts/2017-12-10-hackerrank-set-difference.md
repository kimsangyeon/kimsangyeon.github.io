---
layout: post
title: "Set .difference() Operation"
categories: [ Python ]
author: yeon
---

# hacker rank

## Python Practice
### Set .difference() Operation

Input Format

The first line contains the number of students who have subscribed to the English newspaper. 
The second line contains the space separated list of student roll numbers who have subscribed to the English newspaper.
The third line contains the number of students who have subscribed to the French newspaper. 
The fourth line contains the space separated list of student roll numbers who have subscribed to the French newspaper.



Output Format

Output the total number of students who are subscribed to the English newspaper only.

> Sample Input
~~~
9
1 2 3 4 5 6 7 8 9
9
10 1 2 3 11 21 55 6 8
~~~

> Sample Output
~~~
4
~~~

### My code
```python
n = input();
s = set(map(int, input().split()));
n = input();
print(len(s.difference(set(map(int, input().split())))))
```

<br>
<br>

[Hacker Rank > Python > set > Set .difference() Operation ](https://www.hackerrank.com/challenges/py-set-difference-operation/problem)