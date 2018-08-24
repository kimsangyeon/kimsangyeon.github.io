---
layout: post
title: "Days 0: Data Types"
categories: [ Javascript ]
author: yeon
---

# hacker rank
---
## 10 Days of Javascript
### Days 0: Data Types

Input Format

| Data Type | Parameter | Description |
| :-------- | :-------: | ----------: |
| string    | second Integer | The string representation of an integer you must sum with first Integer. |
string      | second Decimal | The string representation of a floating-point number you must sum with firstDecimal. |
string      | second String  | A string of one or more space-separated words you must append to second String. |

Output Format

Print the following three lines of output:

On the first line, print the sum of first Integer and the integer representation of second Integer.
On the second line, print the sum of first Decimal and the floating-point representation of first Decimal.
On the third line, print first String concatenated with second String. You must print first String before second String.


> Sample Input
~~~
12
4.32
is the best place to learn and practice coding!
~~~

> Sample Output
~~~
16
8.32
HackerRank is the best place to learn and practice coding!
~~~

### My code
```javascript
'use strict';

process.stdin.resume();
process.stdin.setEncoding('utf-8');

let inputString = '';
let currentLine = 0;

process.stdin.on('data', inputStdin => {
    inputString += inputStdin;
});

process.stdin.on('end', _ => {
    inputString = inputString.trim().split('\n').map(string => {
        return string.trim();
    });
    
    main();    
});

function readLine() {
    return inputString[currentLine++];
}

/**
*   The variables 'firstInteger', 'firstDecimal', and 'firstString' are declared for you -- do not modify them.
*   Print three lines:
*   1. The sum of 'firstInteger' and the Number representation of 'secondInteger'.
*   2. The sum of 'firstDecimal' and the Number representation of 'secondDecimal'.
*   3. The concatenation of 'firstString' and 'secondString' ('firstString' must be first).
*
*	Parameter(s):
*   secondInteger - The string representation of an integer.
*   secondDecimal - The string representation of a floating-point number.
*   secondString - A string consisting of one or more space-separated words.
**/
function performOperation(secondInteger, secondDecimal, secondString) {
    // Declare a variable named 'firstInteger' and initialize with integer value 4.
    const firstInteger = 4;
    
    // Declare a variable named 'firstDecimal' and initialize with floating-point value 4.0.
    const firstDecimal = 4.0;
    
    // Declare a variable named 'firstString' and initialize with the string "HackerRank".
    const firstString = 'HackerRank ';
    
    console.log(firstInteger + parseInt(secondInteger));
    console.log(firstDecimal + parseFloat(secondDecimal));
    console.log(firstString + secondString);
}


function main() {
    const secondInteger = readLine();
    const secondDecimal = readLine();
    const secondString = readLine();
    
    performOperation(secondInteger, secondDecimal, secondString);
}

```

<br>
<br>

[Hacker Rank > 10 Days of Javascript > Days 0: Data Types ](https://www.hackerrank.com/challenges/js10-data-types/problem)