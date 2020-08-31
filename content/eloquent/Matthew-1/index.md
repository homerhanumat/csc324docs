---
title: "Matthew Article 1"
author: "Matthew Mills"
date: 2020-08-29T13:04:55-04:00
draft: false
type: article
---

An article explaining my solution to the sum of a range of numbers bonus range exercise from chapter 4.

<!--more-->

## The Problem

You can check out the problem here: https://eloquentjavascript.net/04_data.html
{{< rawhtml >}}
<blockquote>
The introduction of this book alluded to the following as a nice way to compute the sum of a range of numbers:

console.log(sum(range(1, 10)));
Write a range function that takes two arguments, start and end, and returns an array containing all the numbers from start up to (and including) end.

Next, write a sum function that takes an array of numbers and returns the sum of these numbers. Run the example program and see whether it does indeed return 55.

As a bonus assignment, modify your range function to take an optional third argument that indicates the “step” value used when building the array. If no step is given, the elements go up by increments of one, corresponding to the old behavior. The function call range(1, 10, 2) should return [1, 3, 5, 7, 9]. Make sure it also works with negative step values so that range(5, 2, -1) produces [5, 4, 3, 2].

Write a function arrayToList that builds up a list structure like the one shown when given [10, 20] as argument.
</blockquote>
{{< /rawhtml >}}

## My Solution

Here is the full code to my solution:

```{javascript}
let range = function(start, end, step) {
    let array = [];
    for (let m = start; step > 1 || step === undefined ? m <= end : m >= end; step ? m = m + step : m++)
        array.push(m);
    return array;
};

let sum = function(arrays) {
    return arrays.reduce(function(x, y) {
        return x + y;
    });
};
```
Here is the code i will be explaning.

```{javascript}
function range(start, end, step = start < end ? 1 : -1) {
  let array = [];

  if (step > 0) {
    for (let i = start; i <= end; i += step) array.push(i);
  } else {
    for (let i = start; i >= end; i += step) array.push(i);
  }
  return array;
}

function sum(array) {
  let total = 0;
  for (let value of array) {
    total += value;
  }
  return total;
}
```


Here is the code that the textbook gives for us to try the function on:

```{javascript}
console.log(range(1, 10));
console.log(range(5, 2, -1));
console.log(sum(range(1, 10)));
```
lets go through this line by line.

```{javascript}
function range(start, end, step = start < end ? 1 : -1) {
  let array = [];
```
this is function being created and it having 3 arguments. there is also an array being created

```{javascript}
if (step > 0) {
    for (let i = start; i <= end; i += step) array.push(i);
  }
```
this 'if' statment is for if you ender a step argument that is greater than 0. the 'for' loop it is taking the 'start' argument 
and comparing it to the end argument to see if the start value is less than the end argument. it is also checking to see what the step argument is.

```{javascript}
else {
    for (let i = start; i >= end; i += step) array.push(i);
  }
  return array;
}
```
this is for if the step argument is not greater than 0 or is undefined. it then does the same thing as the last chunk just with a fixed step value. after the 'if' and 'else' are done it then returns the end values for each argument.








