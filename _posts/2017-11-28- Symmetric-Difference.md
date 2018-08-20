---
layout: post
title: "Symmetic Difference"
author: "Yeon"
---

# hacker rank
---
## Python Practice
### Symmetic Difference!

Input Format

The first line of input contains an integer, M. 
The second line contains M space-separated integers. 
The third line contains an integer, N. 
The fourth line contains N space-separated integers.

> Sample Input
~~~
4
2 4 5 9
4
2 4 11 12
~~~

> Sample Output
~~~
5
9
11
12
~~~

### My code
```python
if __name__ == '__main__':
    a,b = [set(input().split()) for _ in range(4)][1::2]
    print('\n'.join(sorted(a^b, key=int)))
```

<br>
<br>

[Hacker Rank > Python > String > Symmetric-Difference ](https://www.hackerrank.com/challenges/symmetric-difference/problem)