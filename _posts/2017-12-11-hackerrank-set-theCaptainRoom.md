---
layout: post
title: "The Captain's Room"
author: "Yeon"
---

# hacker rank

## Python Practice
### The Captain's Room

Input Format

The first line consists of an integer, K, the size of each group.
The second line contains the unordered elements of the room number list.



Output Format

Output the Captain's room number.

Explanation

The list of room numbers contains 31 elements. Since K is 5, there must be 6 groups of families. In the given list, all of the numbers repeat 5 times except for room number 8. 
Hence, 8 is the Captain's room number.

> Sample Input
~~~
5
1 2 3 6 5 4 4 2 5 3 6 1 6 5 3 2 4 1 2 5 1 4 3 6 8 4 3 1 5 6 2 
~~~

> Sample Output
~~~
8
~~~

### My code
```python
k,arr = int(input()),list(map(int, input().split()))
myset = set(arr)
print(((sum(myset)*k)-(sum(arr)))//(k-1))

```

<br>
<br>

[Hacker Rank > Python > set > The Captain's Room ](https://www.hackerrank.com/challenges/py-the-captains-room/problem)