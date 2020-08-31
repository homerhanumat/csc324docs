---
title: "Ch03: Recursion"
author: "Riley Noe"
date: 2020-08-30T20:53:24-04:00
draft: falsegit 
type: article
---

## Problem

**CHAPTER 3: Recursion**

We’ve seen that % (the remainder operator) can be used to test whether a 
number is even or odd by using % 2 to see whether it’s divisible by two. 
Here’s another way to define whether a positive whole number is even or odd:

Zero is even.

One is odd.

For any other number N, its evenness is the same as N - 2.

Define a recursive function isEven corresponding to this description. The 
function should accept a single parameter (a positive, whole number) and return 
a Boolean.

Test it on 50 and 75. See how it behaves on -1. Why? Can you think of a way 
to fix this?

<!--more-->

 ## Here is my code:

```javascript

debugger;
function isEven(n) {

    //If n is negative, it is multiplied by -1 to turn positive.
    if (n < 0) {
        n = n * -1;
    }

    //if n equals 0, the number is even and the function ends.
    if (n==0) {
        return true;
    }

    //if n is 1, the number is odd and the function ends.
    if (n==1) {
        return false;
    }

    // if n is neither 0 or 1, the function will reach the recurvise function, which subtracts 2 from n to 
    // bring n closer to 0 or 1.
    return isEven(n - 2);
    
}

console.log(isEven(75));
//false

console.log(isEven(50));
//true

console.log(isEven(-1));
//false

```

## Explaination:

The function isEven is used to determine whether the parameter n is odd or even. It does this using three if statements. The first if statement is used to determine whether or not n is positive or negative. If n is negative is redefined to n * -1, turning it positive. If n is already positive the function will jump to the next if statement. The second if statement returns true if n is equal to 0. The boolean value true is only returned if the original n is even. The third if statement returns false if n is equal to 1. False is only returned if the original value of n is negative. If n is greater than 1, return isEven(n-2) is a recursive function that restarts the entire function with a number closer to 1 and 0. If the original n is 75, the function will subtract 2 from n every loop until it reaches 1. 

This function also works with negative numbers. For example, if we use the debugger to run the code:
console.log(isEven(-5)); the following will happen:

Since n equals -5, the debugger will enter into the first if statement. The parameter n will be redifined as n * -1, which means that -5 is now 5. Essentially, I am taking the absolute value of n to ensure that the recursive function doesn't enter an infinite loop of subtracting 2 from an already negative number. Next, the debugger will pass over the next two if statements because n is neither 0 or 1. The debugger will enter the recursive function, returning the function isEven(3). As 3 is positive and neither 0 or 1, the debugger will pass over the first three if statments and enter into the recursive function. 2 is subtracted from 3 and returned into the function isEven as 1. This means that the debugger will start from the top, skipping the first 2 if statements becuase 1 is neither negative or 0. When the debugger reaches the third if statement, it will enter because 1 == 1. It will then return false because 1 is an odd number. Once the boolean value is returned, the debugger will be stopped.

