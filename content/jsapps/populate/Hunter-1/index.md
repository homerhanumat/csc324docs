---
title: "Populating a Table Article"
author: "Hunter Nosek"
date: 2020-09-10T20:50:07-04:00
draft: false
type: article
---

An article explaining my solution to the populating a table problem.

<!--more-->

## The Problem

You can check out the problem here: https://csc324docs.netlify.app/jsapps/populate/

{{< rawhtml >}}
<blockquote>
In this assignment you will use JavaScript in the browser to select a table and fill it with information obtained from an array of objects. You’ll get some practice with the DOM and with iteration.

In order to prepare for this exercise, read Chapters 13 and 14 of Eloquent JavaScript.

Note that the custom.js file defines an array called artists. Complete the file with code that locates the table on the index page and populates it with the information in artists.
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
  <script src="js/custom.js"></script>
</body>

</html>
```

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
```
I will slowly go through this so the reader will be able to understand what each function is doing.

We are given an array of 5 objects, each of which has a name, birthyear, and link. Because of this, we need to create 3 header cells. I started out by creating an array with the three names for the header cells:

```javascript
const names = ["Name", "Date of Birth", "Link"];
```
Now I needed to create a function that will create the header cells, and insert these names in the header cells. Here is a look at that function:

```javascript
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
```

First off, notice that this function has one parameter: `tbl`. `tbl` is the bhangra table on the index.html page. I was able to find it using `document.querySelector("#bhangra)`. I use the `createTHead()` to create the `<thead>` element in the table, which I call `Header`. Next, I go inside of `Header` to insert a row, which I call `Row`.

Now that I have a row inserted inside of the `<thead>` element, I can create the for loop that will go through my `names` array and make them into header cells. So first thing that happens inside the for loop is that I create a `<th>` element, which I call `head`. I also create a text node that includes the name that is in the ith place, and call that `text`. Now that I have everything I need ready to complete the header cell in the row, I use `appendChild` to put the text in the `<th>` element, then I use `appendChild` to put the `<th>` in the row. The for loop does this three times, successfully creating three header cells in the first row of my table.

Next comes the part where I have to populate the table with the artist information. Here is a look at my function that does that:

```javascript
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
```
Notice how this function has two parameters: `table` and `data`. `data` will just be the array of artists when I call the function. Since I need to add a row for each object in the array, I start this function out by creating a for loop that will go through each object of the array. I do this by saying `for (let each of data)`. For each iteration of this loop, I insert a row, calling it `row`. Now since I need to populate the row with the information of the artist, I create another for loop that will go through the object to get the name, birthyear, and link. I do this by saying `for (let i in each)`.

I start this for loop by inserting a `<td>` cell that I call `td`. I then create the text that comes from the ith piece of information inside the particular object, which I call `text`. I end this for loop by placing this text in the td cell. This happens three times for each object in the array.

This will go through each piece of information in each object, successfully populating the table with the 5 artists, with the names, birthyears, and links for all of them!

Here is a look at the final product:

![a table](bhangra.png)