---
layout: post
title: "Find Angle MBC"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

## Python Practice

<br>

### Find Angle MBC

<br><br>

Input Format

<br>

The first line contains the length of side AB.
The second line contains the length of side BC.

<br>

Output Format

<br>

Output <MBC in degrees. 

<br>

Note: Round the angle to the nearest integer.

<br>

Examples: 
If angle is 56.5000001°, then output 57°. 
If angle is 56.5000000°, then output 57°. 
If angle is 56.4999999°, then output 56°.

<br>

> Sample Input
~~~
10
10
~~~

<br>

> Sample Output
~~~
45°
~~~

<br><br>

### My code

<br>

```python
from math import atan2
from math import degrees

ab = float(input())
bc = float(input())

print(str(round(degrees(atan2(ab, bc)))) + '°')
```

<br>
<br>

[Hacker Rank > Python > math > Find Angle MBC](https://www.hackerrank.com/challenges/find-angle/problem)