---
title: "Sorting a Table"
author: "Kaitlyn Brewer"
date: 2020-09-14T20:47:45-04:00
draft: false
type: article
---

This will be one solution for the sorting a table assignment.

<!--more-->
## Disclaimer
I will only include the code that I added to custom.js for this assignment. The original code can be found on the [assignment page](https://csc324docs.netlify.app/jsapps/populate/) and the code that I added to populate the inital table [here](https://csc324docs.netlify.app/jsapps/populate/kaitlyn-3/).

## The Problem
Add three buttons to the populate a table assignment that:
* Sort the artists by name
* Sort the artists by birth year
* Randomly shuffle teh artists

## The Solution
Here is my solution code:
```{javascript}
function deleteTable(table) {
  for (let i = 0; i < artists.length; i++) {
    table.deleteRow(1);
  }
}

function byName(a, b) {
  if (a.name == b.name) return 0;
  if (a.name < b.name) return -1;
  return 1;
 }
 function sortName() {
   let artistName = artists.sort(byName);
   deleteTable(table);
   populate(table, artistName);
 } 
let nameButton = document.querySelector("#name-button"); 
nameButton.addEventListener("click", sortName);


function byYear(a, b) {
  if(a.birthYear == b.birthYear) return 0;
  if (a.birthYear < b.birthYear) return -1;
  return 1;
}
function sortYear() {
  let artistYear = artists.sort(byYear);
  deleteTable(table);
  populate(table, artistYear);
}
let yearButton = document.querySelector("#year-button");
yearButton.addEventListener("click", sortYear)


Array.prototype.shuffle = function() {
  let input = this; 
  for (let i = input.length - 1; i >= 0; i--) {
    let randomIndex = Math.floor(Math.random()*(i+1));
    let itemAtIndex = input[randomIndex];
    input[randomIndex] = input[i];
    input[i] = itemAtIndex;
  }
  return input;
}
function randomShuffle() {
  deleteTable(table);
  let randomize = artists.shuffle();
  populate(table, randomize);
}
let randomButton = document.querySelector("#random-button");
randomButton.addEventListener("click", randomShuffle);
```
First, we should look at the `deleteTable` function.
```{javascript}
function deleteTable(table) {
  for (let i = 0; i < artists.length; i++) {
    table.deleteRow(1);
  }
}
```
Because we use the `populate` function to recreate the table with each button, this `deleteTable` function removes the original, unsorted rows before adding the new. sorted rows. For every row of the table, the entire row is removed. We will use this in our other functions. Without this, the table has the five rows for the original, unosrted table, and with each button, adds five additional rows with the artists sorted or shuffled (depending on what button is pushed). This function ensures that the table has only the five rows that we being requested by the button push. 

Now, let's look at the mechanics for each button. 

```{javascript}
function byName(a, b) {
  if (a.name == b.name) return 0;
  if (a.name < b.name) return -1;
  return 1;
 }
 function sortName() {
   let artistName = artists.sort(byName);
   deleteTable(table);
   populate(table, artistName);
 } 
let nameButton = document.querySelector("#name-button"); 
nameButton.addEventListener("click", sortName);
```
The `byName` function will compare the names of two artists and will move them in relation to each other within the table. If `a.name == b.name`, a 0 will be returned and no change will be made. If `a.name < b.name`, a -1 will be returned the the `a.name` will be moved below the `b.name` when put into the `artists.sort` of the `sortName` function. Within the `sortName` function, the names are sorted as defined in`byName`, the original table is deleted, and a new table is populated based on the sorted names of the artists. The `nameButton` searches for the ID of `#name-button` in the `index.html`. The last line says that when the button is clicked, that's when `sortName` is actually called. 

```{javascript}
function byYear(a, b) {
  if(a.birthYear == b.birthYear) return 0;
  if (a.birthYear < b.birthYear) return -1;
  return 1;
}
function sortYear() {
  let artistYear = artists.sort(byYear);
  deleteTable(table);
  populate(table, artistYear);
}
let yearButton = document.querySelector("#year-button");
yearButton.addEventListener("click", sortYear)
```
Here, I used the exact same approach as with the sorting by names, but just changed the parameters to be based on the `birthYear` of the artists, rather than the `name`. 

```{javascript}
Array.prototype.shuffle = function() {
  let input = this; 
  for (let i = input.length - 1; i >= 0; i--) {
    let randomIndex = Math.floor(Math.random()*(i+1));
    let itemAtIndex = input[randomIndex];
    input[randomIndex] = input[i];
    input[i] = itemAtIndex;
  }
  return input;
}
function randomShuffle() {
  deleteTable(table);
  let randomize = artists.shuffle();
  populate(table, randomize);
}
let randomButton = document.querySelector("#random-button");
randomButton.addEventListener("click", randomShuffle);
```
The first section here is creating a `shuffle` method for an array. This method essentially switches the positions of random elements in the array. A more in depth look at this method can be found [here](https://www.kirupa.com/html5/shuffling_array_js.htm). This is the original creation of the method and was also referenced by Dr. White in class. From that point, the `randomShuffle` function removes the original table, then randomizes the array of artists, and repopulates the table. The rest works the same as before, finding the `#random-button` ID in the `index.html` and noting that a click to that button should be the call to the `randomShuffle` function. 