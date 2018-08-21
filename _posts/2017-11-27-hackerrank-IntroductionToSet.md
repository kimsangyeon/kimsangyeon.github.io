---
layout: post
title: "Introduction to Sets"
categories: [ Python ]
author: "Yeon"
---

# hacker rank
---
## Python Practice
### Intoroduction to Sets

Input Format

The first line contains the integer, N, the total number of plants.
The second line contains the N space separated heights of the plants.



> Sample Input
~~~
10
161 182 161 154 176 170 167 171 170 174
~~~

> Sample Output
~~~
169.375
~~~

### My code
```python
def average(array):
    arraySet = set(array);
    return sum(arraySet)/len(arraySet);

if __name__ == '__main__':
    n = int(input())
    arr = list(map(int, input().split()))
    result = average(arr)
    print(result) 
```

<br>
<br>

[Hacker Rank > Python > Set > Introduction to Sets ](https://www.hackerrank.com/challenges/py-introduction-to-sets/problem)