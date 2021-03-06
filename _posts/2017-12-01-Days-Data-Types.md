---
layout: post
title: "Days 0: Data Types"
categories: [ Javascript ]
image: assets/images/banner/javascript.png
author: yeon
---

# hacker rank

<br>

---
## 10 Days of Javascript

<br>

### Days 0: Data Types

<br>

Input Format <br>



| Data Type | Parameter | Description |
| :-------- | :-------: | ----------: |
| string    | second Integer | The string representation of an integer you must sum with first Integer. |
string      | second Decimal | The string representation of a floating-point number you must sum with firstDecimal. |
string      | second String  | A string of one or more space-separated words you must append to second String. |

<br>

Output Format

<br>

Print the following three lines of output:

<br>

On the first line, print the sum of first Integer and the integer representation of second Integer. <br>
On the second line, print the sum of first Decimal and the floating-point representation of first Decimal. <br>
On the third line, print first String concatenated with second String. You must print first String before second String. <br>

<br>

> Sample Input
~~~
12
4.32
is the best place to learn and practice coding!
~~~

<br>

> Sample Output
~~~
16
8.32
HackerRank is the best place to learn and practice coding!
~~~

<br><br>

### My code

<br>

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