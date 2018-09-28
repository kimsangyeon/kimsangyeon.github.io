---
layout: post
title: "Check Subset"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### Check Subset

<br>

Input Format

<br>

The first line will contain the number of test cases, T. 
The first line of each test case contains the number of elements in set A.
The second line of each test case contains the space separated elements of set A.
The third line of each test case contains the number of elements in set B.
The fourth line of each test case contains the space separated elements of set B.

<br><br>


Output Format

<br>

Output True or False for each test case on separate lines.

<br><br>

Explanation

<br>

Test Case 01 Explanation

<br>

Set A = {1 2 3 5 6} <br>
Set B = {9 8 5 6 3 2 1 4 7} <br>
All the elements of set A are elements of set B. <br>
Hence, set A is a subset of set B. <br>

<br>

> Sample Input
~~~
3
5
1 2 3 5 6
9
9 8 5 6 3 2 1 4 7
1
2
5
3 6 5 4 1
7
1 2 3 5 6 8 9
3
9 8 2
~~~

<br><br>

> Sample Output
~~~
True 
False
False
~~~

<br><br>

### My code
<br>

```python
for i in range(int(input())):
    a = int(input()); A = set(input().split()) 
    b = int(input()); B = set(input().split())
    bSubSet = True
    for a in A:
        if a not in B:
            bSubSet = False
    print(bSubSet)
```

<br>
<br>

[Hacker Rank > Python > set > Check Subset ](https://www.hackerrank.com/challenges/py-check-subset/problem)