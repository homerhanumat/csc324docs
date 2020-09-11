---
title: "arrayToList as a Recursive Function"
author: "Kaitlyn Brewer"
date: 2020-09-03T14:02:08-04:00
draft: false
type: article
---

This will be a differnt look at the arrayToList function from Eloquent Javascript chapter 4. This will be an alternative, recursive solution.

<!--more-->

## The Problem

Write a function that takes a given array and puts it into a list structure. 

## The Solution
Here is the full code and the book-given test example. 

```{javascript}
function arrayToList(array) {
  let list = new Object();
  if (array.length == 1) {
      list.value = array[array.length - 1];
      list.rest = null;
      return list;
  } else {
      list.value = array[0];
      array.splice(0,1);
      list.rest = arrayToList(array);
      return list;
  }
}
//Test
console.log(arrayToList([10, 20]));
```
Let's go through line by line. 

```{javascript}
function arrayToList(array) {
  let list = new Object();
```
Here we see the function declaration and the creation of a new object for the list to go into. 

```{javascript}
if (array.length == 1) {
      list.value = array[array.length - 1];
      list.rest = null;
      return list;
```
This if statement is to stop the recursion from calling itself again once the array length is 1. Once it finishes with the last value in the array, the rest of the list is set to null and the final list is returned. 

```{javascript}
} else {
      list.value = array[0];
      array.splice(0,1);
      list.rest = arrayToList(array);
      return list;
  }
}
```
This pushes the value of an element in the array into a list, while cutting that value out of the array. This ensures that the array length is eventually equal to 1 and the recursion will eventually stop. It then calls the function again to check the array length. When the array length is eventually 1, the final list is returned. 

## Example in Debugger
For a more in depth look at this example in debugger, watch the following video.

{{< youtube QCtdGBBIwTM >}}