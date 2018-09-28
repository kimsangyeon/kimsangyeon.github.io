---
layout: post
title: "Introduction to Sets"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

---
## Python Practice

<br>

### Intoroduction to Sets

<br>

Input Format*

<br>

The first line contains the integer, N, the total number of plants. <br>
The second line contains the N space separated heights of the plants. <br>

<br>

> Sample Input
~~~
10
161 182 161 154 176 170 167 171 170 174
~~~

<br>

> Sample Output
~~~
169.375
~~~

<br><br>

### My code

<br>

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