---
layout: post
title: "Set Mutations"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### Set Mutations

<br>

Input Format

<br>

The first line contains the number of elements in set A. <br>
The second line contains the space separated list of elements in set A. <br>
The third line contains integer N, the number of other sets. <br>
The next 2 * N lines are divided into N parts containing two lines each. <br>
The first line of each part contains the space separated entries of the operation name and the length of the other set. <br>
The second line of each part contains space separated list of elements in the other set. <br>

<br>

Output Format <br>

Output the sum of elements in set A. <br>

<br>

> Sample Input
~~~
 16
 1 2 3 4 5 6 7 8 9 10 11 12 13 14 24 52
 4
 intersection_update 10
 2 3 5 6 8 9 1 4 7 11
 update 2
 55 66
 symmetric_difference_update 5
 22 7 35 62 58
 difference_update 7
 11 22 35 55 58 62 66
~~~

<br>

> Sample Output
~~~
38
~~~

<br><br>

### My code

<br>

```python
aLen = int(input());
A = set(map(int, input().split()))
n = int(input());

for _ in range(n):
    cmd, sLen = input().split(' ');
    s = set(map(int, input().split()))
    eval('A.' + cmd + '(s)');
    
print(sum(A))
```

<br>
<br>

[Hacker Rank > Python > set > Set Mutations ](https://www.hackerrank.com/challenges/py-set-mutations/problem)