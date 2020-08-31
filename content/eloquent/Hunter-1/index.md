---
title: "Hunter Javascript Article #1"
author: "Hunter Nosek"
date: 2020-08-29T13:04:55-04:00
draft: false
type: article
---

An article explaining my solution to the function ArrayToList() from chapter 4.

<!--more-->

## The Problem

You can check out the problem here: https://eloquentjavascript.net/04_data.html
{{< rawhtml >}}
<blockquote>
Objects, as generic blobs of values, can be used to build all sorts of data structures. A common data structure is the list (not to be confused with array). A list is a nested set of objects, with the first object holding a reference to the second, the second to the third, and so on.

Write a function arrayToList that builds up a list structure like the one shown when given [10, 20] as argument.
</blockquote>
{{< /rawhtml >}}

```{javascript}
{value: 10, rest: {value: 20, rest: null}}
```
## My Solution

Here is the full code to my solution:

```{javascript}
 function arrayToList(arr) {
     final = null;
     for (i = (arr.length -1); i >= 0; i--) {
        final = {value: arr[i], rest : final};
     }
     return final;
 }
```
Here is the code that the textbook gives for us to try the function on:

```{javascript}
console.log(arrayToList([10, 20]))
```

I will use the debugger to help myself explain how the code works.

The function starts out by setting a variable called 'final' to null, which is what will eventually get returned at the end of the for loop. We want it to be null so we can create the list structure in it. Notice that I didn't put 'let' or 'var' in front of it, so it will be in the global environment.

The function then goes into a loop. Here's another look at the parameters of it:

```{javascript}
for (i = (arr.length -1); i >= 0; i--)
```
The index variable is set to the end of the array, and it will go backwards until the index variable hits zero, where it will go through one last time.

Here's the code that is in the loop, that creates the desired list structure:

```{javascript}
final = {value: arr[i], rest : final};
```
This is where we start setting final equal to the list structure. We use the curly braces so it is an object. In the first part of the object, we set value equal to the value in the array that we give the function in the ith place. Since the for loop is going backwards, the value will be the last one in the array. In the second part of the object, we set rest equal to final. Since final is known as null in the global environment at this point in time, rest will be equal to null.

So after going through the loop one time, this is what final is equal to in the global environment:

```{javascript}
{value: 20, rest : null}
```

Since the array we gave it only has two elements, the for loop will run its code one more time.

This time, it will run the exact same code as the first time. Final will be set equal to the object that contains value and rest. Value will be the first array value instead of the second. Rest will be equal to what final currently is in the global environment, which is still {value: 20, rest : null} from the first go around. 

This is what final is equal to in the global environment after the second time going through the for loop:

```{javascript}
{value: 10, rest: {value: 20, rest : null}}
```

Since we have gone through all of the array values, the for loop will stop and final is returned.






