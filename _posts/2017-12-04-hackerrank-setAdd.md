---
layout: post
title: "set.add()"
categories: [ Python ]
author: "Yeon"
---

# hacker rank

## Python Practice
### set.add()

Input Format

The first line contains an integer N, the total number of country stamps.
The next N lines contains the name of the country where the stamp is from. 

Output Format

Output the total number of distinct country stamps on a single line.

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

> Sample Output
~~~
5
~~~

### My code
```python
if __name__ == '__main__':
    n = int(raw_input())
    print(len(set([str(raw_input()) for _ in range(n)])))
```

<br>
<br>

[Hacker Rank > Python > set > set.add() ](https://www.hackerrank.com/challenges/py-set-add/problem)