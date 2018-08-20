---
layout: post
title: "Set .union() Operation"
author: "Yeon"
---

# hacker rank

## Python Practice
### Set .union() Operation

Input Format

The first line contains an integer, n, the number of students who have subscribed to the English newspaper. 
The second line contains n space separated roll numbers of those students. 
The third line contains b, the number of students who have subscribed to the French newspaper. 
The fourth line contains b space separated roll numbers of those students.


Output Format

Output the total number of students who have at least one subscription.

> Sample Input
~~~
9
1 2 3 4 5 6 7 8 9
9
10 1 2 3 11 21 55 6 8
~~~

> Sample Output
~~~
13
~~~

### My code
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