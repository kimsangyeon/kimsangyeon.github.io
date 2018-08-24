---
layout: post
title: "Check Subset"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

## Python Practice
### Check Subset

Input Format

The first line will contain the number of test cases, T. 
The first line of each test case contains the number of elements in set A.
The second line of each test case contains the space separated elements of set A.
The third line of each test case contains the number of elements in set B.
The fourth line of each test case contains the space separated elements of set B.



Output Format

Output True or False for each test case on separate lines.



Explanation

Test Case 01 Explanation

Set A = {1 2 3 5 6} 
Set B = {9 8 5 6 3 2 1 4 7} 
All the elements of set A are elements of set B. 
Hence, set A is a subset of set B.
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

> Sample Output
~~~
True 
False
False
~~~

### My code
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