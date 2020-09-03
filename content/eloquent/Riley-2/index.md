---
title: "Flatening"
author: "Riley Noe"
date: 2020-09-03T12:11:15-04:00
draft: false
type: article
---

<h4> Eloquent Javascript Ch 5</h4>

[click here to view the chapter](https://eloquentjavascript.net/05_higher_order.html/) 

<blockquote>

 Use the reduce method in combination with the concat method to "flatten"an array 
 of arrays into a single array that has all the elements of the original arrays.

For example,

```javascript
let exampleArray = [[1,2,3],[4,5,6],7];

console.log(flat(exampleArray));

```

The solution should return:

```javascript
[1,2,3,4,5,6,7];
```

</blockquote>

*The solution outlined in this problem was created by developer, Paul Ryan. You can see how he explained his answer [at this link](https://alligator.io/js/finally-understand-reduce/).*


<!--more-->

**My Code**

```javascript
debugger;
function flat(array){

    const initialValue = [];

    return array.reduce((total, value) => {
            
        return total.concat(Array.isArray(value) ? flat(value) : value);

    }, initialValue);
}

let arr = [[1,2,3], [4,5], [6]];

console.log(flat(arr));
```

**Explaination**


The function `flat()` takes a parameter *array*. For the sake of this problem, *array* is equal to an array
that has other arrays as elements. The first line creates an empty array *initialValue*, which will be used later. 

In the next line, we see the *reduce* method used on *array*. The *reduce* method will run a set function on every element in an array. In this situation, I take *array* and use *reduce* to run a ternary operator through every element, starting at *initialValue*. The parameters *total* and *value* are determined by the elements inside *array*. The ternary operator is used to determine if the element *value* is an array, if so the code runs `flat(value)` as a recursive function. This function then "zooms" in on the sub array to examine its elements. If any of those elements are also an array, the recursive function will run again, until *value* is set to an element that is not another array. If *value* is not an array, the ternary operator will *concat* *value* into *total* as a new element. Once every element in *array* has been added to *total* the function will return *total*.



Debugger example: 

If you run the code above and enter the debugger, the process will begin at the function declaration. Enter into the function, the empty array *initialValue* is created. Step forward, the next line is the *reduce* method outlined above. It includes the variables *total* and *value*, the command line, and the starting place set by *initialValue*. If you step into this line, *total* will equal the empty array *initialValue*, and *value* equals the first element in *array*, i,e, [1,2,3]. Step forward again and you will enter the ternary operator. The ternary operator uses condition `Array.isArray(value)` to determine if *value* is an array. Since *value* equals the array [1,2,3] and, thus, the condition is true, the ternary operator will run the recursive function `flat(value)`. This time the parameter *array* is set equal to [1,2,3], thus when the debugger steps into the *reduce* method, *total* will still equal the empty array *initialValue*, but *value* will equal the first element of the first element of *arr*, or [1]. As [1] is not an array, the ternary condition will be false and *value* will *concat* into *total*. 

The *reduce* method then restarts with *total* equal to [1] and *value* equal to [2]. As [2] is not an array, the ternary condition will be false and *value* will *concat* into *total*. The 3rd element inside the first element of *arr* is [3]. When the *reduce* method restarts a third time, *total* is equal to [1,2] and *value* is equal to [3]. As [3] is not an array, the ternary operator will *concat* *value* into *total*. 

After all elements in the first element of *arr* have been "flattened" into *total*, the *reduce* method jumps to the second element of *arr*, i.e. [4,5]. The variable *total* is equal to [1,2,3] and *value* is equal to [4,5]. As [4,5] is an array, the ternary condition is true and the code will enter into another recursive function. *total* still equals [1,2,3] and *value* now equals [4], or the first element in the second element of *arr*. Because [4] is not an array, *value* is *concat* into *total*. This result occurs again for the next element considered, [5], because it is also not an array. 

Once the second element of *arr* has been flattened into *total*, the *reduce* method enters into the third element of *arr*, [6]. At this time, *total* equals [1,2,3,4,5] and *value* equals [6]. Since *value* is not an array, the ternary condition is false and [6] will *concat* into *total*. 

With all of *arr* flattened into *total*, *total* is then returned to the *reduce* method, which also returns *total* to the output window. 

Thus, our answer is;
```javascript
[1,2,3,4,5,6]
```




