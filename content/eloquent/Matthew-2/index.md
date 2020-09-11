---
title: "Matthew Article 2"
author: "Matthew Mills"
date: 2020-08-29T13:04:55-04:00
draft: false
type: article
---

An article explaining the issues with my solution for the flattening exercise from chapter 5.

<!--more-->

## The Problem

You can check out the problem here: https://eloquentjavascript.net/05_higher_order.html
{{< rawhtml >}}
<blockquote>
Use the reduce method in combination with the concat method to “flatten” an array of arrays into a single array that
 has all the elements of the original arrays.
</blockquote>
{{< /rawhtml >}}

## My Solution

Here is the full code to my solution:

```{javascript}
let arrays = [[1, 2, 3], [4, 5], [6]];
console.log(arrays.reduce((array1, array2) => array1.concat(array2)));
```

Here is the code that the textbook gives for us to try the function on:


```{javascript}
let arrays = [[1, 2, 3], [4, 5], [6]];
```

lets go through this line by line.

```{javascript}
console.log(arrays.reduce((array1, array2) => array1.concat(array2)));
```
this works as long as 'arrays' is not an empty array. if it is empty it will produce an error instead of giving you your desired output.

## The Fix

The fix to my issue: 

```{javascript}
console.log(arrays.reduce(function(flat, current) {
  return flat.concat(current);
}, []));
```
the code above while almost look exactly the same as my solution, it has its diffrences. the '[]' at the end provides an empty array so the rest of the values can be added to that empty array. 









