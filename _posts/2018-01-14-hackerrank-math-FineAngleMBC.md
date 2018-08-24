---
layout: post
title: "Find Angle MBC"
categories: [ Python ]
author: yeon
---

# hacker rank

## Python Practice
### Find Angle MBC

Input Format

The first line contains the length of side AB.
The second line contains the length of side BC.

Output Format

Output <MBC in degrees. 

Note: Round the angle to the nearest integer.

Examples: 
If angle is 56.5000001°, then output 57°. 
If angle is 56.5000000°, then output 57°. 
If angle is 56.4999999°, then output 56°.
> Sample Input
~~~
10
10
~~~

> Sample Output
~~~
45°
~~~

### My code
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