---
layout: post
title: "No Idea!"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### No Idea!

<br>

Input Format

<br>

The first line contains integers n and m separated by a space. <br>
The second line contains n integers, the elements of the array. <br>
The third and fourth lines contain m integers, A and B, respectively. <br>

<br>

Output Format

<br>

Output a single integer, your total happiness.

<br>

> Sample Input
~~~
3 2
1 5 3
3 1
5 7
~~~

<br>

> Sample Output
~~~
1
~~~

<br><br>

### My code

<br>

```python
n, m = raw_input().split()
arr = map(int, raw_input().split())
a = set(map(int, raw_input().split()))
b = set(map(int, raw_input().split()))

count = [1 if x in a else -1 if x in b else 0 for x in arr]

print(sum(count))
```

<br>
<br>

[Hacker Rank > Python > set > No Idea! ](https://www.hackerrank.com/challenges/no-idea/problem)