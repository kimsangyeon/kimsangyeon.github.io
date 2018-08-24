---
layout: post
title: "Set .discard(), .remove() & .pop()"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

## Python Practice
### Set .discard(), .remove() & .pop()

Input Format

The first line contains integer n, the number of elements in the set s. 
The second line contains n space separated elements of set s. All of the elements are non-negative integers, less than or equal to 9. 
The third line contains integer N, the number of commands.
The next N lines contains either pop, remove and/or discard commands followed by their associated value.



Output Format

Print the sum of the elements of set s on a single line.

> Sample Input
~~~
1 2 3 4 5 6 7 8 9
10
pop
remove 9
discard 9
discard 8
remove 7
pop 
discard 6
remove 5
pop 
discard 5 
~~~

> Sample Output
~~~
4
~~~

### My code
```python
n = input()
s = set(map(int, raw_input().split())) 
cmdLength = input()

for _ in range(cmdLength):
    aCmd = map(str, raw_input().split())
    if(len(aCmd) > 1):
        eval('s.%s(%s)' % (aCmd[0], aCmd[1]))
    else:
        eval('s.%s()' % aCmd[0])

print(sum(s))
```

<br>
<br>

[Hacker Rank > Python > set > Set .discard(), .remove() & .pop() ](https://www.hackerrank.com/challenges/py-set-discard-remove-pop/problem)