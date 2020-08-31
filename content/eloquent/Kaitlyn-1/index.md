---
title: "reverseArrayInPlace"
author: "Kaitlyn Brewer"
date: 2020-08-30T18:53:50-04:00
draft: false
type: article
---

This will be an explaination for the reverseArrayInPlace function from Eloquent JavaScript chapter 4. 

<!--more-->
## The Problem

Create a function that changes a given array by reversing its elements, without using the standard reverse method.

## The Solution
Here is the full code for the solution, as well as the test given by the book.

```{javascript}
function reverseArrayInPlace(array) {
   for (let i = 0; i < Math.floor(array.length / 2); i++) {
     let old = array[i];
     array[i] = array[array.length - 1 - i];
     array[array.length - 1 - i] = old;
   }
   return array;
 }
//Test
let arrayValue = [1, 2, 3, 4, 5];
reverseArrayInPlace(arrayValue);
console.log(arrayValue);
```
Now let's go through it line by line. 

```{javascript}
function reverseArrayInPlace(array) {
   for (let i = 0; i < Math.floor(array.length / 2); i++) {
```
This is just the function declaration and the for loop. The for loop will start at the 0th place in the array-- the first element. It will go through each element until it reaches the point at which i is no longer less than the lowest whole number closest to the length of the array divided by 2. In the book-given test, that point is when i is 2. 


```{javascript}
let old = array[i];
array[i] = array[array.length - 1 - i];
```
Here, for any point in the array, that element will be replaced by the element in the point of the array length minus 1 minus i. 

```{javascript}
 array[array.length - 1 - i] = old;
   }
```
Now, the element of the aray at the point of the array length minus 1 minus i will be replaced by the element in the array at point i.

```{javascript}
   return array;
 }
 ```
 After the loop is completed (i reaches the point where it is no longer less than the lowest value that is closest to the value of the array length divided by 2), the final modified array is returned. 

 ## Example in Debugger
 For a more specific and in depth look, watch the following video. I also ran through another example, which I had not planned out and did not think about until I was already recording, my apologies if that section is disjointed or confusing. 

 {{< youtube az793kJs-RM >}}