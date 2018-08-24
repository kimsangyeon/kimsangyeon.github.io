---
layout: post
title: "Check Strict Subset"
categories: [ Python ]
author: yeon
---

# hacker rank

## Python Practice
### Check Strict Subset

Input Format

The first line contains the space separated elements of set A. 
The second line contains integer n, the number of other sets. 
The next n lines contains the space separated elements of the other sets.

Output Format

Print True if set A is a strict superset of all other N sets. Otherwise, print False.

Explanation

Set A is the strict superset of the set([1,2,3,4,5]) but not of the set([100,11,12]) because 100 is not in set A. 
Hence, the output is False.

> Sample Input
~~~
1 2 3 4 5 6 7 8 9 10 11 12 23 45 84 78
2
1 2 3 4 5
100 11 12
~~~

> Sample Output
~~~
False
~~~

### My code
```python
setA = set(map(int, input().split()))

bStrictSuperSet = True
for _ in range(int(input())):
    setN = set(map(int, input().split()))
    for n in setN:
        if n not in setA:
            bStrictSuperSet = False
            break
print(bStrictSuperSet)
    
```

<br>
<br>

[Hacker Rank > Python > set > Check Strict Superset ](https://www.hackerrank.com/challenges/py-check-strict-superset/problem)