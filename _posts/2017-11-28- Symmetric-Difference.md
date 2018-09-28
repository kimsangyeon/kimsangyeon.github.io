---
layout: post
title: "Symmetic Difference"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

---
## Python Practice

<br>

### Symmetic Difference!

<br>

Input Format

<br>

The first line of input contains an integer, M. <br>
The second line contains M space-separated integers. <br>
The third line contains an integer, N. <br>
The fourth line contains N space-separated integers. <br>

<br>

> Sample Input
~~~
4
2 4 5 9
4
2 4 11 12
~~~

<br>

> Sample Output
~~~
5
9
11
12
~~~

<br><br>

### My code

<br>

```python
if __name__ == '__main__':
    a,b = [set(input().split()) for _ in range(4)][1::2]
    print('\n'.join(sorted(a^b, key=int)))
```

<br>
<br>

[Hacker Rank > Python > String > Symmetric-Difference ](https://www.hackerrank.com/challenges/symmetric-difference/problem)