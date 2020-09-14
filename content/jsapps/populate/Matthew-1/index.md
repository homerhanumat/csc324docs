---
title: "Populating a Table"
author: "Matthew Mills"
date: 2020-09-10T20:50:07-04:00
draft: false
type: article
---

An article explaining my solution to the populating a table problem.

<!--more-->

## The Problem

You can find the problem here: https://csc324docs.netlify.app/jsapps/populate/

{{< rawhtml >}}
<blockquote>
In this assignment you will use JavaScript in the browser to select a table and fill it with information obtained from an array of objects. You’ll get some practice with the DOM and with iteration.

In order to prepare for this exercise, read Chapters 13 and 14 of Eloquent JavaScript.

Note that the custom.js file defines an array called artists. Complete the file with code that locates the table on the index page and populates it with the information in artists.
</blockquote>
{{< /rawhtml >}}

Here is the my index.html solution file code:

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
        <tr>
          <th>Name</th>
          <th>Date Of Birth</th>
          <th>Link</th>
        </tr>
      </table>
    </section>
  </article>
  <script src="js/custom.js"></script>
</body>

</html>
```


Here is the my coustom.js solution file code:

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

 let tablefill = function(table, data) {
for(let element of data) {
let row = table.insertRow();
for (m in element) {
  let box = row.insertCell();
  let text = document.createTextNode(element[m]);
box.appendChild(text);
}
}
 }

 let table = document.querySelector("#bhangra");
 let data = Object.keys(artists[0]);
tablefill(table,artists);
```

i will go throgh this piece by piece 

``` javascript
let tablefill = function(table, data) {
for(let element of data) {
let row = table.insertRow();
```
this is creating a funtion that takes two input variables the headers and `table` and `data`. it is also assiging the correct number of rows for the data provided.

``` javascript
for (m in element) {
  let box = row.insertCell();
  let text = document.createTextNode(element[m]);
box.appendChild(text);
}
``` 
this `for` loop is what places the information into the corresponding cell on the table. the `appendChild` is what sticks the information in the next row/cell as it it creating a new element under the first element.

``` javascript
 let table = document.querySelector("#bhangra");
 let data = Object.keys(artists[0]);
tablefill(table,artists);
```
this chunk starts off with the variable table being assigned to `bhangra` within the `index.html` file. next we have data being told to start from the begining of the array provided. then the function is finally called to run. 

``` javascript
  <tr>
          <th>Name</th>
          <th>Date Of Birth</th>
          <th>Link</th>
        </tr>
```
this is in my `index.html` it is assiging the header names 

Here is what the final table looks like when produced into a website.
![a table](bhangra.png)

