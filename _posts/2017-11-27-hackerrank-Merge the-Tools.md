---
layout: post
title: "Merge the Tools!"
categories: [ Python ]
author: yeon
---

# hacker rank
---
## Python Practice
### Merge the Tools!

The first line contains a single string denoting s. 
The second line contains an integer, k, denoting the length of each subsegment.

> Sample Input
~~~
AABCAAADA
3
~~~

> Sample Output
~~~
AB
CA
AD
~~~

### My code
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