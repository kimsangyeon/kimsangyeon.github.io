---
layout: post
title: "Polar Coordinates"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### Polar Coordinates

<br>

Input Format

<br>

A single line containing the complex number z. Note: complex() function can be used in python to convert the input as a complex number.

<br>

Output Format

<br>

Output two lines: <br>
The first line should contain the value of r. <br>
The second line should contain the value of A. <br>

<br>

Explanation

<br>

Set A is the strict superset of the set([1,2,3,4,5]) but not of the set([100,11,12]) because 100 is not in set A. 
Hence, the output is False.

<br>

> Sample Input
~~~
1+2j
~~~

<br>

> Sample Output
~~~
2.23606797749979 
1.1071487177940904
~~~

<br><br>

### My code

<br>

```python
from cmath import phase
z = complex(input())
print(abs(z))
print(phase(z))
```

<br>
<br>

[Hacker Rank > Python > math > Polar Coordinates ](https://www.hackerrank.com/challenges/polar-coordinates/submissions/code/60787056)