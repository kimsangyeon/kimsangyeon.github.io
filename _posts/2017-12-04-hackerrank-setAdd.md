---
layout: post
title: "set.add()"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### set.add()

<br>

Input Format

<br>

The first line contains an integer N, the total number of country stamps. <br>
The next N lines contains the name of the country where the stamp is from. <br>

<br>

Output Format

<br>

Output the total number of distinct country stamps on a single line.

<br>

> Sample Input
~~~
7
UK
China
USA
France
New Zealand
UK
France 
~~~

<br>

> Sample Output
~~~
5
~~~

<br><br>

### My code

<br>

```python
if __name__ == '__main__':
    n = int(raw_input())
    print(len(set([str(raw_input()) for _ in range(n)])))
```

<br>
<br>

[Hacker Rank > Python > set > set.add() ](https://www.hackerrank.com/challenges/py-set-add/problem)