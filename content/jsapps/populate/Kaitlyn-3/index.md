---
title: "Populating a Table"
author: "Kaitlyn Brewer"
date: 2020-09-11T20:35:00-04:00
draft: false
type: article
---

This will be one solution for the populating a table assignment. 

<!--more-->
## Disclaimer
I will only include the code that I added into `custom.js`, but all of the original code and the index.html can be found on the [assignment page](https://csc324docs.netlify.app/jsapps/populate/) of this webiste. 

## The Problem
Use Javascript in the browser to populate a table with information from `artists`, a given array of objects. 

## The Solution 
Here is the code that I added to `custom.js`:

```{javascript}
 function populate(table, data) {
  for(let element of data) {
    let row = table.insertRow();
    for(let i in element) {
      let cell = row.insertCell();
      let text = document.createTextNode(element[i]);
      cell.appendChild(text);
    }
  }
}

let titles = ["Name", "Date of Birth", "Link"]

function tableHead(table) {
  let head = table.createTHead();
  let row = head.insertRow();
  for (let n of titles) {
    let th = document.createElement("th");
    let text = document.createTextNode(n);
    th.appendChild(text);
    row.appendChild(th);
  }
}
let table = document.querySelector("#bhangra");
populate(table, artists);
tableHead(table);
```
>Note thay `custom.js` also has an array of five artists with their names, birth years, and a link to a YouTube video of one of their songs. This array is called `artists`. 

Let's discuss the different functions.

```{javascript}
function populate(table, data) {
  for(let element of data) {
    let row = table.insertRow();
    for(let i in element) {
      let cell = row.insertCell();
      let text = document.createTextNode(element[i]);
      cell.appendChild(text);
    }
  }
}
```
This function is responsible for forming the shell of the table. Later, the call to this function will fill in this shell. For every element in a given array, a new row will be added. For every row that is added, a new cell and text node will be created for each key of the object. The `appendChild(text)` will add the text to the cell. 

```{javascript}
let titles = ["Name", "Date of Birth", "Link"]

function tableHead(table) {
  let head = table.createTHead();
  let row = head.insertRow();
  for (let n of titles) {
    let th = document.createElement("th");
    let text = document.createTextNode(n);
    th.appendChild(text);
    row.appendChild(th);
  }
}
```
The array called `titles` will be used in the creation of the table header.

In this function, first the space for the header is created, setting it aside from the actual contents of the table. Then, a row is inserted for the titles. For every element in `titles`, it is tied to a `<th>` html tag and the text from `titles` is added into that tag. 

```{javascript}
let table = document.querySelector("#bhangra");
populate(table, artists);
tableHead(table);
```
Here, the table is being inserted into a particular spot in the index.html. Specifically, it is being inserted where there is the ID marker `#bhangra`.
There are also the function calls to `populate` and `tableHead`, where in `table` is the space defined by the `#bhangra` ID and `artists` is the array provided in the beginning of `custom.js`. Here is what the final product should look like. 

![a table](bhangra.png)


