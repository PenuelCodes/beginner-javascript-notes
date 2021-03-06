---
attachments: [619.png, 620.png, 621.png, 622.png, 623.png, 624.png, 625.png, 626.png, 627.png, 628.png, 629.png, 630.png, 631.png, 632.png, 633.png, 634.png, 635.png, 636.png, 637.png, 638.png, 639.png, 640.png, 641.png, 642.png, 643.png, 644.png, 645.png, 646.png, 647.png, 648.png, 649.png, 650.png, 651.png, 652.png, 653.png, 654.png, 655.png, 656.png, 657.png, 658.png, 659.png, 660.png, 661.png, 662.png, 663.png, 664.png, 665.png, 666.png, 667.png, 668.png, 669.png, 670.png, 671.png, 672.png, 673.png, 674.png, 675.png, 676.png, 677.png, 678.png, 679.png, 680.png, 681.png, 682.png, 683.png, 684.png, 685.png, 686.png, 687.png, 688.png, 689.png, 690.png, 691.png, 692.png, 693.png, 694.png, 695.png, 696.png, 697.png, 698.png, 699.png, 700.png, 701.png, 702.png, 703.png, 704.png, 705.png, 706.png, 707.png, 708.png, 709.png, 710.png, 711.png, 712.png, 713.png, 714.png, 715.png, 716.png, 717.png, 718.png, 719.png, 720.png, 721.png, 722.png, 723.png, 724.png, 725.png, 726.png, 727.png, 728.png, 729.png, 730.png, 1470.png, 1471.png, 1472.png, 1473.png]
title: 'Module 9: Gettin'' Loopy'
created: '2020-04-13T22:24:51.247Z'
modified: '2020-08-20T11:51:56.686Z'
---

- [Module 9: Gettin' Loopy](#module-9--gettin--loopy)
  * [49 Looping and Iterating - Array .forEach](#49-looping-and-iterating---array-foreach)
  * [50 - Looping and Iterating - Mapping](#50---looping-and-iterating---mapping)
  * [51 - Looping and Iterating = Filter, Find and Higher Order Functions](#51---looping-and-iterating---filter--find-and-higher-order-functions)
  * [52 - Looping and Iterating - Reduce](#52---looping-and-iterating---reduce)
  * [53 - Looping and Iterating - Reduce Exercise](#53---looping-and-iterating---reduce-exercise)
    + [Regular Expression](#regular-expression)
  * [54 - Looping and Iterating - for, for in, for of, and while Loops](#54---looping-and-iterating---for--for-in--for-of--and-while-loops)
    + [The for loop](#the-for-loop)
      - [for of Loop](#for-of-loop)
    + [`for of` loop](#-for-of--loop)
    + [`for in` loop](#-for-in--loop)
    + [`while` and `do while` loops](#-while--and--do-while--loops)

---

# Module 9: Gettin' Loopy

## 49 Looping and Iterating - Array .forEach

Let's talk about looping and iterating. There are a few different ways to loop in Javascript and we will cover them all.

The most common way you are going to loop over something in javascript is looping over an array. Most of the looping also works the exact same way. 

We will use a method that lives on the array, and we will pass it a callback, just like in the previous video. 

The callback function will run once for every item in the array, giving us access to each individual item.

Open up the `array-looping-methods-START.html` file, which contains all the practice data we will be using for these exercises. Most of it is the same as the last video with the addition of a `students` array.

```js
const toppings = ['Mushrooms ', 'Tomatoes', 'Eggs', 'Chili', 'Lettuce', 'Avocado', 'Chiles', 'Bacon', 'Pickles', 'Onions', 'Cheese'];
```

If you wanted to loop out over every single one of the toppings in the array and log them to the console, or display them to the user, the very basic loop we have is the `.forEach()`. 

You should recognize it from previous exercises we did, when we were adding event listeners to multiple elements.

What we are going to do is take `toppings` and use the `forEach` method on it, passing it a callback function that will run once for each item in the array. 

We can define our function outside or inline. 

```js
function logTopping(topping){
  console.log(topping);
}
toppings.forEach(logTopping)
```

![](../attachments/619.png) 10:06

If you refresh the page, you will see that we are logging every single one of the toppings as we loop over them. 

One thing Wes likes to do is throw a debugger into the foreach and take a look at the dev tools. 

Modify the code as shown below to add the debugger breakpoint 👇

```
function logTopping(topping){
  console.log(topping);
  debugger;
}
```

When you refresh the HTML page, the debugger should open once it hits the first item in the array. 

![](../attachments/620.png) 9:52

As you can see, the debugger is in paused state. We have access to the call stack, and it tells us we are in the function `logTopping`. 

Below that, the debugger tells us what the `topping` variable is equal to which is "Mushrooms", as well as the value of the `this` variable, which is equal to the Window.

![](../attachments/621.png) 9:24 

If you click the symbol shown in the image above twice, the javascript code will continue running.  

Now we are on the "Tomatoes" item. You can click all the way through the array. 

As you know, we can also inline the function as shown below and it will still work exactly the same 👇

```js
toppings.forEach(topping => {
  console.log(topping);
})
```

One thing you might be having trouble with is where is this `topping` variable shown highlighted below is coming from. You may be wondering if it's a special keyword because it is a singular of toppings which is the name of the variable that holds the `toppings` array. 

![](../attachments/622.png) 8:25

If you remember back to when we learned about arguments and placeholders we said that arguments were the actual values and the parameters were the placeholders.

When we define the function, we put a placeholder, a **parameter** in there, and then when the `forEach` loop is called, Javascript will slot the appropriate array item value into our parameter variable, whatever we may have called it.

To capture the argument, simply define the function with a parameter. 

How do we know that? 

We can look at the `forEach()` docs on MDN. 

![](../attachments/623.png) 4:30 / 7:22

In our case, we chose to name the `currentValue` parameter `topping`. 

We also have the ability to get the index and the array, so let's take a look at what that looks like. 

Modify the code like so 👇

```js
function logTopping(topping, index, array){
  console.log(topping,index, array);
}
toppings.forEach(logTopping);
```

When you refresh the HTML page and open the console, you will see that for each item in the array, the actual item was logged, the index and also the original array. 

![](../attachments/624.png) 4:52

Why would you need to pass the original array? 

Because if you need to grab something from the original array, you can. 

Let's do a quick example where we have to loop over each topping and:
 - log the topping
 - log the next topping if there is one
 - log the previous topping if there is one
 - if it's the last item in the array, log "goodbye"

The first one is easy, simply add `console.log(topping)`. 

Let's do the next topping. 

We have the index already and the original array, which we will rename because `array` is a bad parameter name. We also won't name it `toppings` because we already have a `toppings` array that lives outside of this function. Let's rename it to `originalArray` instead, like so 👇

```js
function logTopping(topping,index,originalArray)
``` 

Add a log of `originalArray[index]` and refresh the HTML page. 

![](../attachments/625.png) 6:26

```js
console.log(originalArray[index + 1]);
```

So now if you try adding 1 to the index as shown above, you should get the next one.  👇

Modify the code as shown below to add a log to see when it's looping

```js
function logTopping(topping, index, originalArray){
  console.log(topping);
  console.log(originalArray[index + 1]);
  console.log('--------🍕-----');
}
```

When you refresh the HTML page, you should see the following 👇

![](../attachments/626.png) 6:49

If you scroll all the way to the bottom, you will see that when we get to the last one, the next index returns `undefined`. 

![](../attachments/627.png) 6:57

We can check whether the next topping exists or not by adding the following code 👇

```js
const nextTopping = originalArray[index + 1];
if(nextTopping){
  console.log(nextTopping);
}
```

Now if you refresh the page and look at the console, you will see that for the last item, we are not logging the next one because it doesn't exist. 

![](../attachments/628.png) 7:22

We can go a bit further and make it a bit easier to understand using a ternary function.

```js
const nextTopping = originalArray[index + 1];
nextTopping ? console.log(nextTopping) : null;
```

That works just the same. Instead of putting `null`, you could put an empty string `""`, it doesn't matter as long as you put something there. 

Now the previous topping. 

Move the `prevTopping` and `nextTopping` variables to the top of the function and use the ternary operator to log the previous topping like so 👇

```js
const nextTopping = originalArray[index + 1];
const prevTopping = originalArray[index - 1];

prevTopping ? console.log(prevTopping) : null;
nextTopping ? console.log(nextTopping) : null;
 console.log('--------🍕-----');
```

![](../attachments/629.png) 8:25

Now the first and last topping should only have 2 items logged while all the other items have 3 items logged.

If it's the last item in the array we need to log "goodbye". How can we do that? 

Let's use `.length` on the array and a ternary statement. 

```js
index === array.length - 1 ? console.log('Goodbye') : console.log("getting the next topping");
```

![](../attachments/630.png) 9:21

Let's break down what we did exactly in that last example. 

Sometimes it helps to make it more readable if you put part on it's own line like so 👇

```js
index === originalArray.length - 1
? console.log("Goodbye")
: console.log('Getting the next topping');
```

So the condition we are checking is `index === originalArray.length - 1`, which checks whether the current index matches the last index in the array.  

We have access to the index of the currrent item in the `index` variable, and we can get the index of the last item in the array by doing `originalArray.length - 1`.  


If it is the last index, log "goodbye" and if it doesn't, log "getting the next topping". 

You could use an if statement instead of the ternary statement, it would work just as well.

We can also use the && hack we learned about earlier, like so 👇

```js
index === originalArray.length && console.log('Goodbye');
```

Why does that work? 

Because if the first statement is true, it will keep going for the next one and if it is false, it will short circuit and never get to the second one. 

That is what we referred to as **abusing conditionals** in our previous videos.

That wraps up the `forEach` method. 

It is a bit different than the other looping methods because it doesn't return any values. 

Notice how when we loop over each of our items we don't store our results in a variable like below 👇

```js
const result = toppings.forEach(logTopping);
```

When you loop over an array with `forEach` it doesn't actually return anything to you. It goes off and does some work for every item that is in that array. 

Let's see how that is different from what Wes likes to call the 'Big Three' which are: 
- Map
- Filter
- Reduce

We will go over those in the next video. 

---

## 50 - Looping and Iterating - Mapping

In the previous lesson we learned about `forEach`, which is useful when you want to loop over some data and do something with each piece of data.  That "something" may be displaying the data on a page, logging the value, or attaching an event listener to each item, those are often referred to as things called **side effects**. 

A **side effect** is when you are inside of a function and you reach outside of that function to do something else. 

While side effects are totally fine, because at some point you do need to do things that reach outside the function, there are a whole slew of other types of loops that are simply taking in data, doing something with that data and then returning the data that has been modified, massaged or transformed in some way. 

That is where we get into `map`, `filter`, and `reduce`. 

We have already looked at one example of `filter` and that is `find`, where you take in an array and return one thing. 

That is a transformation of that data and are often referred to as **pure functions**. 

**Pure functions** take in data, they return data, they always work exactly the same way given the data that's inputted, it returns the exact same thing. They don't reach outside themselves to do that. 

Let's talk about `map`. 

Map is like a machine in a factory. It takes in data, performs an operation and then spits it out on the other side.

`map` will always produce the same length of the array as it starts with. 

Let's go into a little example right now. 

Add `console.clear()` to the script tag to clear all the `toppings` work we did in the previous lesson. 

Wes loves the analogy of a machine, taking in data, performing an operation and then spitting it out on the other side. You can think of like a toy machine in a factory which adds one arm then the other arm then a leg. 

Let's do a really simple example. 

We have this array below 👇

```js
const faces = ['😃', '🤠', '🤡', '🤑', '😵', '🌞', '🐶', '😺'];
```

Let's create some functions that will map over each one. 

Let's make function `addArms`, that takes in a face, and returns an emoji. 

```js
function addArms(face){
  return `👋${face} 👋`;
}
```

That is just a regular function like we have written a hundred times by now. You can play with it in the console. It's silly, but it works.

![](../attachments/631.png) 3:01

Now what we can do is we can take our array of faces and add arms to all of them, and this how that works. 

```js
const toys = faces.map(addArms);
console.log(toys);
```

![](../attachments/632.png) 3:36

As you can see, what was returned to us is an array of exactly the same length as we put it in, so if the array had 8 things, it will have 8 things when it's returned, there is no way to return more or less items with `map`. 

You simply take in something and return something else. 

One other simple example is let's say you have this code below. 

```js
const fullNames = ['wes','kait','poppy'].map(name => `${name} bos`);
console.log(fullNames);
```

![](../attachments/633.png) 4:33

We could do multiple transforms. 

Let's make the code above into a function. 

```js
function bosify(name){
  return `${name} Bos`;
}

const fullNames = [ 'wes', 'kait', 'poppy'].map(bosify);
```

![](../attachments/634.png) 5:17

The first names don't have capitals so make another function `capitalize` which takes in a word. 

You can access each character of a word using an index. 

For example `'wes'[0]`, `'wes'[1]`, `'wes'[2]` will return the following 👇

![](../attachments/636.png) 5:55
 
So you can capitalize the first letter of the word as shown below. 

```js
function capitalize(word){
    return word[0].toUppercase();
}
```

Let's try the code as we have it so far. Chain the maps like so 👇

```js
const fullNames = [ 'wes', 'kait', 'poppy'].map(capitalize).map(bosify);
```

You can chain as many maps as you want because each returns a new array until it reaches the last one. 

A nice way to format that to make it easier to read is to put each map on its on line. 

You still only put one semi colon `;` at the end of the chain, not on each line. 

```js
const fullNames = ['wes','kait','poppy']
  .map(capitalize)
  .map(bosify);
console.log(fullNames);
```

![](../attachments/638.png) 6:56

As you can see, that does not return the whole word. 

Let's fix that.

We will use `slice` to return the words from index 1 to the end of the word like so 👇

```js
function capitalize(word){
    return word[0].toUppercase() + word.slice(1);
}
```

![](../attachments/639.png) 7:12

As you can see, that works. 

Let's change that so instead of using the `+` operator, we use backticks because it's better to reserve adding for numbers. 

Modify the code as shown below. 

```js
function capitalize(word){
    return `${word[0].toUppercase()}${word.slice(1)}`;
}
```

![](../attachments/640.png) 7:%6

Map will always take in an item, do some work with it and then return a new value. 

The same thing works with numbers. 

```js
const orderTotals = [342, 1002, 523, 34, 634, 854, 1644, 2222];
```

Lets say we want to add tax to all items in the `orderTotals` array. 

Watch what happens if for every single item in our map, we just return one. 

```js
const orderTotalsWithTax = orderTotals.map(total => 1);
```

![](../attachments/641.png) 8:32

As you can see, all the items in the array have now been turned into 1. 

Why? 
Because whatever you return from your map function will replace whatever was initially in your map function.

It is not **mutable**. 
What that means is our `orderTotals` are still there. 
The new array has the updated value. 

Back to our example, to add the tax to every item in `orderTotals`, add the following code 👇

```js
const orderTotalsWithTax = orderTotals.map(total => total * 1.13);
```

![](../attachments/642.png) 9:09

As you can see, we now have our values with tax added to them. 

Wes finds map to be extremely helpful.

There is one really silly example that Wes wants to show us. 

There is this thing on twitter where you can make cowboy bodies out of emojis.

![](../attachments/643.png) 9:41

```js
function attachBody(face, body) {
  return `
      ${face}
　　　　　${body.repeat(3)}
　　　　 ${Array(3).fill(body).join(' ')}
　　　👇🏽　 ${body.repeat(2)}　👇🏽
    ${Array(2).fill(body).join('   ')}
    ${Array(2).fill(body).join('   ')}
　　　　　👢　　👢
  `
}

faces.map(face => attachBody(face, '🍟')).forEach(body => console.log(body))
```

What Wes has done here is he has taken our `faces` array that we used earlier, looped over each item and pass it as an argument to `attachBody` along with the emoji to make the body out of. 

That will return us a new array and then for each of those we just log them. 

The `attachBody` function simply takes in a face, and then whatever the body is made up of and we use backticks so we can use multiple lines and then it fills in the variables.

So it fills in the `face` variable, then the `body` variable repeats 3 times.  

One thing Wes hasn't shown us yet is `repeat`. 

You can take a string and call repeat on it and javascript will repeat that however many times you like, like so 👇

```js
'x'.repeat(199);
```

![](../attachments/644.png) 10:46

Another thing Wes hasn't shown us yet is `Array.fill()`.  

With `Array(3)`, it will create 3 empty spots in an array, much like `Array.from()`. 

![](../attachments/645.png) 10:53

However if you want to fill them with the exact same thing, you can use `Array(3).fill('x')`. 

That is a bit quicker than `Array.from` and the map function that we looked at. 

![](../attachments/646.png) 11:09

In our `attachBody` function, we are just filling it with an emoji and then calling `.join(' ')` with a space separator in it. That gives us the actual body of the person.

`.map` can be used with any type of data. 

So far we have looked at examples with strings and numbers but more often than not, you will actually have an array of objects that comes back from the API. 

Let's take a look at an example with the `peoples` array.

```js
const people = [
  {
    birthday: "April 22, 1993",
    names: {
      first: "Keith",
      last: "Buckley",
    },
  },
  {
    birthday: "January 3, 1975",
    names: {
      first: "Larry",
      last: "Heep",
    },
  },
  {
    birthday: "February 12, 1944",
    names: {
      first: "Linda",
      last: "Bermeer",
    },
  },
];
```

Each person is signified by an object, and each person has a `birthday`, and a `names` object which has a nested `first` and `last` property inside of that.

That data is okay but it's not in the format that we need. That happens all the time when you are working with APIs. 

So what we have to do is take in that data and "massage" it a little bit and then return the new formatted data that we want. 

Go ahead and do that, as shown below 👇

```js
const cleanPeople = people.map(function(person){
  console.log(person);
})
```

We are using an inline function which takes in an parameter of `person` (which will be each item in the array as it loops through), and we log the `person`. 

It is fine to log within a `map` function, just don't ever do things like updating the DOM inside of a `map` function. That is what a `forEach` is for.

The first thing we need this function to do is get the person's birthday, and then figure out how old they are, and then return their full name and birthday in an object. 

First we have to get their birthday, which is stored in a string like "February 12, 1944". 

That is not very helpful to us because when you want to work with dates in Javascript, it has to be changed over to what is called a **Javascript Date**.

You can do that within the inline map function like so 👇

```js
const cleanPeople = people.map(function(person){
  console.log(person);
  const birthday = new Date();
})
```

If you don't pass a date when you create a date in Javascript as shown below, it will give you the current date time.

```js
new Date()
``` 

![](../attachments/647.png) 14:17

The date you see in the console in the video is the date that Wes is recording the video. 

If you do pass a string of a date to `new Date()`, like we have access to with `person.birthday`, it will return that date. 

```js
const cleanPeople = people.map(function(person){
  console.log(person);
  const birthday = new Date(person.birthday);
  console.log(birthday);
})
```

![](../attachments/648.png)14:37

As you can see, for each person we log the person and then it actual logs a true javascript date.

_HOT TIP 🔥: Use `console.dir(birthday)` to see all the methods that exist on a Date object._

If the date that you pass to the `new Date()` function doesn't have a time value, it will default to midnight. 

Now that we have the birthday, we want to figure out how old the person is. In order to do that, we need to know the current date. 

Modify the inline function like so to capture the current date in the variable `now` 👇

```js
const cleanPeople = people.map(function(person){
  const birthday = new Date(person.birthday);
  const now = new Date();
  console.log(birthday,now);
})
```

![](../attachments/649.png) 15:20

As you can see we have 3 different dates showing up. 

There are a number of methods on a Date in javascript that allow you to work with it. 

What Wes likes to do when comparing dates or trying to figure out how much time is in between two dates, is to change them into **timestamps**. 

Open up the console and run the code below. You will see that we get a number returned to us.

```js
const now = new Date();
now.getTime();
```

![](../attachments/650.png) 15:48

That number might look random but it is actually not random at all. 

That is the number of milliseconds since January 1, 1970. That is the time when they said okay, this is when date starts. Any dates that are negative, go back from that time and any dates that are positive go forward for that time. 

There is actually a shortcut to get the timestamp and that is using `Date.now()`. If you try running that a few times in the console, the number should change each time.

![](../attachments/651.png) 16:17

If you ever have one of these timestamps, you can go to the website https://epoch.now.sh. 

![](../attachments/652.png) 16:36

This website allows you to convert any date in the future or in the past to a timestamp. Javascript deals with milliseconds so you want to always work with that. 

It also allows you to do the opposite. It will take in a timestamp and convert it back to a regular date for you. 

So back to our inline map function, we don't want to just grab the persons birthday and convert it to a date, we want to convert it to a full blown timestamp. 

We can do that by chaining the `getTime` method onto `new Date(person.birthday).getTime();`. 

For the `now` variable, use `Date.now()` to get the timestamp instead of `new Date()`.  

`.now()` is a static method because it lives on the `Date` object.

```js
const cleanPeople = people.map(function(person){
  const birthday = new Date(person.birthday).getTime();
  const now = Date.now();
  console.log(birthday,now);
})
```

To find the difference between the two dates, use the following code 👇

```js
const age = now - birthday;
console.log(age);
```

![](../attachments/653.png) 18:12

That is how old each person is in milliseconds. 

We need to convert it into years. We need to do some math for that. 

Let's ask ourselves how many milliseconds in a year. We know there are 1000 milliseconds in a second, there is 60 seconds in a minute, there is 60 minutes in an hour, there are 24 hours in a day and 365 days in a year.

`1000 x 60 x60 x 24 x 365 = 31536000000`

There are other ways to do dates that will account for leap years and all that. 

There are whole libraries out there like the date functions library **date-fns**. Those libraries provide you with a whole bunch of robust tools for working with dates. 

Take our age calculation timestamp and divide it by that number like so 👇

```js
const cleanPeople = people.map(function(person){
  const birthday = new Date(person.birthday).getTime();
  const now = Date.now();
  const age = now - birthday / 31536000000;
  console.log(age);
})
```

![](../attachments/654.png) 19:22

That leaves us with some decimals which we can just take the lower bound of their number, because if they haven't hit their next birthday yet, you would say you are 26 years old. 

How do we take the lower bound of any number? 

It's not round because you don't round up to say how old you are. 
You take the lower bound with `Math.floor`. 

Modify the code like so 👇

```js
const age = Math.floor(now - birthday / 31536000000);
```

![](../attachments/655.png) 19:52

Now that we have their birthday and figured out how old they are, we want to return their full name and birthday in an object.

To do this, simply return an object from the inline function that has a property of `age `which is equal to our `age` variable, and then the `name` property will be the person's last and first name variables combined using interpolation as shown below. 

```js
const cleanPeople = people.map(function(person){
  const birthday = new Date(person.birthday).getTime();
  const now = Date.now();
  const age = Math.floor(now - birthday / 31536000000);
  console.log(age);
  return {
    age: age,
    name: `${person.names.first} ${person.names.last}`,
  }
})
```

Note: as mentioned before, if the property is the same name as the variable, we could have returned the object like so  👇

```js
 return {
    age,
    name: `${person.name.first} ${person.name.last}`,
  }
```

They both work the exact same way.

Let's log `cleanPeople` in a table. 

```js
console.table(cleanPeople);
```

![](../attachments/656.png) 21:16

As you can see we have everyone's name and age. 

That is what `map` does. It takes in some data that doesn't look exactly how you like it. You do a bunch of data massaging and then spit it out the other end. 

---

## 51 - Looping and Iterating = Filter, Find and Higher Order Functions

You can skip this lesson if you feel confident with your knowledge of `filter` and `find` because we have already covered that a few times. 

Wes just wants to have a video specifically dedicated to it so you can come back and refer it at a later time conveniently. 

Let's continue from the example in our previous lesson, where we created a `cleanPeople` array, which we will work with in this example. 

![](../attachments/657.png) 00:25

Very often you will find yourself in a situation where you either need to find one person in an array or you want to filter the list down to be a subset of it. 

Let's say you want to find people who are over 40 years old. 

You can use `.filter()` for that. 

The way filter works is you loop over every single item in an array, and you either say yes (true) or no (false). 

If you return true that item will be in the array subset, if you return false it will take out that item from the array that is returned.

```js
const over40 = cleanPeople.filter(function(person){
  if(person.age > 40 ){
    return true;
  }
  else {
    return false;
  }
})
console.table(over40);
```

That is the verbose way to write it, which Wes is using just to show us how it works.

![](../attachments/659.png) 1:39

As you can see, we now have only a subset of the original array. 

Now let's refactor the function above to make it more concise.

How Wes would approach it is he would look at the condition within the filter function. If the condition is met, we will return true. 

That means there is no need for an else because anything that comes after the condition will only run if the condition is true. So that else is unnecessary.

```js
  if(person.age > 40 ){
    return true;
  }
  return false;
```

Since the condition evaluates to true or false, we can just return the condition like so 👇

```js
const over40 = cleanPeople.filter(function(person){ return person.age > 40});
```

We can make it an arrow function like so 👇

```js
const over40 = cleanPeople.filter((person) => { return person.age > 40});
```

We can go one step further and make it an implicit return and take off the parameter parenthesis like so 👇

```js
const over40 = cleanPeople.filter(person => person.age > 40);
```

If there ever is a situation where we call this filter method on an array with no people over 40 in it, it will just return to us an empty array. 

![](../attachments/660.png) 3:29

If you wanted to check if there were any people over 40 in this case you could use the following code 👇

```js
if(over40.length){
  console.log('There are some people over 40');
}
 ```

That is how filter works. 

`.find()` works the exact same way except that find only finds one item in the array and returns it whereas filter will always return to you all of the items that match. 

`.filter()` will always return an array

`.find()` will always return the item that you want. 

Let's use the `students` array for our find example. 

Here is what that array looks like 👇

```js
const students = [
  {
    id: "11ce",
    first_name: "Dall",
    last_name: "Puckring",
  },
  {
    id: "2958",
    first_name: "Margarete",
    last_name: "Brandi",
  },
  {
    id: "565a",
    first_name: "Bendicty",
    last_name: "Woodage",
  },
  {
    id: "3a16",
    first_name: "Micki",
    last_name: "Mattes",
  },
  {
    id: "f396",
    first_name: "Flory",
    last_name: "Gladeche",
  },
  {
    id: "de5f",
    first_name: "Jamill",
    last_name: "Emilien",
  },
  {
    id: "54cb",
    first_name: "Brett",
    last_name: "Aizikowitz",
  },
  {
    id: "9135",
    first_name: "Lorry",
    last_name: "Smallman",
  },
  {
    id: "978f",
    first_name: "Gilly",
    last_name: "Flott",
  },
];
```

Now let's say you want to find a student with the `id` of `565a`.

```js
const student = students.find(student => );
```

The code above is incomplete, but one weird thing worth pointing out is that we are naming the variable that we are storing the item in as `student` but we are also naming the individual loop a student. 

Is that okay? 

It is allowed because the student which is a parameter of the `.find()` loop is scoped to within that function. It is confusing however so it's often better to change it to something else. 

We will name the parameter `stud` instead like so 👇

```js
const student = students.find(stud => stud.id === '565a');
console.log(student);
```

![](../attachments/661.png) 5:19 

As you can see, the correct student record is returned. 

If that didn't match anything, what would we find? 

We would get `undefined`. You always want to check if something got found. 

![](../attachments/662.png) 5:25

As you may have noticed, the `find` method did not return an array of students to us, it returns to us an object which is the student itself. 

We could just swap the `.find()` to a `.filter()` like so 👇

```js
const student = students.filter(stud => stud.id === '565a');
console.log(student);
```

![](../attachments/663.png) 5:41

As you can see, that returns to us an array of one item. 
That is the different between `.filter()` and `.find()`, everything else is exactly the same.

One neat thing that we could do is make an external function and then pass that in, like so 👇

```js
function isStudent(student){
  return student.id === '565a';
}
const student = students.find(isStudent);
console.log(student);
```

Now that is a little bit weird. Why would we write a function that is hardcoded to a specific id? It's more likely that we will be looking for a student with their own specific id, so a hardcoded value would not work for all students. 

What we can do is wrap that in another function called `findById`, which takes in one parameter,`id`, and which returns another function like so 👇

```js
function findById(id){
  return function isStudent(student){
    return student.id === id;
  }
};
```

This is called a **high order function** or a **higher order function**. It is a function that will return another function. 

Now we can simply replace the method we pass to `.find()` like so 👇

```js
const student = students.find(findById('56a'));
```

`findById('56a')` will generate a new function that is coded to find the id that we are looking for (56a). 

![](../attachments/664.png) 7:22

It still finds the right person, it's just a little bit more flexible 

Let's say you run into a scenario where the object has a lot of properties. 

Are you going to create a separate function called `findByFirstName` and then `findByLastName` and then all the other properties? 

Instead of doing that, we can modify the function to be even more flexible. Start by creating a new function which takes in 2 things:
- the property
- the property value 

It will return a function which is the looping function. 

We are not going to return if the `id` is equal to the `id`, we are going to return if the `student` property is equal to the property value we are looking for. 

```js
function findByProp(prop, propWeAreLookingFor){
  return function isStudent(student){
    return student[prop] === propWeAreLookingFor;
  }
}
```

Now that might be a little confusing to you. Let's go over how it works.

```js
const student = students.find(findByProp('id', '565a'));
```

We have made the function really flexible now. If you ad the coded above, you will see that it still works, but we can also make other student where the first name property is equal to  'Micki'. 


```js
const student = students.find(findByProp('id', '565a'));
const student = students.find(findByProp('first_name', 'Micki'));
console.log(student);
console.log(student2);
```

![](../attachments/666.png) 9:17

Let's go over the function one more time. 

The `findByProp` function takes in a prop as the first parameter and `propWeAreLookingFor` as the second parameter. 
What that means is the first parameter takes in the key, and the second parameter takes in the value we are matching the property against.

![](../attachments/667.png) 9:39

In the image above, the text that is selected is the property `last_name` . It is the property key. 

![](../attachments/668.png) 9:40

The property value for the `last_name` property for the student shown above is `Aizikowitz`. 

So our function takes in a property and a value, and then it will look in each object for whatever property you specified is equal to whatever value you specified.

![](../attachments/669.png) 9:55

The reason we have to use square brackets and not the dot notation in the code highlighted in the image above is because the property that we are looking for is being passed in as an argument to the function. 

This is a bit advance so don't feel too let down if you feel a bit confused. 

It took Wes years to understand the benefit of a function like we just made with `findByProp`. 

---

## 52 - Looping and Iterating - Reduce 

Let's add a `console.clear()` to the bottom of the script section in the HTML page we have been using for the last few examples. 

So far we have covered `.map()`, where you take in items and return transformed items, and `.filter()` where you take in items and return a subset of those items. 

`.reduce()` is probably one of the trickier array methods to understand because it does so much and there are a couple of different use cases for it. 

So what does it do? 

It takes in an array of data (just like `map` and `filter`) and it will return to you a result of or a single value. 

Now what does that exactly mean? 

Let's do an example to demonstrate. 

```js
const orderTotals = [342, 1002, 523, 34, 634, 854, 1644, 2222];
```

We want to take the `ordersTotal` array and add up all the numbers in the array. 

One way you could approach it is to set a let variable to 0 and then use a `forEach()` to loop over each item and add to the total. 

```js
let total = 0;
orderTotals.forEach(singleTotal => {
  total = total + singleTotal;
})
console.log(total);
```

![](../attachments/670.png) 1:40

As you can see, that does work. However, is that the best way to add up a bunch of things? 

No, it is not. 

![](../attachments/671.png) 1:52

We have the callback method within the `forEach`, which relies on an external variable being made. So we have sort of reached outside of it. That is what is referred to as a **side effect** which is where you update a variable that exists outside of the function. 

`.reduce()` will allow us to loop over every single item in that array, and in this case it would allow us to do a running total with those numbers. 

Here are some visualizations that Wes has pulled from online by google image searching "map filter reduce".

![](../attachments/672.png) 2:36

In the image above, the language is not javascript but it doesn't matter because each language has some version of map, filter and reduce. 

The `map` function in the image above takes in raw materials of cow, potato, chicken and corn and that returns the cooked materials via the cook function. 

The filter will return to you a subset of the original array of what is vegetarian. 

`.reduce()` will take in an array of food and return to you something that is compiled into a smaller version of it.

If you think about making a reduction when you're cooking or making a soup, what you do is you add a whole bunch of stuff to it and then you let it simmer and sort of become one. It is typically reduced down to something that is smaller than the original value that it came from. 

Now we will go through a bunch of use cases for `.reduce()`. 

Make a new variable called `allOrders`. We will call `.reduce()` on our `orderTotals` array.

```js
const allOrders = orderTotals.reduce();
```

We need a callback function that will be run on each item in the array, which we will call `tallyNumbers`. 

It will take in 2 arguments because that is what the callback function of a reduce method takes. 

Let's look that up in the MDN docs.

![](../attachments/673.png) 4:26

The 2 parameters it takes is the **accumulator** and the current value.

The **accumulator** is the thing that has been handed to you from the last instance of the loop. The `currentValue` parameter is the current item in the array.

We will name our parameters `tally` and `currentTotal`. 

Inside of the function, add a log of the current tally and current total, like so 👇

```js
function tallyNumbers(tally, currentTotal){
  console.log(`The current tally is ${tally}`);
  console.log(`The current total is ${currentTotal}`);
  console.log('--------');
}
const allOrders = ordersTotal.reduce(tallyNumbers);
console.log(allOrders);
```

![](../attachments/674.png) 5:31

Now there might be some stuff in the console does not make sense, so let's go through it together. 

The first time the loop runs, the current tally is 342 and the current total is 1002. 

The second time the loop runs, we get the current tally is `undefined` and the current value is 523. In fact every time other than the first instance of the loop, `tally` is undefined. 

That is because `reduce()` takes in another argument which is what do you want to start the accumulator at. 

In our case we want to start counting at 0 so we pass in 0 like so 👇

```js
const allOrders = orderTotals.reduce(tallyNumbers, 0);
```

![](../attachments/675.png) 6:39

So as you can see, in the first loop the `tally` is 0 and then in the rest it is `undefined`. 

Now that we got the loop working, we have this problem where everything after the first loop is returning `undefined` for the tally. 

That is because of the accumulator parameter, `tally`, that is passed from the previous iteration of the loop. 

If we were to just return `'WES IS COOL';` from each of the iteration in our loop, the accumulator is going to be equal to that on the next iteration. 

Modify the `tallyNumbers` function by adding `return 'WES IS COOL'` as shown below. 

```js
function tallyNumbers(tally, currentTotal) {
  console.log(`The current tally is ${tally}`);
  console.log(`The current total is ${currentTotal}`);
  console.log("----------");
  return "WES IS COOL";
}
const allOrders = orderTotals.reduce(tallyNumbers, 0);
```

![](../attachments/676.png) 7:18

As you can see, the first time the loop runs, `tally` is 0 because we started with an accumulator of 0 and then for all the next instances, our accumulator `tally` is equal to "WES IS COOL" because whatever you return from this function is what the accumulator is equal to. 

So what we really want to do is return the current tally + the current order's total. 

```js
function tallyNumbers(tally, currentTotal) {
  console.log(`The current tally is ${tally}`);
  console.log(`The current total is ${currentTotal}`);
  console.log("----------");
  return tally + currentTotal;
}
const allOrders = orderTotals.reduce(tallyNumbers, 0);
```

![](../attachments/677.png) 7:49

In the console above, as you can see we start with 0 because our accumulator starts at 0 as shown in the highlighted code in the image below. 

![](../attachments/678.png) 7:56

If we were to not pass an accumulator, the first loop iteration will take the first two numbers. In our case, that would still work but Wes always like to pass a default value so we know what we are starting with and so we can see what type we are starting with. 

So we start with 0, then the `currentTotal` is 342. Then in the next iteration, because we have returned 342 from the previous iteration, we are going to start with that as `tally` variable in the next iteration. We add the current value and return the `tally` variable to the next iteration and so on.

A reduce will loop over items in an array and every single time that you loop over an item in an array, you have an option to return a value which you can use to accumulate values or distill them down into one value.

Now, if we want to total the numbers, we already have them in the `allOrders` variable so we can simply log that variable to the console which should return to us 7255.

For the next example, let's look at the `inventory` variable. 

```js
const inventory = [
  { type: "shirt", price: 4000 },
  { type: "pants", price: 4532 },
  { type: "socks", price: 234 },
  { type: "shirt", price: 2343 },
  { type: "pants", price: 2343 },
  { type: "socks", price: 542 },
  { type: "pants", price: 123 },
];
```

It is an array of objects and each object has a `type` and a `price` property on it. 

In this exercise, we need to figure out how many instances there are with type of pants, how many are pants, and how many are socks. 

We also want to figure out what is the total value of all of the inventory that we have.

You could probably figure out how to calculate the total value form the last exercise, but the other part where we need to count how many instances of something there are, happens all the time in Javascript.

Let's add some code. 

Make a function called `inventoryReducer` which we will pass to `.reduce()` when we call it.  

```js
function inventoryReducer(){

}
const inventoryCounts = inventory.reduce(inventoryReducer,);
```

We also need to decide what value we should start with for the accumulator. 
In our case, we want to return an object that looks something like this 👇

```js
{
  shirts: 3,
  pants: 2,
  socks: 523
}
```

In order for us to get that, we need to pass an object. 

We could pass an object like this 👇

```js
const inventoryCounts = inventory.reduce(inventoryReducer, {
  shirts:0,
  pants: 0,
  socks: 0
});
```

That would start everything off at zero. 

However, more often then not, you are not aware of all of the different types that will be coming in so there is no way for you to go in and make a huge list of everything ahead of time. Or -- you might be aware of it and there are 50 different things so it doesn't make sense to do that.

What we will do instead is we will start of with an empty object and then add the keys and set them to one as they appear, otherwise if they already exist, we will increment them by one. 

```js
const inventoryCounts = inventory.reduce(inventoryReducer, {});
```

Shown above is how you pass an empty object as the accumulator

Our reducer takes two things: 

1. our accumulator which we will call `totals`
2. our item which we will call `item`


Let's add a log to our reducer function which logs the item's type like so 👇

```js
function inventoryReducer(totals, item){
  console.log(`Looping over ${item.type}`);
}
```

![](../attachments/680.png) 11:54

Inside of the reducer we need to increment the type by 1 and then return the accumulator or return the totals so the next loop can use it. 

To increment the type, let's try the following code. 

```js
function inventoryReducer(totals, item){
  console.log(`Looping over ${item.type}`);
  totals.shirt = totals.shirt + 1; 
  return totals;
}
const inventoryCounts = inventory.reduce(inventoryReducer, {});
console.log(inventoryCounts);
```

![](../attachments/681.png) 12:42 

Hm.. shirt is equal to `NaN`. Why would that be? 

That is because if you are trying to add one to something that doesn't exist, it will give you `NaN` (not a number). 

What we can do is check if the shirt already exists on `totals` and if it does, we increment it by one, but if it doesn't, we will set it to 0. 

Instead let's set `totals.shirt` to equals itself plus 1 or 1 like so 👇

```js
totals.shirt = totals.shirt + 1 || 1;
```

Lets try it. 

![](../attachments/682.png) 13:17

Why did that work? This is an example of **taking advantage of conditionals** or **abusing conditionals**. 

If we were to write that as an if statement, it would look like this 👇

```js
if(totals.shirt){
  totals.shirt = totals.shirt + 1;
}
else {
  totals.shirt = 1;
}
```

Note you can also increment totals.shirt like this `totals.shirt++;` Both work!

So what is happening there is if the property doesn't exist, we first need to add it, and set it to 1, and then we can start incrementing it.

In this statement `totals.shirt = totals.shirt + 1 || 1;`, if `totals.shirt + 1` turns out to be `NaN`, then that is falsy and it will fall back to 1. 

It's a bit harder to read which in a lot of cases isn't ideal, but it is nice to do it in a one liner. 

Shown below is yet another way 👇

```js
totals.shirt ? totals.shirt + 1 : totals.shirt = 1;
```

We are checking if `totals.shirt` exists, if it does, we increment it by 1, if it doesn't we create the property and set it to 1. 

One thing you may have noticed is we have been hard coding shirt, which we shouldn't be doing because there are a few different types. 

We can change it to a variable lookup item using square brackets like so 👇

```js
totals[item.type] = totals[item.type] + 1 || 1;
```

![](../attachments/683.png) 15:33

As you can see, now our accumulator has the 2 shirts, 2 socks and 3 pants.

Pretty often a reduce can be done in an arrow function, a really quick one. 

In our case, we just want to add up the inventory `price` on each of them. 

We will start with 0 as our accumulator because we want to add up the total prices. 

```js
const totalInventoryPrice = inventory.reduce((acc, item) => acc + item.price, 0);
console.log(totalInventoryPrice);
```

We loop over every single item and then we return the accumulator plus the current item price.

---

## 53 - Looping and Iterating - Reduce Exercise

This lesson is an exercise where you have to use `map`, `filter`, and `reduce` all in one exercise. 

The task is to go to any webpage, like the Mozilla Developer Docs for reduce, copy every single piece of text like Wes is doing in the screenshot below by pressing `Cmd` + `A` and `Cmd` + `C` and then counting how many times every letter and number occurs on the page.

![](../attachments/684.png) 00:27

Here are a couple of tips:
- first grab all the text
- then convert the text to an array of letters 
- then we need to filter the text to grab only letters and numbers and ignore other text content like parenthesis, question marks, white space etc.
- we want to make sure that whether the letter is uppercase or lowercase, we still only count it once. For example `a` and `A` would could as two "a"s, not one uppercase A and one lowercase a.

This is going to use `filter`, `map` and `reduce` all in one go. 

Open up the file `reduce-challenge.html`. 

The first thing we will do is get the text in there. 

Create a variable called `text` and use backticks for the value because we are going to paste the text we copied between the backticks and backticks allow our text to be multi line. 

Note: the text within the `text` variable has been shortened for demonstration purposes in the following code examples. 

```js
const text = `
[0, 1, 2, 3, 4].reduce( (accumulator, currentValue, currentIndex, array) => accumulator + currentValue );
If you were to provide an initialValue as the second argument to reduce(), the result would look like this:
The value returned by reduce() in this case would be 20.

Examples
Sum all the values of an array`;


console.log(text);
```

![](../attachments/685.png) 1:48

As you can see, we have over 31.1 KB worth of text. 

How can we convert all of the text into an array of every single letter? 

You can call `split()` or spread it into an array.

For example we can call split on our `text` variable and pass it an empty string so that we split it on nothing like so 👇

```js
const everything = text.split('');
console.log(everything);
```

![](../attachments/686.png) 2:18

As you see, now we get an array with 15,911 letters that are in it. 

Next we need to deal with ignoring the case when counting letters. 

There are 2 ways we can do that:
- we can either lowercase everything immediately or 
- we could filter the things out for what we want

If we do lowercase first, we will be unnecessarily lowercasing things that do not have lowercase and uppercase, such as symbols like the question mark and numbers etc. 

However, if we filter first, then our matcher will have to match both uppercase and lowercase.

Let's get rid of the junk by using `.filter()` before lowercasing. 

 ```js
 const result = everything.filter(char => )
 ```

We pass our filter a `char`, which is an instance of the item from our array, and then we want to filter out any items that are not letters or numbers from a-zA-Z and numbers 0-9. 

### Regular Expression

So how do we check if a character is from a-z, A-Z or 0-9? 

We can use a `.match()` function. 

Let's look at these docs: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions

![](../attachments/1473.png)

A **regular expression** is a way to use what is called a **Regex pattern** to match characters within a string. 

There are a number of different methods that take a Regex like `match`, `matchAll`, `replace`, `search`. 

So if we wanted to filter for the letter a for example, we use a matcher. 

The way you pass a regular expression to the `.match()` method is you put two forward slashes like `//` and then put the matcher in the middle. 

To check for a match with the letter `a` you would do `char.match(/a/)`, like so 👇

```js
const result = everything.filter((char) => {
  // if that characer is a-zA-Z0-9
  if (char.match(/a/)) {
    return true;
  }
  return false;
});
```

![](../attachments/687.png) 4:30

As you can see, when we checked if it is a match with the letter `a`, it returned the value with a bit more information like where we found the word. 

![](../attachments/688.png) 4:40

However when we check if `'a'.match(/b/)`, it returned false because 'a' clearly does not match the letter 'b'. 

In our case, we need a Regex that will match all letters, so we can do that using groups like so `/[a-z]/`. 

Let's try that to see how we are doing.

```js
const result = everything.filter((char) => {
  // if that characer is a-zA-Z0-9
  if (char.match(/[a-z]/)) {
    return true;
  }
  return false;
});
console.log(result);
```

![](../attachments/689.png) 5:06

We have over 10,000 letters in our filtered array now. 
If you look closely, you will see they are all lowercase. 

Let's fix that by modifying the group in our Regex like so 👇

```js
char.match(/[a-zA-Z]/)
```

![](../attachments/690.png) 5:20

As you can see, our array now contains letters as well. 

Now we need to get numbers so we can add 0-9 to our group, as shown below.

```js
char.match(/[a-zA-Z0-9]/)
```

Wes knows this off the top of his head from years of writing regex's. 

However you can use the website https://regexr.com to find lots of patterns there and cheat sheets to help you match any character except a new line.  


![](../attachments/691.png) 5:54

Another thing you could do is pass the case insensitive flag like so 👇

```js
/([A-Z])/i
```

What that will do is it won't care about upper or lowercase. So in our case we could have done the regex like this 👇

```js
char.match(/[a-z0-9]/i)
```

The `i` flag will make it case insensitive. 

Let's refresh to mak sure that still works. 

![](../attachments/692.png) 6:24

As you can see, it does work, and we also getting numbers now. 

_(You might notice in the dev tools that when you expand a large array, it breaks them up into groups as displayed in the image below.)_

![](../attachments/693.png) 6:29

So that is our first filter. The next thing we want to do is to lowercase everything. 

One way we can do that is using `.map()`. 

We can chain the `.map()` directly on the `.filter()`, however the code is getting to be a little bit hard to work with so let's first refactor a bit. 

Refactor the inline function we pass to `filter` to an external function we will name `isValidChar`. 

```js
const everything = text.split("");
function isValidChar(char) {
  return char.match(/[a-z0-9]/i);
}

const result = everything.filter(isValidChar);

console.log(result);
```

That already looks much neater. 

We can make the code even more concise by chaining the `.split()` instead of assigning it to a variable, like so 👇

```js
function isValidChar(char) {
  return char.match(/[a-z0-9]/i);
}

const result = text.split("").filter(isValidChar);

console.log(result);
```

Often developers like to put each method that is chained on it's own line as shown below. 

```js
const result = text
  .split('') //split each char into an item of an array
  .filter(isValidChar);

console.log(result);
```

Now let's chain the map over a function we will call `lowercase`. 

```js
function lowercase(char){
  return char.ToLowerCase();
}
```

You could also write that as an arrow function, which we will use instead so comment the `lowercase` method we just added out and add the code below

```js
const lowercase = char => char.toLowerCase(); 
```

If you refresh the page and open the array in the console, you will see that now there are only lowercase letters.

The last step in this exercise is to count the instances of each letter and number using a reduce. 

Let's create an external function which we will pass to the reduce method. 

We want to start with an empty object so we will pass that as the second argument. 

```js
function instanceCounter(){
}

const result = text
  .split("")
  .filter(isValidChar)
  .map(lowercase)
  .reduce(instanceCounter, {});
```

We will name the accumulator parameter `counts` and the individual character instance `char`. 

Inside of the function, we will check whether the character already exists in the array using square brackets and a ternary function. 

If the character does exist, we will increment it by 1. 

If it does not, we will add it and set it to one. 

```js
function instanceCounter(counts, char) {
  counts[char] ? counts[char] + 1 : (counts[char] = 1);
}
```
If you refresh the page, you might see something like the following error 👇

![](../attachments/694.png) 11:02

In Wes' example, `k` is the second character. 

![](../attachments/695.png) 11:06

Why is it telling us it's `undefined`? 

It's because the first time it works, the first time our reducer accumulator is an object. However, because we didn't return anything from this line, then the second time the return is `undefined`. 

To fix the issue, we simply need to add `return counts;` to the end of our `instanceCounter` method, as shown below. 

```js
function instanceCounter(counts, char) {
  counts[char] ? counts[char] + 1 : (counts[char] = 1);
  return counts;
}
```

If you refresh the page and open the console, you will see it is showing a count of 1 next to each character. 

That's not right!

![](../attachments/696.png) 11:36

Let's debug this by looking at our ternary operator in `instanceCounter`. 

So first we check if the letter exists in the array with `counts[char] ?`.

If it does exist, then the count of that character should be equal to the existing count plus one. 

We forgot the equal sign!

![](../attachments/697.png) 11:56

Modify the code like so

```js
counts[char] ? counts[char] = counts[char] + 1 : counts[char] = 1;
```

You could even put the ternary operator on separate lines as shown below.

```js
counts[char] 
  ? (counts[char] = counts[char] + 1) : (counts[char] = 1);
```

![](../attachments/698.png) 12:26

It looks like we are getting real values!

A fun thing you could do now with the object we get back is figure out how to sort the characters from the most popular to the least popular. 

Let's do it together. 

What if we try using `Object.entries(result);`? 

![](../attachments/699.png) 13:31

It gives us an array of arrays with each arrays first item being the key and the second item being the count.

Next, we can use `.sort()`. 

Create an external function `sortByValue`, and name the two parameters `a` and `b`. 

Within the function, we will compare the second items in the array because the first item is the key and the second item is the count.  We want to compare the count. 

If you recall, the way that sort works is that you can take the previous item and the next item and compare their values. 

You can return any of these from a sort:
- 0, stay where you are. 
- -1, go forward
- 1, go backward towards the end of the array

So instead of saying if it's greater or less than (go back to the sorting video if you want to see that), we can simply just return whatever the value is. 

It might be a positive value, it might be a zero value, that's just the benefit of doing that.

```js
function sortByValue(a, b) {
  return a[1] - b[1];
}
const sortedResult = Object
    .entries(result)
    .sort(sortByValue);
```

![](../attachments/701.png) 14:31


It is possible to do all of the work we just did in one single reduce function,  but it's much easier to read and better for re-usability to split it up into separate functions and chain them along. 

---

## 54 - Looping and Iterating - for, for in, for of, and while Loops

We are going to talk about 4 types of loops in this video:
1. for loops
2. for in loops
3. for of loops
4. while loops

They are not as popular as the array methods that we are working with. However, you should still know them because you will run into them from time to time. 

We will be working out of the `for-loops.html` file. 

### The for loop

Let's start with the for loop. The way it works is you type `for` with parenthesis and then you open and close a block. 

Let's look at the for loop docs really quickly. 

![](../attachments/703.png) 00:36

The for loop requires three things:
1. an initial expression
2. a condition
3. an increment expression

The plain for loop is great for running a block of code a certain number of times for example 5 times. 

Let's start with an extremely basic example. 

Add the code below. 

```js
for(let i = 0; i<= 10; i++){
  console.log(i);
}
```

What we did above is:
- we added the initial expression `let i = 0;` within the parenthesis
- then we added the condition if `i` is less than or equal to 10, `i <= 10;`
- finally we have the increment expression which is `i++`


If you open up the page in a browser and look at the console, you should see 0 through 10 logged, just like in the image below.

![](../attachments/704.png) 20:28

What has happened in the code is we looped from 0 to 10, so we looped 11 times over, and logged what the `i` variable equals. 

Let's go through this piece by piece to make sure we understand it. 

You can think of the first piece, the initial expression, as sort of a setup for the code you are about the write. 

```js
let i = 0;
```

The second piece, the condition, will run each time before the loop runs. In our example the condition is `i <= 10`. 

If the condition is true, then the loop will run one more time, and so on until the condition is false. 

Once the condition is false, the loop will no longer run and it will just move on to the next lines of code underneath it. 

Finally, the last piece is the increment, which in our example is `i++`. 

In this example, we are taking `i`, which we have set to 0, and incrementing it by 1 every time our loop runs. That lets us access this variable, `i`, inside of the loop. 

You might be wondering why we made the `i` variable a `let` instead of a `const`. 

![](../attachments/705.png) 2:18

As you can see, it logs 0 then returns an error. 

Let's go over why.

The first time the loop runs, the setup is run (the initial expression) which assigns a variable called `i` and sets it to 0.

Then we check if it is less than 10 (the condition), which is true then the code moves onto the loop block, which logs `i` which is 0 the first time it runs. 

Once the loop block has finished running, it comes back and increments the `i` variable (the increment) by 1 like so `i++`. 

The error we get in the console is 
>Uncaught TypeError: Assignment to constant variable.

You cannot increment a constant variable, so that is a bit of an issue, which is why we use a `let` instead.

What else can you do with `for` loops? 

They are helpful for if you want to start at say 100, go until `i` is greater than or equal to 120 and increment by 2.

```js
for(let i = 100; i < 120; i += 2){
  console.log(i);
}
```

![](../attachments/706.png) 3:11

As you can see, this loop is fairly flexible in incrementing the way that we want. 

One thing to note is the last part of the loop, the increment part, doesn't have a semi colon. 

If you try to add it like so `for(let i = 100; i <= 200; i += 2;)`. You will get an exception of "Uncaught SyntaxError". 
Thankfully your ESLint should catch that for you and yell at you.

Traditionally, for loops were used to loop over something, like an array of numbers. 

It very well may be that you see this in the wild so Wes is going to show us how it works.

You might notice that we are using a variable named `i` again in this example and wondering how that is possible because we have already used it. 
That is the beauty of `let`. Even though the assignment of the variable `i` is the in parenthesis, it's actually scoped to it's body so you are able to reuse it. 

When we used to just have `var` variables, that was not the case. 

Let's demonstrate how it used to work with `var`. 

Add the following code 👇

```js
for(var i = 0; i <= 120; i +=2){
  console.log(i);
}

console.log(i);
```

![](../attachments/707.png) 4:23

Our code logged 100-120 but then suddenly we see 22. 
Why is that? 

Because the last time the loop ran, that variable was incremented, so the condition was no longer true but the value of the `i` variable was globally scoped so it remained 22. 

So if we wanted to make another loop and we had used `var i`, we would have to find another variable name. 

If you wanted to loop over the array the old fashioned way, you could do this. 👇

```js
for(let i = 0; i < numbers.length; i++){
  console.log(i);
}
```

![](../attachments/708.png) 5:04

As you can see, it logged 0 to 11 because there are 12 numbers in our `numbers` array (you can check the length by typing `numbers.length` in the console).

Now to access the individual number, you would have to use the index to retrieve it using square brackets like so 👇

```js
for(let i = 0; i < numbers.length; i++){
  console.log(numbers[i]);
}
```

![](../attachments/709.png) 5:29

That is the way loops used to be done. It is much easier now with a `foreach` and `map` and `reduce` methods. If you do see the old way, maybe ask yourself can I refactor that?

Another place that `for` loops are useful is when you are working with canvas. 

If you remember back to our Etch-a-Sketch exercise, the canvas element actually has a method on it called `getImageData` that will allow us to pull the stuff out of that canvas. 

![](../attachments/710.png) 6:40

If you open the `etch-a-sketch.html` html file, draw in the top left hand corner of the etch-a-sketch and then inspect the canvas, if you click on the canvas element in the inspector and then flip to the console and type `$0`, you should get the canvas element returned. 

You should be able to access `ctx` which is the canvas context in the console. Call the following code from the console: `ctx.getImageData(0,0,100,100)`.  

That returns a data array with a lot of items, 40000 in our case.

![](../attachments/711.png) 6:49

It is a special kind of array called a **ClampedArray** which is used when you have very, very, very large arrays.

The contents of the array are numbers like 255, 0, 119, and they represent RGBA values. 

![](../attachments/712.png) 7:15

What that code did is it pulled the raw data from the canvas element, and for each pixel on the canvas, it is returning 4 values. 

![](../attachments/713.png) 8:09

The red is 255, the green is 0, the blue is 119, and then it returns to us an alpha channel which is if it's transparent or not. 255 would be totally not transparent and then 0 is totally transparent.

That is a pretty common thing to do, and if you want to loop over that data, you would have to loop over every single pixel, meaning that you would have to take 4 at a time. 

In that scenario a `for` loop that can increment itself by 4 instead of by 1 is very handy.

That is the only place that Wes still uses a for loop. 

#### for of Loop

The `for of` loop is fairly new to the language and it is actually pretty nice. 

So what is it? 

It is used for looping over iterables. If you recall, an **iterable** is anything that has a length, so something like an array or a string. 

Let's say you wanted to log all the letters in the `name` variable. You could do that with the following code 👇

```js
const name = 'Wes Bos';

for(const letter of name){
  console.log(letter);
}
```

![](../attachments/714.png) 9:24 

Why would that be better than splitting the string into an array and using `forEach` like we have learned in a previous exercise? 

One thing is it can handle emojis. 

![](../attachments/715.png) 9:48

For the family emoji, if you log it, you will see we get the family emoji and then the modifier, which is peach skin. 

![](../attachments/716.png)9:58

If you tried that with `name.split('')`, you would see something similar to the image below. 

![](../attachments/717.png) 10:18

As you can see, it doesn't know how to handle the emojis.

Another way you could do it is using the spread operator like so:

```js
[...name]
```

![](../attachments/718.png) 10:25

That is one use case. T

he other use case is something to do with **promises**, which we have not covered yet. 

### `for of` loop

If you ever need to sequence a bunch of data, meaning you have to do one thing after another in a loop, the `for of` loop will allow you to do something called **await** inside of it. 

We will come back to this when we learn about promises later in the course, but now what you need to know is that `for of` loops are very handy for sequencing promises, and that is really the only use case that Wes uses it for. 

The `for of` loop can be used with an array as well. 

Take the following example 👇

```js
for(const number of numbers){
  console.log(number);
}
```

![](../attachments/719.png) 12:06

The downside of the `for of` loop compared to a `forEach` loo is that it doesn't give us the index. It just gives us the raw value. It also doesn't allow us to filter or anything like that.

### `for in` loop

Next we have the `for in` loop, which works similarly. 

Let's use the `numbers` array for this example. 

```js
for(const number in numbers){
  console.log(number);
}
```

![](../attachments/720.png) 12:36

As you can see, we get 0 through 11. 

What is actually happening there is it is giving us the keys of the object. 

`for in` is used for looping over keys of an object. 

Create the following object. 

```js
const wes = {
  name: 'wes',
  age: 100,
  cool: true
}
```

Use the `for in` loop with that object. 

```js
for(const prop in wes){
  console.log(prop);
}
```

![](../attachments/721.png) 13:11

You might be asking, how is that better than using `Object.entries`, `Object.key` or `Object.values`? 

It is not. 

Wes prefers to use those over the `for in` loop, but it is still here if you prefer to use it.

There is one gotcha with the `for in` versus `Object.entries`, which we will demonstrate with an example right now. 

It looks ahead to this thing called **prototypes**. 

Let's make a `baseHumanStats` object as shown below. 

```js
const baseHumanStats = {
  feet:2,
  arms: 2,
  eyes: 2, 
  head: 1
};
```

Create a function `Human` that takes in a `name`, and then within that function add `this.name = name;`. 

This is getting a bit ahead of ourselves, but we can now use this `Human` function to make a `wes2`? 

```js
function Human(name){
  this.name = name;
}

const wes2 = new Human('wes');
```

If you go ahead and take a look at `wes2` by refreshing the page and typing it into the console, you will see that it has a `type` of human with a `name` that is equal to "wes". 

If you were to try typing in  `wes2.arms`, however, you would get `undefined`. 

![](../attachments/723.png) 14:46

However if we take the `Human` function and set the prototype to be the `baseHumanStats` like so 👇

```js
Human.prototype = baseHumanStats;
const wes2 = new Human('wes');
```

If we take a look at `wes2`, it still looks the same, but if you were to look at `wes2.feet` or `wes2.arms`, you will see that it is referencing the values from the prototype. 

![](../attachments/724.png) 15:11

What does that mean?

What happens with a prototype is that when you try to access a property, it first checks on the object itself for a property on that. If it is not on there, it will look up the prototype chain. 

It will say "okay that is not on here, but maybe the thing that created me has a prototype that has that value", and it will look it up.

![](../attachments/725.png) 15:44

In our case this prototype has some sort of base values that it will pull it from. 

We will get into this more when we get into classes but the point of all this is the following.. 

What would happen if you call log `Object.keys(wes2)`? 
Will it log the `name` property only? 
Or will it also log the properties that are on the prototype (feet, arms, eyes, head)? 

![](../attachments/726.png) 16:09

We only get `name`. 

Let's try entries.

```js
console.log(Object.entries(wes2));
```

![](../attachments/727.png) 16:15

We only get the `name` property and value returned to us as you can see above.

Now what would happen if we tried that with a `for in` loop?

```js
for(const prop in wes2){
  console.log(prop);
}
```

![](../attachments/728.png) 16:23

As you can see, it does grab the properties from the prototype that it was made from. 

So, if you need to grab the prototype properties and methods, then you can use a `for in` loop to grab those.

However if you do not need to grab those, you're fine with just using `Object.entries`. 

### `while` and `do while` loops

Next we have the `while` and the `do while` loops. 

These are loops that Wes doesn't use all too often but they are still good to know. 

`while` takes a condition and run infinitely until the condition is false. 

The syntax looks like this 👇

```js
while(){

}
```

Within the parenthesis, we include the condition that we need to check for. 

In our example we will check whether the variable `cool` equals true. If it does, we will log "you are cool".

Now be careful if you run this code because it will cause an infinite loop and might crash your computer. 

```js
let cool = true;
while(cool === true){
  console.log('You are cool');
}
```

![](../attachments/729.png) 17:48

As you can see, that log is happening all the time, just constantly running in the infinite loop we created. 

A `while` loop needs an **exit condition** that will set `cool` to false, or else the condition will never evaluate to false. 

Here is an example of an exit condition we could add 👇

```js
let cool = true;
let i = 1;
while(cool === true){
  console.log('You are cool');
  i++
  if(i > 100){
    cool = false;
  }
}
```

What should happen is after this loop has run 100 times, `cool` will be set to false, and then the condition will evaluate to false and the loop will no longer run.

![](../attachments/730.png) 18:44

As you can see, it ran 100 times before exiting.

It is important to note that someone could set this `cool` variable in another piece of Javascript code and then the next time it runs, it would check whether it is true or false, so that is one way to do it. 

The only different between the `do while` and the `while` loop is that we have a `do` with a block and then a while with a condition on the end, like so 👇

```js
do{

} while()
```

The `do` block will run first, and then it will check the condition after the first run. 

With the `while` loop, the condition will always be checked before the first run. 

While loops are not that popular, but good to know.
