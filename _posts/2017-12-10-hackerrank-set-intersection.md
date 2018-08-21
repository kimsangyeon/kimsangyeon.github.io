---
layout: post
title: "Set .intersection() Operation"
categories: [ Python ]
author: "Yeon"
---

# hacker rank

## Python Practice
### Set .intersection() Operation

Input Format

The first line contains n, the number of students who have subscribed to the English newspaper. 
The second line contains n space separated roll numbers of those students.
The third line contains b, the number of students who have subscribed to the French newspaper. 
The fourth line contains b space separated roll numbers of those students.



Output Format

Output the total number of students who have subscriptions to both English and French newspapers.

> Sample Input
~~~
9
1 2 3 4 5 6 7 8 9
9
10 1 2 3 11 21 55 6 8
~~~

> Sample Output
~~~
5
~~~

### My code
```python
n = input();
s = set(map(int, input().split()));
n = input();
print(len(s.intersection(set(map(int, input().split())))))
```

<br>
<br>

[Hacker Rank > Python > set > Set .intersection() Operation ](https://www.hackerrank.com/challenges/py-set-intersection-operation/problem)