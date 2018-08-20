---
layout: post
title: "No Idea!"
author: "Yeon"
---

# hacker rank

## Python Practice
### No Idea!

Input Format

The first line contains integers n and m separated by a space. 
The second line contains n integers, the elements of the array. 
The third and fourth lines contain m integers, A and B, respectively.


Output Format

Output a single integer, your total happiness.

> Sample Input
~~~
3 2
1 5 3
3 1
5 7
~~~

> Sample Output
~~~
1
~~~

### My code
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