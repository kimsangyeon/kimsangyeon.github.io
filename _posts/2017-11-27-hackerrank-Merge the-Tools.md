---
layout: post
title: "Merge the Tools!"
categories: [ Python ]
image: assets/images/banner/python.png
author: yeon
---

# hacker rank

<br>

---
## Python Practice

<br>

### Merge the Tools!

<br>

The first line contains a single string denoting s. <br>
The second line contains an integer, k, denoting the length of each subsegment. <br>

<br>

> Sample Input
~~~
AABCAAADA
3
~~~

<br>

> Sample Output
~~~
AB
CA
AD
~~~

<br><br>

### My code

<br>

```python
def merge_the_tools(string, k):
    splitNum = len(string)/k;
    for i in range(0, len(string), k):
        str = string[i:i+k];
        sub = ''
        for s in str:
            if s not in sub:
                sub += s;
        print(sub);

if __name__ == '__main__':
    string, k = input(), int(input())
    merge_the_tools(string, k)  
```

<br>
<br>

[Hacker Rank > Python > String > Merge the Tools! ](https://www.hackerrank.com/challenges/merge-the-tools/copy-from/59294080)