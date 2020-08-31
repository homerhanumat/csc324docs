---
title: "Group"
author: "Hunter Nosek"
date: 2020-08-31T14:08:17-04:00
draft: false
type: article
---

An article explaining my solution to the class Group from chapter 6.

<!--more-->

## The Problem

You can check out the problem here: https://eloquentjavascript.net/06_object.html

{{< rawhtml >}}
<blockquote>
The standard JavaScript environment provides another data structure called Set. Like an instance of Map, a set holds a collection of values. Unlike Map, it does not associate other values with those—it just tracks which values are part of the set. A value can be part of a set only once—adding it again doesn’t have any effect.

Write a class called Group (since Set is already taken). Like Set, it has add, delete, and has methods. Its constructor creates an empty group, add adds a value to the group (but only if it isn’t already a member), delete removes its argument from the group (if it was a member), and has returns a Boolean value indicating whether its argument is a member of the group.

Use the === operator, or something equivalent such as indexOf, to determine whether two values are the same.

Give the class a static from method that takes an iterable object as argument and creates a group that contains all the values produced by iterating over it.
</blockquote>
{{< /rawhtml >}}

## My Solution

Here is the full code to my solution:

```javascript
class Group {
     constructor() {
         this.content = [];
     }
     add(val){
         if (!this.content.includes(val)){
             this.content.push(val) 
         }
     }
     delete(val){ 
        if (this.content.includes(val)){ 
        this.content = this.content.filter(item => item !== val) 
        }
     }
     has(val) {
        return this.content.includes(val); 
      }
      static from(all) {
        let final = new Group;
        for (let i of all) {
          final.add(i); 
        }
        return final;
      }
 }
```
Here is the code that the textbook gives for us to try the function on:

```javascript
let group = Group.from([10, 20]);
console.log(group.has(10));
console.log(group.has(30));
group.add(10);
group.delete(10);
console.log(group.has(10));
```

I will go through each function in the class and explain how they work.

My first step in making this was to create the class notation, and fill it in with the functions that this problem requires. The first function is the constructor function, where we create the empty group. Here's a look at it:

```javascript
constructor() {
         this.content = [];
     }
```
This creates the empty group 'content' for the 'this' obhect. The reason we want this is so we can add, remove, and check values in it.

Next is the add function. Here's a look at my method of making it:

```javascript
add(val){
         if (!this.content.includes(val)){
             this.content.push(val) 
         }
     }
```

I start by making the only parameter 'val' since the only job the function is doing is adding a value in an array. The problem asks for this function to add values to the group if it isn't already a member, so checking to see if a value is part of the group is a huge part of the function. To do that, I use an if statement and the 'includes' method on 'content'. I take the complement of it, since I want to add a value if it's not in the array. If this if statement is true, then I use the 'push' method to push the value in 'content'.

Next is the delete function. Here's a look at how I created it:

```javascript
delete(val){ 
        if (this.content.includes(val)){ 
        this.content = this.content.filter(item => item !== val) 
        }
     }
```

Again, I start by making the only parameter 'val' since the only job the function is doing is deleting a value in an array. The problem asks for this function to remove the argument from the group if it's a member, so checking to see if it's a member is once again a huge part of the function. I do the same if statement as last time, except I'm not taking the complement since I want the function to remove it if it is part of the group. Inside of the if statement, I decided to use the 'filter' method on 'content' to remove the argument. I was able to do this by using a higher order function inside filter. The 'filter' method creates a new array that will be stored as 'content', without the argument. The 'item' function inside 'filter' will get rid of the argument by using the comparing every value in the array to the argument with !==.

Next is the has function. Here's a look at how I created it:

```javascript
has(val) {
        return this.content.includes(val); 
      }
```

This function is very simple. It will return a boolean TRUE or FALSE if 'content' includes the argument. I once again used the 'includes
 method on 'content', as I feel it is the clearest way to do it.

Lastly is the static from method. Here is a look at it:

```javascript
static from(all) {
        let final = new Group;
        for (let i of all) {
          final.add(i); 
        }
        return final;
      }
```
This will allow the user to create a new Group, and will add the values in the argument into the new Group. The function returns the new Group. The structure of this is very basic, as it is just a normal for loop that goes through an array and adds the values to a different object.

That's all of the explanations of the structure of my class.

I will now use the debugger to walkthrough what the machine does when it is given some of the trial code.

Consider:

```javascript
let group = Group.from([10, 20]);
```

When this is ran, it goes straight into the static function, where it creates a new Group called 'group'. It then goes through the loop in the static function, where it adds the values in the argument (10 and 20) to the new group. Each iteration in the for loop, when the call 'final.add(i)' is called, the machine goes into the class and checks out what to do in the 'add' function.

Now Consider the rest of the trial code:

```javascript
console.log(group.has(10));
console.log(group.has(30));
group.add(10);
group.delete(10);
console.log(group.has(10));
```

Since group is now created after the first trial code, each of these statements will work. These trial codes are pretty simple on what they do. For example, console.log(group.has(10)) will just return true, since the group has the value 10. The machine goes into the 'has' function in the class, checks if it has the value 10, and returns the boolean value 10. The other trial codes are work very similarly. group.add(10) and group.delete(10) don't return anything to the output, as they just go in the class and go through the 'add' and 'delete' functions.
