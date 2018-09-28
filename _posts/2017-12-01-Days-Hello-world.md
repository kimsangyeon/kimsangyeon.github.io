---
layout: post
title: "Days 0: Hello world!"
categories: [ Javascript ]
image: assets/images/banner/javascript.png
author: yeon
---

# hacker rank

<br>

---
## 10 Days of Javascript

<br>

### Days 0: Hello world!

<br>

Input Format

<br>

| Data Type | Parameter | Description |
| :-------- | :-------: | ----------: |
| string    | parameter valiable| A single line of text containing one or more space-separated words. |

<br>

Output Format

<br>

Print the following two lines of output:

<br>

1. On the first line, print Hello, World! (this is provided for you in the editor). <br>
2. On the second line, print the contents of parameter valiable. <br>

<br>

> Sample Input
~~~
Welcome to 10 Days of JavaScript!
~~~

<br>

> Sample Output
~~~
Hello, World!
Welcome to 10 Days of JavaScript!
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
*   A line of code that prints "Hello, World!" on a new line is provided in the editor. 
*   Write a second line of code that prints the contents of 'parameterVariable' on a new line.
*
*	Parameter:
*   parameterVariable - A string of text.
**/
function greeting(parameterVariable) {
    // This line prints 'Hello, World!' to the console:
    console.log('Hello, World!');
    console.log(parameterVariable);
}

function main() {
    const parameterVariable = readLine();
    
    greeting(parameterVariable);
}
```

<br>
<br>

[Hacker Rank > 10 Days of Javascript > Days 0: Hello world!Symmetric-Difference ](https://www.hackerrank.com/challenges/js10-hello-world/problem)