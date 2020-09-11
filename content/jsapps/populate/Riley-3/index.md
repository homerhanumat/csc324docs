---
title: "Building a Table - Riley"
author: "Riley Noe"
date: 2020-09-11T12:30:31-04:00
draft: true
type: article
---


<blockquote>

In this assignment you will use JavaScript in the browser to select a table and fill it with information obtained from an array of objects. Specifically, we were asked to instert the given array `artists`, into a table, then inteset that table into an html document that can be generated online. We were also given a, an unedited html document and a css file. The solution should look like the table below.

{{< rawhtml >}}
<img src="table.png" class="center"> 
{{< /rawhtml >}}
</blockquote>

*Note:* The array `artists` is located in the file js/custom.js and has five elements. Each element has three properties: name, birthYear and link. This is found in the custom.js document and seen below.

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
 ];
```
<!--more-->

**The HTML**

Before we can put this information into a table, we must make sure that the index.HTML document has a place to put the table. 

```javascript
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
From this HTML chunk, we can see a `<body>` tag followed by an `<article>` tag. The heading of this article is "My Favorite Bhangra Artists," listed inside the `<h1></h1>` tags. The `<section>` tag contains the main content of the article, which is split into a short description and the actual table itself. The description is "The following table gives a list of great Bhangra musicians. Enjoy!" deonted by the `<p></p>` tags. You may notice that there is a `<table id="bhangra"></table>` tag, but no table. This will be further discussed below, for now it is important to know that the tag id is used to get the data from another document. The empty `</table>` tag is followed by `</section></article>` tags to close of the content of the article. 

Still inside the `<body>` tag, however, a `<script src="js/custom.js"></script>` tag is used to signal which documents to pair to. We can see that the source file, src, is set to the file path js/custom.js. Thus, whenever index.html is run, the code will consult the src document, in this case custom.js.


**THE JAVASCRIPT**

The following is a code chunck from the file mentioned above, js/custom.js. 

```javascript
const listDiv = document.querySelector("#bhangra");
 
let contents = "";
contents += "<tr><th>Name</th><th>Year</th><th>Link</th><tr>";
artists.forEach(function(artist) {
  contents = contents + `<tr><td>${artist.name}</td><td>${artist.birthYear}</td><td>${artist.link}</td></tr>`;
})

listDiv.innerHTML = contents;
```
Before I begin, it is important to note that this document is not meant to run independent of the index.HTML file mentioned above. If you run it the code by itself, nothing will console.log() because it's not supposed to. 

Inside this chunk, we see `const listDiv = document.querySelector("#bhangra");`. The const variable `listDiv` is now set equal to a document query selector targeting an html tag with an id set to "bhangra". Since the two documents are connected through the `<script src="js/custom.js"></script>` tag, when the index.html consults custom.js `listDiv` will enter into index.html and search for the tag id "bhangra". At the moment nothing happens becasue there isnt a command attached to `listDiv`.

In the next line, the variable `contents` is created and set to an empty string. This variable will be used to hold the data for our table. 

`contents += "<tr><th>Name</th><th>Year</th><th>Link</th><tr>";`  

If you notice, `contents` is added to an html string. The `<tr></tr>` creates a table row, and the `<th></th>` tag creates a table header. The inserted string is going to be the header row of our table. By using a string variable javascript doesn't get confused with the html. This is why the html string is only added once - because a table only needs one header. 

Below the header, we see `artists.forEach(function(artist) {`. This command takes the array `artists` and implements the forEach method with a function and it's parameter `artist`. This means that every element of `artists` will be set equal to the function paramter `artist`.

Inside this command, `contents = contents + '<tr><td>${artist.name}</td><td>${artist.birthYear}</td><td>${artist.link}</td></tr>';})`, we see that `contents` is set equal to itself + more html code. This code creates a new row in the table using `<tr></tr>`, and puts data inside the row using the table data tag `<td></td>`. Any code inside the "${}" is javascript, which means that `artist.name` inserts the property name for the current element into the table as data. Thus, each artist will have their own row in the table. 

Lastly, we see `listDiv.innerHTML = contents;`, which sets our new table (the html string) equal to the queryselector `listDiv` and it's property `innerHTML`. This means that the html string is will be entered into the index.html. Specifically, it enters into the tag with the id = "bhangra". 

