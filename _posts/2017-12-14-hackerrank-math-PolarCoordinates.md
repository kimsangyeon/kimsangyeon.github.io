---
layout: post
title: "Polar Coordinates"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

## Python Practice
### Polar Coordinates

Input Format

A single line containing the complex number z. Note: complex() function can be used in python to convert the input as a complex number.

Output Format

Output two lines: 
The first line should contain the value of r. 
The second line should contain the value of A.

Explanation

Set A is the strict superset of the set([1,2,3,4,5]) but not of the set([100,11,12]) because 100 is not in set A. 
Hence, the output is False.

> Sample Input
~~~
1+2j
~~~

> Sample Output
~~~
2.23606797749979 
1.1071487177940904
~~~

### My code
```python
from cmath import phase
z = complex(input())
print(abs(z))
print(phase(z))
```

<br>
<br>

[Hacker Rank > Python > math > Polar Coordinates ](https://www.hackerrank.com/challenges/polar-coordinates/submissions/code/60787056)