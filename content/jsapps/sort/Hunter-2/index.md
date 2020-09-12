---
title: "Sorting a Table Article"
author: "Hunter Nosek"
date: 2020-09-11T19:40:04-04:00
draft: false
type: article
---

An article explaining my solution to the sorting a table problem.

<!--more-->

## The Problem

You can check out the problem here: https://csc324docs.netlify.app/jsapps/sort/

{{< rawhtml >}}
<blockquote>
In this assignment you add some buttons to the table you created and populated in the previous assignment. You will practice handling events in JavaScript.

In order to prepare for this exercise, read Chapter 15 of Eloquent JavaScript.

Starting from the site that populates a table of Bhangra artists, add three buttons:

A button that when clicked will sort the artists by name.
A button that when clicked will sort the artists by year of birth.
A button that when clicked will randomly shuffle the rows of the original table.
</blockquote>
{{< /rawhtml >}}

## My Solution

Below is the full code to my solution. 

Here is the index.html file code:

```javascript
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en-us">

<head>
  <title>CSC 324 | Table Assignment</title>
  <meta http-equiv="content-type" content="text/html; charset=utf-8">
  <!-- Enable responsiveness on mobile devices-->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Table assignment for CSC 324 at Georgetown College, Kentucky.">
  <meta name="keywords" content="computer science web javascript">
  <!-- styles -->
  <link rel="stylesheet" href="css/tufte.css">
</head>

<body>
  <article>
    <h1>My Favorite Bhangra Artists</h1>
    <section>
      <p>
        The following table gives a list of great Bhangra 
        musicians.  Enjoy!
      </p>
      <table id="bhangra">
      </table>
    </section>
  </article>
  <div id="buttons">
    <button id="alpha-button">Sort Alphabetically</button>
    <button id="year-button">Sort By Age</button>
    <button id="random-button">Randomize</button>
  </div>
  <script src="js/custom.js"></script>
</body>

</html>
```

You can see the difference with this index.html compared to the index.html on my populating a table assignment is that I had to add three buttons. `alpha-button` for the alphabetically sorting, `year-button` for the birthdate sorting, and `random-button` for randomizing the table.

Here is the custom.js file code:

```javascript
const artists = [
   {
     name: "Ms Scandalous",
     birthYear: 1985,
     link: "https://www.youtube.com/watch?v=2FPivlfvxu0"
   },
   {
    name: "Juggy D",
    birthYear: 1981,
    link: "https://www.youtube.com/watch?v=1jAc_-FVjdI"
  },
  {
    name: "Sukhbir Singh",
    birthYear: 1969,
    link: "https://www.youtube.com/watch?v=HiprNF9Jad0"
  },
  {
    name: "Abrar-ul-Haq",
    birthYear: 1989,
    link: "https://www.youtube.com/watch?v=-lnnVIP7FEc"
  },
  {
    name: "Rishi Rich",
    birthYear: 1970,
    link: "https://www.youtube.com/watch?v=O95-w2gACuA"
  }
 ]

 debugger;
 const names = ["Name", "Date of Birth", "Link"]; 

 function table_head(tbl) {          
   let Header = tbl.createTHead(); 
   let Row = Header.insertRow(); 
   for (let i of names) {
   let head = document.createElement("th"); 
   let text = document.createTextNode(i);
   head.appendChild(text);
   Row.appendChild(head)
   }
 } 

let table = document.querySelector("#bhangra"); 
table_head(table);

 function table_populate(table, data) {  
  for (let each of data) {
    let row = table.insertRow();
    for (let i in each) {
      let td = row.insertCell();
      let text = document.createTextNode(each[i]);
      td.appendChild(text);
    }
  }
}
table_populate(table, artists);

function delete_table(table) {
  for (let i = 0; i < artists.length; i++) {
    table.deleteRow(1);
  }
} 

function byName(a, b) {
  if (a.name < b.name) return -1;
  if (a.name > b.name) return 1;
  return 0;
 }


 function showAlphaArtist() {
   const AlphaArtists = artists.sort(byName);
   delete_table(table);
   table_populate(table, AlphaArtists);
 } 

const AlphaButton = document.querySelector("#alpha-button"); 
AlphaButton.addEventListener("click", showAlphaArtist);

function byYear(a, b) {
  if (a.birthYear < b.birthYear) return -1;
  if (a.birthYear > b.birthYear) return 1;
  return 0;
}

function showYearArtist() {
  const YearArtists = artists.sort(byYear);
  delete_table(table);
  table_populate(table, YearArtists);
} 

const YearButton = document.querySelector("#year-button");
YearButton.addEventListener("click", showYearArtist);

Array.prototype.shuffle = function() {
  let input = this;
  for (let i = input.length-1; i >= 0; i--) {
    let randomIndex = Math.floor(Math.random()*(i+1)); 
    let itemAtIndex = input[randomIndex]; 
    input[randomIndex] = input[i]; 
    input[i] = itemAtIndex;
  }
 return input;
};


function showRandomArtist() {
     delete_table(table);
     const randomArtists = artists.shuffle();
     table_populate(table, randomArtists);
   } 

const randomButton = document.querySelector("#random-button");
randomButton.addEventListener("click", showRandomArtist);
```

You'll see that I have still have the code from my populating a table solution, I'm just adding on the functions needed to make the buttons do their job.

The first new function you see is `delete_table`. Here's a closer look at it:

```javascript
function delete_table(table) {
  for (let i = 0; i < artists.length; i++) {
    table.deleteRow(1);
  }
} 
```

This function will be mentioned a couple of times later, but the function is designed to remove the five rows of artists in the table everytime I press a button. I need it because I call the `table_populate` function everytime a button is pressed, which just adds on five rows of the given information. If I didn't have this `delete_table` function, then five rows will just be added on everytime a button is pressed.

You'll notice that there is a for loop. This will run through the length of artists, so five times. This line is called inside:
`table.deleteRow(1);` Notice how I have it deleting the row of index 1 and not 0. This is because the row with index 0 is the row that contains the headers, which I don't want to touch. Since it deletes the row in index 1, and the function goes through the function 5 times, the row in index 1 will be deleted 5 times. This means that when a row is deleted, the rows with an index above it move back. The function successfully deletes the 5 rows while not touching the row with the headers!

Here is the code that makes the button that sorts by name work:

```javascript
function byName(a, b) {
  if (a.name < b.name) return -1;
  if (a.name > b.name) return 1;
  return 0;
 }


 function showAlphaArtist() {
   const AlphaArtists = artists.sort(byName);
   delete_table(table);
   table_populate(table, AlphaArtists);
 } 

const AlphaButton = document.querySelector("#alpha-button"); 
AlphaButton.addEventListener("click", showAlphaArtist);
```

The function `byName` receives two parameters, and is designed to be used inside the `sort` function. `byName` will check if the first parameter is less than or greater than the second parameter. By doing this, it checks if the letter in the first index of the first name is above or below the letter in the first index of the second name. If the first name is alphabetically behind the second, then the function will return a -1, which will ending up switching them when `byName` is called in `sort`.

Now let's look at the function `showAlphaArtist`. We are creating a new array called `AlphaArtists`, which will be equal to `artists.sort(byName)`. Knowing what the `byName` function does, the artist array will be sorted using `byname`. All of the objects will make its way through `byName` which will organize it alphabetically. So `AlphaArtists` will be the array that contains the artists in alphabetical order. The next line that is called is `delete_table(table)`, which deletes the previous table's 5 rows. Next, we populate the now empty table with the `AlphaArtists` array.

The last two lines in this chuck of code selects the `alpha-button` from the index.html file, and adds the event of running the `showAlphaArtist` function when the button is clicked. The "sort alphabetically" is now ready to be used!

The code that makes the button sort by year is extremely similar:

```javascript
function byYear(a, b) {
  if (a.birthYear < b.birthYear) return -1;
  if (a.birthYear > b.birthYear) return 1;
  return 0;
}

function showYearArtist() {
  const YearArtists = artists.sort(byYear);
  delete_table(table);
  table_populate(table, YearArtists);
} 

const YearButton = document.querySelector("#year-button");
YearButton.addEventListener("click", showYearArtist);
```

The only difference in this code is that the `byYear` function differs from the `byName` function simply by comparing the years, instead of the names. Everything else is the same, and the button works successfully.

Here is the code for the button that randomizes the table:

```javascript
Array.prototype.shuffle = function() {
  let input = this;
  for (let i = input.length-1; i >= 0; i--) {
    let randomIndex = Math.floor(Math.random()*(i+1)); 
    let itemAtIndex = input[randomIndex]; 
    input[randomIndex] = input[i]; 
    input[i] = itemAtIndex;
  }
 return input;
};


function showRandomArtist() {
     delete_table(table);
     const randomArtists = artists.shuffle();
     table_populate(table, randomArtists);
   } 

const randomButton = document.querySelector("#random-button");
randomButton.addEventListener("click", showRandomArtist);
```

I got the code for shuffling an array from this link: https://www.kirupa.com/html5/shuffling_array_js.htm
Please read this to understand how it works! It has graphics and does a very good job explaining it. Everything else is once again the same, except the array that is created inside the `showRandomArtist` is shuffled and not sorted.

Hopefully you got a good grasp of the ideas I used. I tried to only go off of what I had for my populating a table problem, which was somewhat difficult (having to fail and learn to delete rows everytime) but very satisfying!


