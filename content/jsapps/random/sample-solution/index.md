---
title: "Sample Solution"
author: "Homer White"
date: 2020-07-01T18:01:32-04:00
draft: false
type: article
---

My solution uses regular expressions and `window.addEventListener()`.

<!--more-->

## Overview

The embed code needs to appear in the following div:

{{<  highlight html >}}
<!-- from index.html -->

<div id="bhangra">
  <!-- embed code will go here -->
</div>
{{< / highlight>}}

The `artists` array is an array of objects, one for each artist:

{{<  highlight javascript >}}
// from js/custom.js

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
{{< / highlight >}}

We can access any of the URLs like this:

{{< highlight javascript >}}
artists[3].link
// --> Sukbhir Singh's link:  https://www.youtube.com/watch?v=HiprNF9Jad0
{{< / highlight >}}

From the [YouTube documentation](https://support.google.com/youtube/answer/171780?hl=en), we find that some possible embed code for our video would be as folllows:

{{<  highlight html >}}
<iframe width="560" height="315" src="https://www.youtube.com/embed/HiprNF9Jad0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
{{< / highlight>}}

Studying the embed-code, we see that the crucial information is the ID of the video:  `HiprNF9Jad0`, which is the text that occurs after `"watch?v="` in the link for Sukbhir Singh.

This insight gives rise to the following plan:

1. Initialize an array (callled perhaps `ids`) and fill it with the IDs of the videos.
2. Set up an event-listener that, on the `load` event, will:
    * pick an integer at random from 0 to 4 (one less than the length of `ids`);
    * recover the id at the above random location in `ids`
    * use the id to construct a string representing the embed-code;
    * make this string the inner-HTML of the `bhangra` div.

## Implementing Our Plan

First we initialize the `ids` array and then we populate it:

{{< highlight javascript >}}
// this will hold the ids:
 let ids = [];

 // from artists, strip the id from each video link and
 // push to ids
 function getID(artist) {
   const link = new String(artist.link);
   const pattern = /watch\?v=(.*)$/
   const match = pattern.exec(link);
   ids.push(match[1]);
 }
{{< / highlight >}}

The key tool in the above code is the regular expression `/watch\?v=(.*)$/`, which captures the text `"watch\?v="` until the end of the URL.  This is the ID of the video!

Next we set up our event-listener:

{{< highlight javascript >}}
const iframe = document.querySelector("#bhangra");

function deliverVideo() {
  const randomNumber = Math.floor(ids.length * Math.random());
  const randomID = ids[randomNumber];
  const bhangraDiv = document.querySelector("#bhangra");
  const src = "https://www.youtube.com/embed/" + randomID;
  let embed = '<iframe id="bhangra" width="560" height="315" src=';
  embed = embed + src + ' frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; ';
  embed = embed + 'picture-in-picture" allowfullscreen></iframe>';
  bhangraDiv.innerHTML = embed;
}

window.addEventListener("load", deliverVideo);
{{< / highlight >}}

Note how:

* `Math.random()` returns a pseudorandom real number between 0 and 1;
* `ids.length * Math.random()` therefore evaluates to a random real number between 0 and 5;
* hence `Math.floor(ids.length * Math.random())` evaluates to a random _whole_ number from 0 to 4.

## Code

{{< rawhtml >}}<a href="random-content-sol.zip" download>This zip-file</a>{{< /rawhtml >}} contains `index.html` and all supporting files.  download and extract to see the full solutions.  A live version can be seen at [http://random-content-sol.surge.sh](http://random-content-sol.surge.sh).