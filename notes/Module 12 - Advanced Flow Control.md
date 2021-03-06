---
attachments: [993.png, 994.png, 995.png, 996.png, 997.png, 998.png, 999.png, 1000.png, 1001.png, 1002.png, 1003.png, 1004.png, 1005.png, 1006.png, 1007.png, 1008.png, 1009.png, 1010.png, 1011.png, 1012.png, 1013.png, 1014.png, 1015.png, 1016.png, 1017.png, 1018.png, 1019.png, 1020.png, 1021.png, 1022.png, 1023.png, 1024.png, 1025.png, 1026.png, 1027.png, 1028.png, 1029.png, 1030.png, 1031.png, 1032.png, 1033.png, 1034.png, 1035.png, 1036.png, 1037.png, 1038.png, 1039.png, 1040.png, 1041.png, 1042.png, 1043.png, 1044.png, 1045.png, 1046.png, 1047.png, 1048.png, 1049.png, 1050.png, 1051.png, 1052.png, 1053.png, 1054.png, 1055.png, 1056.png, 1057.png, 1058.png, 1059.png, 1060.png, 1061.png, 1062.png, 1063.png, 1064.png, 1065.png, 1066.png, 1067.png, 1068.png, 1069.png, 1070.png, 1071.png, 1072.png, 1073.png, 1074.png, 1075.png, 1076.png, 1077.png, 1078.png, 1079.png, 1080.png, 1081.png, 1082.png, 1083.png, 1084.png, 1085.png, 1086.png, 1087.png, 1088.png, 1089.png, 1090.png, 1091.png, 1092.png, 1093.png, 1094.png, 1095.png, 1096.png, 1097.png, 1098.png, 1099.png, 1100.png, 1101.png, 1102.png, 1103.png, 1104.png, 1105.png, 1106.png, 1107.png, 1108.png, 1109.png, 1110.png, 1111.png, 1112.png, loop-animation.gif, loupe-0-timer.gif, loupe-gif.gif, loupe-interval.gif, loupe-multi.gif, submit.gif, typer.gif]
title: 'Module 12: Advanced Flow Control'
created: '2020-05-07T23:18:40.737Z'
modified: '2020-09-18T12:49:24.831Z'
---

- [Module 12: Advanced Flow Control](#module-12--advanced-flow-control)
  * [66 - The Event Loop and Callback Hell](#66---the-event-loop-and-callback-hell)
  * [67 - Promises](#67---promises)
    + [`.then()`](#-then---)
    + [`Promise.all()`](#-promiseall---)
    + [`Promise.race()`](#-promiserace---)
  * [68 - Promises - Error Handling](#68---promises---error-handling)
    + [`Promise.allSettled()`](#-promiseallsettled---)
  * [69 - Refactoring Callback Hell to Promise Land](#69---refactoring-callback-hell-to-promise-land)
  * [70 - Async/Await](#70---async-await)
  * [71 - Async Await Error Handling](#71---async-await-error-handling)
      - [Handling Errors with Higher Order Functions](#handling-errors-with-higher-order-functions)
  * [72 - Async Await Prompt UI](#72---async-await-prompt-ui)
      - [Running an Event Listener Only Once](#running-an-event-listener-only-once)
  * [73 - Async Typer UI - two ways](#73---async-typer-ui---two-ways)

---

# Module 12: Advanced Flow Control 

## 66 - The Event Loop and Callback Hell

Before we get into **promises**, we need to talk about how Javascript is **asynchronous** and how the event loop works. 

You may often hear that almost everything in Javascript is **non-blocking** (asynchronous). What does that mean?

For us to understand that, we need to first talk about how Javascript events work.

Javascript is a **single threaded language**, meaning that only one thing can be run at a time. Some other languages are **multi-threaded**, which means they can run multiple processes at once. 

Because Javascript is single threaded, which means we can only run one thing at a time. 

Let's visualize that with some examples. 

Open up the `event-loop.html` file within the `exercises/` directory. Add two logs within the script tag and then refresh the page to check them. 

```js
console.log('Starting');
console.log('ending');
```

![](../attachments/993.png) 00:58

No one is surprised by that.

Let's add some code in between the two logs. In this demo we want to wait for two seconds, which we could do with a timeout. 

```js
console.log('Starting');
setTimeout(function(){
  console.log('Running');
}, 2000);
console.log('ending');
```

Now if you refresh the page, what will you see? 

You might expect to see starting, running, ending, but instead we get Starting, ending, and then running. 

![](../attachments/994.png) 1:20

Why is that not in the order that we coded it in? Shouldn't the timeout cause the code to pause for two seconds, log running and then log ending?

It doesn't work that way.  The way that Javascript works is it will parse the first line and log Starting. 

Next, it will parse the next few lines which is the `setTimeout()` function. It will say "okay I won't do anything yet but after two seconds I will come back to this code". 
It moves on and logs "ending". 
2 seconds later, the callback that the `setTimeout` function queued up comes back and is executed.  

That is what is referred to as the **call stack**. 

The **call stack** and **event loop** is a pretty complicated thing to understand. 

Instead of Wes trying to explain it, he has some homework for us. 

Philip Roberts has an amazing talk where he explains the event loop. You do not have to watch it before continuing with the course but it's probably one of the most popular Javascript talks ever given and he does an excellent job of explaining the event loop.

https://www.youtube.com/watch?v=8aGhZQkoFbQ 

Philip Roberts also built this cool little tool called _loupe_ which will help us visualize the callstack.

![](../attachments/995.png) 3:23 

We have already looked at the callstack in Javascript and we have seen when you click something, it gives you a trail of what functions were called up to then. 

However we know that the call stack can only ever run one function at a time. 

So what happens in a scenario like our example where you have two logs between a `setTTimeout`? 

![](../attachments/996.png) 3:48

Javascript is asynchronous. 
What that means is that Javascript won't stop running that code, instead if will put it off in what we call the web API, and when that comes back after two seconds, it is going to stick it in the **callback queue**. 

When the call stack has a free second, when it's not currently running anything, it is going to reach into the callback queue, grab the callback and run it for us. 

Let's go ahead and take the code and paste it into the loupe page. 

_Note: at the time Wes is recording the video, the tool is a bit outdated and does not handle arrow functions, or back ticks so just use regular function declarations._

_(Wes is going to modify his timeout to 7 seconds instead of 4 so he can talk to us. Feel free to choose a shorter one for your example)_

![](../attachments/998.png) 4:34

Once you have done that click save and run. 

![](../attachments/loupe-gif.gif)

The first thing that it runs our log. 

![](../attachments/1003.png) 4:51

Next it runs our time out function. 

![](../attachments/1004.png) 4:53

It sees that there is a callback so it puts that in our Web Apis. 

![](../attachments/1005.png) 4:54

When the callback is done waiting, it will stick it into the callback queue. 

![](../attachments/1006.png) 5:00

If the call stack has nothing else to do at the time, it will reach into the queue and grab the next thing.

So the callstack is what Javascript itself is doing.  The Web Apis are things that are waiting or things that we are listening for like event handlers (if we were listening for a click on a button, that would go in our web apis). 

When something happens in the Web Api (like the click of a button or a timer that has finished), it will stick the callback into the callback queue which the call stack will reach into when it has nothing left to do.

Let's say after the `setTimeout` we wanted to add an interval that logs BOOP every 100 milliseconds. Name the function `boop` so we can visualize it more easily. 

![](../attachments/1007.png) 6:07

The first log and `setTimeout` behave just like they did before. When it gets to `setInterval`, we already have a callback for `setTimeout` in the web apis.

![](../attachments/1008.png) 6:12

Then it logs "ending". 

![](../attachments/1009.png) 6:12

Next ,`setInterval` runs. 

![](../attachments/1010.png) 6:13

Now every second you can see that it keeps going back to the `boop` function. 

![](../attachments/1011.png) 6:18


![](../attachments/loupe-gif.gif) 6:26

One thing Wes wants to show us is that even if the `setTimeout` duration was set to 0, you would still get the logs returned in the order of "Starting, Ending, Running". 

```js
setTimeout(function(){
  console.log('Running');
}, 0);
console.log(ending);
```

If you refresh the page and look at the console, you will see that we still get the following...
>Starting
>ending
>Running

![](../attachments/1012.png) 6:40

Even though the timeout happens after 0 seconds, what happens is Javascript runs the first line, then runs the `setTimeout` and queues up the callback to happen after 0 seconds, then it runs the next line and even though the timeout is 0 seconds, it still adds it to the web api which in turn adds it to the callback queue. Because the browser was already busy with the log, it runs the callback after. 

Let's demo that in loupe. 

![](../attachments/loupe-0-timer.gif) 

It logs, runs `setTimeout`, puts running in the web api which puts it in the call back queue, and then when the "ending" log is finished executing, Javascript grabs from the callback queue and runs it. 

As a beginner and intermediate web developer you don't have to understand all the nitty gritty of the call stack and event loop. 

What is really important that you understand is javascript is single threaded, meaning that the callstack can only ever run one thing at a time. 

Let's run the default example on loupe that is supplied to demonstrate what happens when multiple things are queued up. 

The example is in jQuery but it's the same idea. 

When you click a button, we set a timer for 2 seconds that says you clicked me, then it logs "hi" then another timer is set for 5 seconds, and then it logs welcome to loupe.

![](../attachments/1013.png) 8:55

![](../attachments/loupe-0-timer.gif)  

How that works is first the click listener goes on the call stack and gets put into the web apis, then the event listener is added. The hi is run and logged, and after that the timer also gets put in the web apis, and then it logs welcome to loupe. 
Once the timer is finished, it will get moved to the callback queue. 

Now every time we click the button, it sticks an event handler in the queue and you can see the callstack is reaching in and grabbing the next callback to handle itself. 

![](../attachments/1014.png) 9:10

So how do we deal with a scenario in Javascript where we do actually want to wait for something?

Let's say we wanted to go off to an API and grab some data and then come back to it. We shouldn't have to freeze up the entire browser, or we shouldn't have to stop everything else in the browser while that goes and fetches it. Instead what we want is to send off the fetch request and to go and get the data and then carry on with the rest of our life. 
When the data does come back to us, we can deal with it, very similarly to how `setTimeout` will run the callback after the alloted time. 

Callbacks are great, but it is very difficult to orchestrate multiple things at once. 

Let's try with an example. 

What we want to do is make a div and do a few things to it: 
1. change the text to GO when clicked
2. Make it a circle after 2 seconds
3. Make it red after 0.5s
4. make it a square after 0.25 seconds
5. make it purple after 0.3s
6. fade out after 0.3s

That is not an uncommon thing in javascript, where you have to perform some things in a series, one after the other.

What we will do is make a div within the body tag and give it a class of `go`. 

```html
<div class="go">Click Me</div>
```

Comment out all the other code we have in the script tag and let's start with selecting the div and changing the text to go when clicked.

When the div is clicked, we will grab the event and save the div element in a variable `el`. The reason we are saving that in a variable will make sense in just a second.

```js
go.addEventListener('click', function(e){
  const el = e.currentTarget;
  console.log(el);
})
```

![](../attachments/1015.png) 12:02

As you can see, we have the div.  

Let's add some default styling there. Add style tag on the page with some styling. 

```css
.go { 
  margin: $rem;
  background: white;
  background: 5rem; 
  width: 25rem;
}
```

Now when you refresh the page, your button should look like this: 

![](../attachments/1016.png) 12:43

Next we have to make it a circle after two seconds. We can do that by adding a `setTimeout`. 

```js
go.addEventListener('click', function(e){
const el = e.currentTarget;
console.log(el);
setTimeout(function(){
  el.classList.add('circle');
}, 2000);
});
```

Now back in the style tag, let's add a border radius of 50% for the class circle. 

```css
.go.circle {
  border-radius:50%;
}
```

![](../attachments/1017.png)

If you refresh the page you will see that the div style changes to a circle after 2 seconds. 

We forgot to change the text when clicked for step one so right before the `setTimeout` add 👇

```js
el.textContent = 'GO!';
```

Let's put a height on the go CSS style class as well so that it is square. 

![](../attachments/1018.png) 13:38

We can add a transition on there too.

```css
.go { 
  margin: $rem;
  background: white;
  background: 5rem; 
  width: 25rem;
  height:25rem;
  transition: all 0.2s; 
}
```

After 0.5 seconds we need to make it run. Let's add another `setTimeout` to do that.

```js
go.addEventListener('click', function(e){
const el = e.currentTarget;
console.log(el);
  setTimeout(function(){
      el.classList.add('circle');
      setTimeout(function(){
        el.classList.add('red');
      }, 500);
    }, 2000);
});
```

Let's add the follow css styles to the css class red and to purple. 

```css
.go.red {
  background:red;
}

.go.purple {
  background: purple;
  color: white;
}
```

![](../attachments/1019.png) 14:31

Now after 0.25 seconds we need to make it a square. 

```js
go.addEventListener("click", function(e) {
      const el = e.currentTarget;
      console.log(el);
      //1. make it a circle after 2 seconds
      setTimeout(function() {
        el.classList.add("circle");
        //2. make it red after 0.5s
        setTimeout(function() {
          el.classList.add("red");
          //3. make it square after 0.3
          setTimeout(function() {
            el.classList.remove("circle");
          }, 300);
        }, 500);
      }, 2000);
    });
```

Now we need to make it purple after 0.3 seconds.

Add these styles 👇

```css
.go.purple {
  background: purple;
  color: white;
}
```

```js
go.addEventListener("click", function(e) {
      const el = e.currentTarget;
      console.log(el);
      //1. make it a circle after 2 seconds
      setTimeout(function() {
        el.classList.add("circle");
        //2. make it red after 0.5s
        setTimeout(function() {
          el.classList.add("red");
          //3. make it square after 0.3
          setTimeout(function() {
            el.classList.remove("circle");
            //4. make it purple after 0.3s
            setTimeout(function() {
              el.classList.remove("red");
              el.classList.remove("purple");
              //5. fade out after 0.5 seconds
              setTimeout(function(){
                el.classList.add('fadeOut');
              })
            }, 300);
          }, 300);
        }, 500);
      }, 2000);
    });

```

Add this style now 👇

```css
.go.fadeOut {
  opacity: 0;
}
```

![](../attachments/loop-animation.gif) 16:44

That was a really simple animation, but look if you look at the code the way it is now, that is what is referred to as **callback hell**.

Callback hell is when you nest things inside of each other because they all depend on the previous callback to being called before it can then go ahead and run, when you need to run things in sequence, one after the other. It is also rendered to as **"Christmas Tree" code** because of how indented the code is sideways. It's not all that great. 

The solution to call-back hell is the "promise" land. 

Promises are a sort of "I owe you" for something that will happen in the future. They allow us to write code that is much easier to look at. 

We will be looking at that in the next video. 

---

## 67 - Promises

The solution to callback hell is to use a **promise**, and although we haven't covered that yet, we will now. 

Promises are an IOU for something that will happen in the future. 

If you think of our timer, data being returned from an API or someone giving access to a webcam, when we request or start those things, what we often get in return is not the immediate data back, because those things take time. Instead of getting the immediate data returned, we get a promise. 

You can think of a Promise as a little ticket you have in your hand that says "I might get a timer, or some data at some point" and eventually at some point we will get some data back (it can also fail which is called rejecting). 

Or, when we were asking for a user's webcam, like we did in our Face Detection exercises, we used the code below.

```js
const stream = await navigator.mediaDevices.getUserMedia({
  video: { width: 1280, height:720 },
});
video.srcObject = stream;
await video.play();
```

We had to wait for the user to give us access to their webcam before playing the video. That happens all the time in Javascript, and that is what a promise is.

In the `playground` directory, make a `promises.html` file. Add our base HTML and the following script tag. 

```html
<script>
function makePizza(){

}

</script>
```

Inside of this script tag, we are going to make a pizza promise. 

When you make a pizza, it takes time. You can't make it instantly. You gotta put the toppings on, the pepperoni on, and that takes time. 

If you were to order a pizza by phoning them or doing it online, they will immediately give you some sort of order number. That order number is not the pizza -- you cannot eat it, but you know that the order number or that receipt is a "promise" that they will give it to you when its finished. 

So what we need to do is to make a promise and then return it from our function immediately as shown below.

```js
function makePizza(){
  const pizzaPromise  = new Promise();
  return pizzaPromise;
}
```

Promises are made immediately, but they do not resolve immediately (they resolve once the timer is finished or the data comes back). 

That idea of returning happening immediately and resolving happening when it's done is really important. 

A promise takes a callback function, and that callback function is going to give us 2 arguments: 
1. the `resolve` function 
1.  the `reject` function 

The first will always be resolve, second will always be reject. 

Now what you can do is when you are ready, you can resolve the promise or if something went wrong you can reject it, as shown below. 

```js
function makePizza(){
  const pizzaPromise = new Promise(function(resolve. reject){
    resolve('');
  });
  return pizzaPromise;
}
const pizza = makePizza();
console.log(pizza);
```

Now if we refresh the page, what do you think we will get in the console? Will we get the pizza or something else, like a promise?

![](../attachments/1020.png) 4:39

If you refresh the page, you should see the promise. 

What is important to note is that our `makePizza` function doesn't give us the pizza, it gives us the promise of pizza, that at some point in the future, we will either resolve a slice of pizza or reject it if something went wrong.

Let's make the function a bit more robust.

We will take in some toppings and will resolve using backticks. Modify the code as shown below to make a `pepperoniPromise` and a `canadianPromise`.

```js
function makePizza(toppings){
  const pizzaPromise = new Promise(function(resolve. reject){
    resolve(`Here is your pizza 🍕 with the toppings ${toppings.join(' ')}`);
  });
  return pizzaPromise;
}
const pepperoniPromise = makePizza('[pepperoni]');
const canadianPromise = makePizza(['pepperoni', 'mushroom', 'onions'])

console.log(pepperoniPromise, canadianPromise);
```

![](../attachments/1021.png) 6:09

As you can see, we get our 2 promises. But how do we get the actual pizza itself? 

This is a bit confusing because the dev tools will show you the value when it is resolved, but in Javascript if you actually want to access the value of the pizza, you cannot say `pepperoniPromise.value` or anything. 

### `.then()`

The way that we can access it by using the `then()` method, which takes in a callback method. The callback method will pass you the pizza, which we will then log. 

```js
pepperoniPromise.then(function(pizza){
  console.log("Ahh I got it!");
  console.log(pizza);
});
```

Now when you refresh the page you should see the logs below. 

![](../attachments/1022.png) 7:00

At this stage, you might be wondering "why are you doing it like this Wes? this seems like a much harder way to just return data".

The reason for that is we haven't introduced any time delays in our example so let's go ahead and do that. 

We will add a 1 second wait for the pizza to cook using `setTimeout` and then call `resolve` from within that timeout. 

```js
function makePizza(toppings){
  const pizzaPromise = new Promise(function(resolve, reject){
    //wait 1 second for the pizza to cook
    setTimeout(function(){
      resolve(`Here is your pizza 🍕 with the toppings ${toppings.join(' ')}`);
    }, 1000)
    //if something went wrong, we can reject this promise
  });
  return pizzaPromise;
}

const pepperoniPromise = makePizza(['pepperoni']);
pepperoniPromise.then(function(pizza){
  console.log("Ahh I got it!");
  console.log(pizza);
});
```

If you refresh the page, you will see in the console that we get our promise immediately and then a second after we actually have access to our pizza. 

![](../attachments/1023.png) 7:59 

That is a great example of how we sometimes have to wait.

Often what you will see is instead of making a promise and then returning it, people will often just return the promise immediately. 

```js
function makePizza(toppings){
  return new Promise(function(resolve, reject){
    //wait 1 second for the pizza to cook
    setTimeout(function(){
      resolve(`Here is your pizza 🍕 with the toppings ${toppings.join(' ')}`);
    }, 1000)
    //if something went wrong, we can reject this promise
  });
}
```

![](../attachments/1024.png) 8:27

The logic to how a Promise gets resolved is always inside of the Promise body, which in the example is the code below 

```js
function(resolve, reject){
    //wait 1 second for the pizza to cook
    setTimeout(function(){
      resolve(`Here is your pizza 🍕 with the toppings ${toppings.join(' ')}`);
    }, 1000)
    //if something went wrong, we can reject this promise
  }
```

![](../attachments/1025.png) 8:36

That function will resolve or reject whenever it feels ready. In our case, we feel like the pizza is ready after one second.

So what is happening here is when we declare our `pepperoniPromise` we can call `makePizza(['pepperoni'])`, which returns a promise of pizza. In order to get the pizza, the way we can access the resolved value is by chaining a `.then` onto it. 

```js
console.log('Starting');
pepperoniPromise.then(function(pizza){
  console.log('Ahhh got it!');
  console.log(pizza);
});
console.log('finishing');
```

When you refresh the page you will see that we get "Starting" then "finishing" then the "I got it" message. 

![](../attachments/1026.png) 9:21

We will look at how we can use `async/await` to actually do that sequentially if we would like to, but for now we know we can chain a `.then()` onto it.

Why is that any more useful than a regular callback? 

That is useful because let's say we wanted to make multiple pizzas one after the other, and we have an oven that can only cook one at at time. 

Delete our `canadianPizza` and `pepperoniPizza` declaration code and everything below it in the script tag and just leave the line below 

```js
makePizza(['pepperoni']);
```

We can chain a `.then()` immediately onto it (because `makePizza` returns a promise), which gives a function that has a pizza. LLog the pizza so that we know that it still works. 

The neat thing is if from this `then()` we return another `makePizza`, you can then chain another `.then()` on that function. 

```js
makePizza(['pepperoni', 'ham']).then(function(pizza){
   console.log(pizza);
   return makePizza(['ham', 'cheese']);
}).then(function(pizza){
  console.log(pizza);
})
```

As you can see first we get one pizza and then after a second we see the other pizza logged to the console. 

![](../attachments/1027.png) 11:03

You can chain as many as you want. 

Often people like to organize the code so that each `.then()` is on it's own line to make it more readable as you see below.


```js
makePizza(['pepperoni', 'ham'])
  .then(function(pizza){
    console.log(pizza);
    return makePizza(['ham', 'cheese']);
  })
  .then(function(pizza){
    console.log(pizza);
    return makePizza(['hot peppers','onion', 'feta']);
  })
  .then(function(pizza){
    console.log(pizza);
  })
```

Unlike what we were doing the lesson where we were adding and removing classes which were all nested in callback hell, this chaining of `then` is the promise land and it allows us to keep all of our logic one level deep.

The downside to that is if you had a log of First and After all our promise chaining, both logs would execute before any of our pizzas are logged. 

```js
console.log('First');
makePizza(['pepperoni', 'ham'])
  .then(function(pizza){
    console.log(pizza);
    return makePizza(['ham', 'cheese']);
  })
  .then(function(pizza){
    console.log(pizza);
    return makePizza(['hot peppers','onion', 'feta']);
  })
  .then(function(pizza){
    console.log(pizza);
  })
console.log('Right after');
```

![](../attachments/1028.png) 12:26

We will look at how we can use async/await to get around that. 

If you look at the call stack, what we know is that it first runs the function `makePizza(['pepperoni'])` (highlighted in the image below), which immediately returns a promise. 

![](../attachments/1029.png) 12:34

Then it runs the bottom log, before jumping back up to the first `then()` we have when the promise is resolved, and then it keeps going down the promise chain. 

Let's make our `makePizza` function a bit more resilient, starting with `toppings`. 

Set an empty array as the default because sometimes people might order a pizza with nothing on it.

```js
function makePizza(toppings = [])
``` 

For every single topping that is added to the pizza, let's add 200 milliseconds to the initial bake time which is 500. Let's calculate that and save it in a variable as shown below 👇 

```js
const amountOfTimeToBake = 500 + (toppings.length * 200);
```

Now we will take that variable and pass it to our timeout. 

```js
function makePizza(toppings = []){
  const pizzaPromise = new Promise(function(resolve, reject){
    const amountOfTimeToBake = 500 + (toppings.length * 200);
    //wait 1 second for the pizza to cook
    setTimeout(function(){
      resolve(`Here is your pizza 🍕 with the toppings ${toppings.join(' ')}`);
    }, amountOfTimeToBake)
    //if something went wrong, we can reject this promise
  });
  return pizzaPromise;
}
```

![](../attachments/1030.png) 13:35

When we refresh the page and the above code is executed, what should happen is ham and cheese should be logged to the console faster than the pizza with 3 toppings. 

Let's chain 2 more pizzas together, one with no toppings, the other with a lot of toppings.  Then let's resolve that last pizza and just log it using an arrow function as shown below. 

```js
console.log('First');
makePizza(['pepperoni', 'ham'])
  .then(function(pizza){
    console.log(pizza);
    return makePizza(['ham', 'cheese']);
  })
  .then(function(pizza){
    console.log(pizza);
    return makePizza(['hot peppers','onion', 'feta']);
  })
  .then(function(pizza){
    console.log(pizza);
    return makePizza();
  })
  .then(function (pizza) {
        console.log(pizza);
        return makePizza(['one', 'two', 'three', 'four', 'one', 'two', 'three', 'four', 'one', 'two', 'three', 'four']);
      })
  .then(pizza => {
      console.log('All done! here is your last pizza');
      console.log(pizza);
    })
  console.log('Right after');
```

### `Promise.all()`

Let's say we have a big oven and we can make all the pizzas at once. You could run them all **concurrently**, instead of one after another like we are doing (which is referred to as **sequentially**). 

If you have 10 employees and an oven big enough to cook them all at once, you can do it like so 👇

```js
// Run them Concurrently
  const pizzaPromise1 = makePizza(['hot peppers', 'onion', 'feta']);
  const pizzaPromise2 = makePizza(['one', 'two', 'three', 'four', 'one', 'two', 'three', 'four', 'one', 'two', 'three', 'four']);
  const pizzaPromise3 = makePizza(['ham', 'cheese']);
```

So how do we know when all of those promises are done? We could do `.then()` on each of them like so 👇

![](../attachments/1031.png) 16:36

But those are going to pop into the console in whatever order they are done, which isn't what we want. We can instead make it into a "mega promise" that we then wait upon. 

If you have a few promises and all you care about is when all 3 of them are finished, you can make a mega promises, which we will call a `dinnerPromise`. 

```js
const dinnerPromise = Promise.all([pizzaPromise1, pizzaPromise2, pizzaPromise3]);
```

`Promise.all()` is a static method because it lives on the "momma" Promise directly. 

It takes an array of "baby" promises which are `pizza1`, `pizza2`, `pizza3`. 

That makes one big promise which then you can call `.then()` on and we get passed the `pizzas` which we will log. 

```js
dinnerPromise.then(pizzas => {
  console.log(pizzas);
})
```

Now we wait for all 3 to be finished, and we get an array of all 3 of them. 

![](../attachments/1032.png) 17:58

If you wanted the first pizza it would be `pizza[0]`. 

A pretty common thing to do is destructure the pizzas. 

Let's convert the arrow function to a regular function to make it clearer to understand. 

We will use **array destructuring**. Let's call the first pizza `hottie`, second one `garbagePail` and third one `hamAndCheese`. 

Those will now be equal to 3 variables which we can now log or use however we want like so 👇

```js
dinnerPromise.then(function (pizzas) {
  [hottie, garbagePail, hamAndCheese] = pizzas;
  console.log(hottie, garbagePail, hamAndCheese);
}); 
```
![](../attachments/1033.png) 18:58

You do not have to destructure those variables in the body of the function, you can destructure the argument directly with square brackets.

```js
dinnerPromise.then(function ([hottie, garbagePail, hamAndCheese]) {
  console.log(hottie, garbagePail, hamAndCheese);
});
```

That is saying take the first argument and destructure it into a variable named `hottie` , the second one into `garbagePail` and so on.

If you refresh the page you will see it still works. 

To reiterate, `Promise.all()` will take all of your promises and will only resolve when all 3 of the sub-promises have been resolved themselves.

### `Promise.race()`

Similarly there is `Promise.race()`. Let's say someone is really hungry and they will take whichever pizza the first pizza is that is ready because they are very hungry. 

We could do this 👇

```js
const firstPizzaPromise = Promise.race([pizzaPromise1, pizzaPromise2, pizzaPromise3]);
```

Now we can log it. 

```js
firstPizzaPromise.then(pizza => {
  console.log('You must be hungry, here is the first one ready');
  console.log(pizza);
})
```

TO reiterate, `Promise.race()` will wait for the first one to finish rendering. 

![](../attachments/1035.png) 20:46

There are also a couple of other ones which we will get into when we talk about error handling. 

That is a high level overview of promises. 

---

## 68 - Promises - Error Handling

In this lesson we will talk about the opposite of resolving, which is rejecting. 

When a promise goes awry, and you want to bail on it, you can call the reject function. 

Let's go back to our `makePizza` definition and inside of our promise we need to check whether one of the toppings chosen for the pizza is pineapple. 

If it is true, we need to reject the pizza from happening. 

For now will only check for lowercase "pineapple" but we will have to try to weed out people who uppercase it as well later. If that condition is met, then we will call reject and pass it "seriously? get out". 

To do that we will add the code below.

```js
if(toppings.includes('pineapple')){
  reject("Seriously? Get out 🍍");
}
```

Now let's go to the bottom of the script section and comment out the code we added in the previous lesson when we were doing an example on how to run promises concurrently. 

Below that commented out code add the following 👇

```js
makePizza(['cheese','pineapple']).then(pizza=>{
  console.log(pizza);
})
```

![](../attachments/1037.png) 1:55

What does that log "Uncaught (in promise)" mean? 

It means that there was an error in one of our promises, but we did not write any code in order to handle that error and try to catch it. 

The way you catch an error in a promise is you chain a `.catch()` to it. 

Catch will pass you the error as a parameter which we will use to log the error as shown bel;ow. 

```js
makePizza(['cheese','pineapple']).then(pizza=>{
  console.log(pizza);
}).catch(err=>{
  console.log('Oh noooo!!');
  console.log(err);
})
```

As you see, we no longer get an error logged because we caught and logged the error ourselves.

![](../attachments/1038.png) 2:24

`.then()` will only run when the promise resolves successfully, and the catch will only run if the promise doesn't go successfully.

Almost always with your promise built functions you must chain a `.then()` and a `.catch()` at the end so that if anything goes wrong, you are able to catch it and display it to the user.

What Wes will usually do is make a function called `handleError` which will take in the error and log it like so 👇

```js
function handleError(err){
  console.log('Oh noooo!');
  console.log(err);
}
```

Now instead of catching the error using the code we had before we can simply replace it as shown below 👇

```js
makePizza(['cheese','pineapple']).then(pizza=>{
  console.log(pizza);
}).catch(handleError);
```

In the code above we are passing the reference to the function which will then handle the error.

It's important to note that not every single promise needs a catch on the end.  

Go back to our pizzas where we chained a bunch of promises together and modify the pizza with no toppings to instead pass the topping of "pineapple", 

![](../attachments/1040.png) 3:59

What happens there is we go through the chain of promises and then as soon as we hit the code where we try to make a pizza with a pineapple we get the "uncaught in promise" error. 

![](../attachments/1041.png) 4:06

So how do we catch the error? 

Does it mean we have to add a `catch` after each `then`? That would be annoying. 
Thankfully, the answer is no. 

You just need to put one catch at the very end that will be able to handle our error. 

![](../attachments/1042.png) 4:31

The thing about an error happening in a promise chain is that where the error happens, it will then bail out of executing the rest of the promise chain. 

If you have 7 or 8 steps in the promise chain and they are all dependent on one another, then that is good because if step 3 in the breaks, you don't want to continue to step 4.

But sometimes you want to continue even if one of the promises fails. If that is the case, then promise chaining is not what you want to use. Instead, you'd want to use some of the other Promise static methods like `Promise.all()` or `Promise.race()`.

Let's do an example. We will start with 2 pizzas. 

```js
const p1 = makePizza(['pep']);
const p2 = makePizza(['pineapple']);
```

### `Promise.allSettled()`

We will use a new API that we haven't learned yet called `Promise.allSettled()`.

Let's start by making a mega promise.

```js
const dinnerPromise2 = Promise.allSettled([p1, p2]);
```

Let's just get the results and log them for now. 

```js
dinnerPromise2.then(results=> {
  console.log(results)l
})
```

![](../attachments/1043.png) 6:17

As you can see in our results we can see that the first one was **fulfilled** and the second one was **rejected**. 
Fulfilled is another word they use for resolved.

If we tried that example but with `Promise.all()` like so, you will see that the code will break. 

```js
const dinnerPromise2 = Promise.all([p1, p2]);
```

![](../attachments/1044.png) 6:39

That is because `Promise.all` assumes that all of them will go successfully. 

If you want to catch any errors that happen in `Promise.all()` you would have to catch them like so 👇

```js
const dinnerPromise2 = Promise.all([p1, p2]).catch(handleError);
```

![](../attachments/1045.png) 7:02

That is probably not what you want because if one of them breaks, you might still want the other one, because those other pizzas are still good. 

`Promise.allSettled()` will tell you when all the promises are done, regardless of whether they were rejected or resolved.

There are a few more error handling techniques that we need to use but they do not get introduced until we learn **async/await**. 

Let's go back and refactor the last exercise we did to use promises instead of callback hell.

---

## 69 - Refactoring Callback Hell to Promise Land

In this lesson we will go back to the event loop example, where we added the classes of `circle`, `purple` and `fadeout`, and we will refactor it to use promises instead.

![](../attachments/1046.png) 00:13

We will be coming back to this example one more time and refactor it after we learn `async/await`.

Take out `event-loop.html` file, duplicate it and rename it as `promise-chain.html`.

The first thing we want to do is make a function that will simply wait for a certain amount of time. This is something Wes does in almost every single project because it is such a common thing.

Make a function called `wait` which will take in the number of milliseconds we want to wait using the parametetr `ms`, which we will default to 0 seconds, and then we will return a new promise which will resolve after the number of milliseconds that got sent in.

Then we will just test our new method by waiting 2 seconds (2000 milliseconds) before logging "DONE".

```js
function wait(ms = 0){
  return new Promise(function(resolve){
    setTimeout(resolve, ms);
  });
}

wait(200).then(()=>{
  console.log('Done');
})
```

Now if you refresh the page, after 2 seconds you should see "done" logged to the console.

![](../attachments/1048.png) 2:03

That is such a common thing that Wes actually has an npm package called **Waait** which gets around 75k downloads per week and all it does is return a promise that resolves after a certain number of milliseconds that have been passed in. 

We can use the implicit return and arrow function to refactor the `wait` function as shown below to be on one liner 👇

```js
const wait = (ms = 0) => new Promise(resolve =>  setTimeout(resolve, ms));
```

Now that we have this `wait` function, we can start to tackle all the callback hell.

Let's just rewrite it starting at the beginning by taking all our `setTimeouts` and instead making them promise based.

The first thing we will do is make an external function called `animate` and when someone clicks the go button, we will run `animate`. 

`animate` will take in the event and let's start moving logic up to it. 

For the event listener we already had on `go`, we will replace `click` with `clickXXXXX` so it doen't actually trigger and we can refactor piece by piece.


```js
function animate(e){

}
go.addEventListener('click', animate);

go.addEventListener('clickxxxx', function go(e){

})
```

The first thing we want to do is grab the element, then we want to change the text to "GO" when clicked, which is immediately so we can put it right into our animate function. 

```js
function animate(e){
  const el = e.currentTarget;
  //1. change the text to GO when clicked
  el.textContent = 'GO';
}
```

Now we want to make it a circle after 2 seconds so we can use the `wait` function we made. We will chain a `.then()`, although there is no piece of data that is resolved from the wait, it simply is just done. 

```js
function animate(e){
  const el = e.currentTarget;
  //1. change the text to GO when clicked
  el.textContent = 'GO';
  wait(200).then(()=>{
     el.classList.add('circle');
  })
}
```

Now after 2 milliseconds, the GO square will turn into a circle. If you refresh the page, you will see it still works.

![](../attachments/1049.png) 6:11

Now how do we make it red after 0.5 seconds? 
We cannot just call it after the wait function because that will cause it to go red before it goes to circle.

What we can do instead is we can return another `wait()` of 500 milliseconds and then chain another  `.then()` onto it and put our third item in there, as shown below. 

```js
function animate(e){
  const el = e.currentTarget;
  //1. change the text to GO when clicked
  el.textContent = 'GO';
  //2. make it a circle after 2 seconds
  wait(200).then(()=>{
     el.classList.add('circle');
     return wait(500);
  }).then(()=>{
    //3. make it red after 0.5 seconds
    el.classList.add('red');
  })
}
```

To make this more readable you can format them each on their own line like so 👇

```js
function animate(e){
  const el = e.currentTarget;
  //1. change the text to GO when clicked
  el.textContent = 'GO';
  //2. make it a circle after 2 seconds
  wait(200)
  .then(()=>{
     el.classList.add('circle');
     return wait(500);
  })
  .then(()=>{
    //3. make it red after 0.5 seconds
    el.classList.add('red');
  })
}
```

Now we have to make it a square after 0.25 seconds by removing the class of circle.  

```js
.then(()=>{
  //3. make it red after 0.5 seconds
  el.classList.add('red');
  return wait(250);
})
.then(()=>{
  el.classList.remove('cirlce');
})
```

Now after 500 milliseconds we want to remove the red class and add the purple one like so 👇

```js
.then(()=>{
  //3. make it red after 0.5 seconds
  el.classList.add('red');
  return wait(250);
})
.then(()=>{
  el.classList.remove('circle');
  return wait (500);
})
.then(()=>{
  el.classList.remove('red');
  el.classList.add('purple');
})
```

Now finally, after half a second, we need to make it invisible.

```js
.then(()=>{
  el.classList.remove('red');
  el.classList.add('purple');
  return wait(500);
})
.then(()=>{
  el.classList.add('fadeOut');
})
```

So what we have done here is taken the nested callback function and made it one level deep, which is waiting returning, waiting returning. That is chaining multiple `.then()`s onto each other.

That gets much better when we get to `async/await` but for now, this is the best way we can refactor these promises into a promise chain. 

---

## 70 - Async/Await

Although in the last lesson we refactored our callback hell example to use promises, the syntax still isn't that great because we are nesting at least one level deep inside of callback hell with the `.then()` syntax. 

`async/await` is a new syntax that will allow us to use the keyword `async` and the keyword `await` for a much nicer, easier to read looking code and we will see how that works in just a second. 

Your functions that return promise still stay exactly the same way. There is nothing that needs to change about your promise generating functions. We need to change where we actually call the code to use `async/await`. 

Go into the `playground` folder and make a new file called `async-await.html` and add our base HTML. 

Add a script tag and create that wait function we have built a few times now. 

```html
<script>
function wait(ms = 0){
  return new Promise((resolve)=>{
    setTimeout(resolve,ms);
  })
}

</script>
```

Now if we want to use the `async await` syntax there are a few things that need to happen. 

First of all, you can only use `async await` inside of a function that is marked as `async`. 

Make a function `go()` which logs "starting", and "ending". In order to make it wait for two seconds between the logs, you would add the following code 👇

```js
function go(){
  console.log('Starting');
  wait(2000);
  console.log('Ending');
}
go();
```

Now we know if we run `go` on page load, we will get "starting" and "ending" immediately. 

![](../attachments/1050.png) 2:32

What async await allows us to do is put the keyword `await` in front of a promise based function and it will sort of temporarily pause that function from running until that promise is resolved. 

```js
function go(){
  console.log('Starting');
  await wait(2000);
  console.log('ending')
}
go();
```

If you modify the code as shown above and then refresh the page, you will see an error in the console.

![](../attachments/1051.png) 2:52

>Uncaught SyntaxError: await is only valid in async function

To fix this, we need to mark our function as `async`. That tells the code that somewhere inside of the function, we will be doing some awaiting. 

Mark the function `async` as shown below. 

```js
async function go(){
  console.log('Starting');
  await wait(2000);
  console.log('ending');
}
```

Now if you go ahead and save the function and then refresh, we will getting "starting" logged to the console and then two seconds later we will get "ending".

That is beautiful because we achieved that without chaining a bunch of `.then()` . 

If we wanted to wait for another period of time in the same function before executing something else, we can.

```js
async function go(){
  console.log('Starting');
  await wait(2000);
  console.log('running');
  await wait(200);
  console.log('ending');
}
```

![](../attachments/1052.png) 3:51

We are now able to just stick these calls to our `wait` function wherever we want within our `go` function and the execution of that function will temporarily pause until the promise has been resolved.

Marking functions as `async` can work with any type of function.

Let's go over all the functions just to demonstrate. 

You can add `async` to a function declaration as shown below 👇

```js
// Function Declaration
async function fd(){}
```

You can also mark an arrow function as async 👇

```js
//arrow function
const arrowFn = async () => {}
```

You can also mark callback functions async. 

For example, if you had an event listener, you could make the callback function async as shown below 👇

```js
window.addEventListener('click', async function(){

})
```

You cam also make methods async.

```js
const person = {
  sayHi: async function(){

  }
}
```

You can also mark methods async using the method shorthand and function property, as shown below. 

```js
const person = {
  //method
  sayHi: async function(){

  },
  //method shorthand
  async sayHello(){

  },
  //function property
  sayHey: async () => {

  }
}
```

Essentially whenever you have a function, put the word `async` in front of it and that will allow you to do awaiting inside of it. 

You cannot do what is referred to as top level await. 

If you go take the code within the go function and try to run it directly in the script tag and try calling `wait` as shown below, it will not work 👇

```js
console.log('one');
await wait(200);
console.log('two');
```

We get an error in the console.

>Uncaught SyntaxError: await is only valid in async function

![](../attachments/1053.png) 6:24

You can however copy and paste the call to the wait function and call it directly from devtools console. 

Let's take a look at some other examples.

Go to our `promises.html` file that we have and let's grab the `makePizza` function, and move it over to the `async await` file. 

Both of those functions return a promise.  

![](../attachments/1054.png) 7:48

Go to the bottom of the script tag and make another async function `makeDinner`. 

Within that function we will call `makePizza` to make `pizza1` and then we will log it. 

```js
async function makeDinner(){
  const pizza1 = makePizza(['pepperoni']);
  console.log(pizza1);
}
makeDinner();
```

If you comment out the `go` function and the code where we call `go` and instead just run the code we added right above, you will see that we get a promise logged to the console. 

![](../attachments/1055.png) 8:43

That is because we are running the function and storing it in a variable, which will store the promise in the variable. Note that we call it "await" instead of "wait" because it is asynchronously waiting. Meaning it won't actually pause all of javascript, it's not going to block the rest of the javascript from running. 

If we instead put an `await` in front of our `makePizza` function, we will asynchronously be waiting for the pizza to be done, and when it is, we will simply log it.

```js
async function makeDinner(){
  const pizza1 = await makePizza(['pepperoni']);
  console.log(pizza1);
}
makeDinner();
```

![](../attachments/1056.png) 9:44

Similarly we can do that with pizza2 as well. 

```js
async function makeDinner(){
  const pizza1 = await makePizza(['pepperoni']);
  console.log(pizza1);
  const pizza2 = await makePizza(['mushrooms']);
  console.log(pizza2); 
}
makeDinner();
```

![](../attachments/1057.png) 9:58

Now let's say we want to wait for both of those to be done because the way it is coded right now could be possibly inefficient. 

This is what is referred to as a **foot gun** in the industry, when you give somebody the tools it is possible they could write code that is not performant. 

What that means is if you are making a pepperoni and a mushroom pizza, the way we have coded it, you have to wait for the pepperoni pizza to be created, baked and taken out before we even start making the next pizza. 

It is likely that we could be making the pizza's concurrently, so what we can do is instead of waiting for one, then moving onto the next line and making the next one, we will remove the await from both of them, make them both into promises and then make one big promise which we can await. 

```js
async function makeDinner(){
  const pizzaPromise1 = makePizza(['pepperoni']);
  const pizzaPromise2 = makePizza(['mushrooms']);
  const pizzas = Promise.all([pizzaPromise1, pizzaPromise2]);
  console.log(pizzas);
}
```

If you do it like above, we will still only get the big promise. 

![](../attachments/1058.png) 11:18

We need to modify the code to await the mamma promise like so 👇

```js
const pizzas = await Promise.all([pizzaPromise1, pizzaPromise2]);
```

![](../attachments/1059.png) 11:29

Now we get the actual pizzas instead of just the promises. Go ahead and destructure the two pizzas that are returned.

```js
const [pep, mush] = await Promise.all([pizzaPromise1, pizzaPromise2]);
console.log(pep, mush);
```

![](../attachments/1060.png) 11:46

What we want to do now is go back to the code that we wrote early on with our promise chain and rewrite it one more time into async await. 

![](../attachments/1061.png) 12:15

Take the entire animate function and copy it and rename it to `animate2`. 

Modify the click event to call `animate2` as shown below.

```js
go.addEventListener('click', animate2);
```

Go back to the `animate2` function. 

The first thing you need to do is mark the function as `async` and then to check that it still works. 

```js
async function animate2(e){
```

Open it up in the browser to make sure that it still works. Then refactor the animate function to instead await as shown below. 

```js
async function animate2(e) {
  const el = e.currentTarget;
  // 1. Change the text to GO when clicked.
  el.textContent = 'GO';
  // 2. Make it a circle after 2 seconds
  await wait(200);
  el.classList.add('circle');
  await wait(500);
  el.classList.add('red');
  await wait(250);
  el.classList.remove('circle');
  await wait(500);
  el.classList.remove('red');
  el.classList.add('purple');
  await wait(500);
  el.classList.add('fadeOut');
}

function animate(e) {
  const el = e.currentTarget;
  // 1. Change the text to GO when clicked.
  el.textContent = 'GO';
  // 2. Make it a circle after 2 seconds
  wait(200)
    .then(() => {
      el.classList.add('circle');
      return wait(500);
    })
    .then(() => {
      // 3. Make it red after 0.5s
      el.classList.add('red');
      return wait(250);
    })
    .then(() => {
      el.classList.remove('circle');
      return wait(500);
    })
    .then(() => {
      el.classList.remove('red');
      el.classList.add('purple');
      return wait(500);
    })
    .then(() => {
      el.classList.add('fadeOut');
    })
}
```

As you can see in `animate2` there are no `.then()` and no callbacks, we simply just pause the function from running with our `await` in front of a function that returns to us a promise. 

In the next video we will look at how to handle errors with `async await` and we will go over a lot of the browser APIs that come with `async await`.

---

## 71 - Async Await Error Handling

We will talk about error handling strategies for `async await` in this lesson. 

Because there is no `.then()` that we are chaining on with promises, it's not as easy as just chaining a `.catch()` onto the end of a promise chain in order to deal with what is going on. 

We will cover 4 different ways that you can do error handling in `async await`, and then Wes will explain which approach he would use in which scenarios. 

Go into our playground and copy the `async-await.html` file and rename it to `async-await-error-handling.html`. 

Go and delete everything except for these two functions: `wait` and `makePizza`. 

```html
<body>
<script>
function wait(ms = 0) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  })
}

function makePizza(toppings = []) {
  return new Promise(function (resolve, reject) {
    // reject if people try with pineapple
    if (toppings.includes('pineapple')) {
      reject('Seriously? Get out 🍍');
    }
    const amountOfTimeToBake = 500 + (toppings.length * 200);
    // wait 1 second for the pizza to cook:
    setTimeout(function () {
      // when you are ready, you can resolve this promise
      resolve(`Here is your pizza 🍕 with the toppings ${toppings.join(' ')}`);
    }, amountOfTimeToBake);
    // if something went wrong, we can reject this promise;
  });
}
</script>
</body>
```

In our `makePizza` function, we know that if it includes pineapple, it will reject because there is an error. 

Go below the `makePizza` function declaration and we will make a function `go()`, which will make one pizza with the topping pineapple, and then we will call the function right below, like so 👇

```js
function go(){
  const pizza = makePizza(['pineapple']);
}
go();
```

If you refresh the page, you will see we get an error. 

![](../attachments/1062.png) 1:32

If you try to log `pizza` within the `go` function, we don't get anything, we do not even get the error logged. 

There are 4 ways that we could handle that. 

The first 2 are with `try` and `catch`. 

**try and catch** in Javascript is basically what the name suggests. You try a bunch of stuff and you wrap it in a safety blanket and then if anything goes wrong, you catch the error and handle it.

You would use a try and catch inside the go function like so 👇

```js
async function go(){
  try{
    const pizza = await makePizza(['pineapple']);
    console.log(pizza);
  } catch(err){
    console.log('Ohhhh nooo!');
    console.log(err);
  }
}
```

Now if you refresh the page, you should see the following..

![](../attachments/1064.png) 2:56

What happened is any code inside of the try block is in the safe zone. It won't break the entire application if some of the code within the try errors out. Instead, it will just fail over to the `.catch()`. 

That works with anything, not just async await.

If we tried calling a function that doesn't exist such as `window.doesNotExist()`, you will see we still get the errors for that. 

![](../attachments/1065.png) 3:28

One downside to this is the syntax messes up the beautiful async await syntax because you have to wrap everything inside of the try and catch. 

The benefit to that is you can have multiple promises.

For example, if we tried to make multiple pineapple pizzas, if either one failed, it would be caught by the same try/catch. 

Another way we can do that is using what Wes refers to as "mix and match", meaning that we can use async/await but use the promise syntax for error handling.  

Let's go and get rid of the try/catch we just added all together. 

Instead, lets make a function `handleError`. 

```js
function handleError(err){
  console.log('Ohhhh nooo');
  console.log(err);
}
```

Normally within function like `handleError` you would want to display the error in the UI to your user, send it off to an error handling service to log it, or something like that so you know what is going on, on the clients side. 

In our case, we are just logging "Oh no!" and get the error. 

What we can do is now chain a `.catch()` to the end of our `makePizza` call from within our async `go` function and pass it reference to `handleError`. 

```js
async function go(){
  const pizza = await makePizza(['pineapple']).catch(handleError);
  console.log(pizza);
}
```

Now when it runs, it will give us "oh nooo. Seriously? get out" and then logs undefined.

![](../attachments/1066.png) 4:52

We are sort of mix and matching to get the best of both worlds. We are using await to get the data from the promise instead of using the `.then()`. But we are still using the other syntax which is adding a `.catch()` onto the end of the function. 

That approach is helpful when you want to handle the error at the time that you define the function, so you handle it inside of the function. 

Sometimes you want to handle the error when you call the actual function. 

If that is the case, we wouldn't handle it inside of the definition, but we would go down to where we call our async function and chain a `.catch()` onto there. 

Look at the following example below 👇

```js
function handleError(err){
  console.log('Ohhhh nooo');
  console.log(err);
}

async function go(){
  const pizza = await makePizza(['pineapple']).catch(handleError);
  console.log(pizza);
}

go.catch(handleEror);
```

![](../attachments/1067.png) 5:45 

When you refresh the page you will see that the exact same thing just happened. 

What is interesting about that is you can also catch things that are unrelated. 

For example if within our `go()` function we call another function that does not yet exist, it will catch that error as well. 

```js
async function go(){
  window.doesNotExist();
  const pizza = await makePizza(['pineapple']).catch(handleError);
  console.log(pizza);
}
```

You might be saying to yourself "Wes, you said that `.then()` and `.catch()` can only be used on functions that return a promise, but here you are using a `.catch` on a function that does not return a promise". 

`go()` doesn't return a promise, does it?

Let's check by returning pizza from the function as shown below. 

```js
async function go(){
  const pizza = await makePizza(['pineapple']).catch(handleError);
  console.log(pizza);
  return pizza;
}
const result = go().catch(handleError);
console.log(result);
```

What will the result be? Will we get the pizza? Will we get nothing? 

![](../attachments/1069.png) 6:43

We get a promise! Whaaaaat?! 

This is a very important thing about promises in `async await`. 

When you mark a function as `async`, it will immediately return a promise to you. 
When a function is not marked with `async`, it is a regular function that will return the data that you want. 

What is possible is that you can `await` `async` functions as well, because they in themselves are promises. So you could do something as shown in the code below. 

```js
go().then(result => {
  console.log(result);
}).catch(handleError);
```

![](../attachments/1070.png) 7:35

In that example it went straight to catch. 

But if instead we were making a pepperoni pizza and modified the topping to be pepperoni instead of pineapple, then we would actually get access to the pepperoni pizza. 

![](../attachments/1071.png) 7:42

Asynchronous functions will always return a promise themselves, which means we can use the `.catch()` or the `.then()` syntax on the `async` functions if we want. 

Why is that useful? 

You often have a function with a few promises inside of it, but then you want to wait for that entire function to finish returning it's data.  If that is the case, you use a `.then().catch()` or an `await()` on it.

Similarly, we do something as shown below 👇

```js
async function go(){
  const pizza = await makePizza(['pineapple']).catch(handleError);
  console.log(pizza);
  return pizza;
}

async function goGo(){
  const result = await go();
}

goGo();
```

If you refresh the page and run that, you will get an error. 

![](../attachments/1072.png) 8:56

How would you then handle that? 

```js
goGo().catch(handleError);
```

![](../attachments/1073.png) 9:09

As you can seem by chaining a `.catch()` onto it, we handle the error. 

You can nest promises as deep as you want and it is pretty common to have a good number of your functions marked as `async` and sort of have promises happening inside of promises. We will get into a lot more examples of that, so that might be a little confusing to you. 

Let's bring the examples back to `go().catch(handleError)`. 

That is the approach that Wes uses most often. It's sort of the best of both worlds. You can use the `await` like you want, and then you can catch them at call time.

The only difference would be calling `.catch()` inside of `go()`, like so 👇

```js
async function go(){
  const pizza = await makePizza(['pineapple']).catch(handleError);
}
```

That is useful if you need to do something with the error inside the function like display a special modal at the time of definition, rather than at the time of call.

#### Handling Errors with Higher Order Functions

The last way to handle an error with async/await is called a **higher order function**.We have talked about this a couple of times now. 

A higher order function is a function that returns another function. 

The way it works is you go ahead and define all of your functions, just as if you were never to have any errors. (That is the way Wes typically likes to write his code, he will write them as `async` functions and he doesn't worry about error handling inside of those functions.) 

When it comes time to calling that function, you have two options. You can catch it at run time like `go().catch(handleError)` or you can make a safe function with a higher order function. 

Create a higher order function, `makeSafe` that takes in 2 parameters:
1. The function that we want to make safe
2. The function we want to be responsible for handling the error 

What this function will do is it will return another function which then calls our original function and chains the `.catch()` onto the end. 

This might not make sense to you, it didn't make sense to Wes for years, so don't sweat it if that's confusing. 

```js
// make a safe function with a HOF
function makeSafe(fn, errorHandler){
  return function(){
    fn().catch(errorHandler);
  }
}
```

If we just tried calling `go()` we would get an exception. 

But if we instead call `go` by first wrapping it in the `makeSafe(go)` function, as shown below, it will handle the error gracefully. 

```js
const safeGo = makeSafe(go, handleError);
safeGo();
```

That is because `makeSafe` takes in a function, and then returns a new function that is just your original function with a `.catch()` tacked onto the end of it.  
![](../attachments/1074.png) 12:28

Now we have the function `safeGo` now that we can just call it without worrying about anything.

![](../attachments/1075.png) 12:41

That works just fine.

Why would that be better than catching it like we were with `go().catch(handleError)` ? 

More often than not, Wes has a function like `safeGo` or a function that does a specific task, and he uses that like 30 different times throughout his application. If he has to write the code to handle the error 30 different times, that is pretty cumbersome.  

What you can do instead is make the safe function once (using `makeSafe` in our example),  and then you can carry the safe function and run it whenever you want, knowing the error handler will have been attached on. 

Those are a couple of different options you can use. 

Wes most often catches errors at run time using `go().catch(handleError)`, and then when he is in Node/Express land, he tends to reach for a higher order function.

---

## 72 - Async Await Prompt UI

In this lesson we will be working more with promises and async await to build a sort of prompt interface. 

A pretty common thing to do in Javascript is when someone clicks a button or something happens on the page, you want to pop up a little box, ask them for something, and then go ahead and get that data back and display it on the page somehow. 

![](../attachments/1076.png) 00:17

There is a prompt that is built into the browser, but the problem with that prompt if you can only have one input box. 

If you wanted multiple input boxes or an image upload or something like that, you couldn't do that with the built in. 

The built-in interface is also blocking, meaning that when it is popped up, you cannot do anything else on the page. 

We are going to see how we can re-implement this with promises and async/await.

We will be working out of the `/exercises/72 - Async Prompts/` directory, and are starting with some very basic HTML. 

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Async Prompt</title>
  <link rel="stylesheet" href="../../base.css">
  <link rel="stylesheet" href="./style.css">
</head>

<body>

  <div class="wrapper">
    <button class="askMe" data-question="What is your name?">Enter Name</button>
    <button class="askMe" data-cancel data-question="What is your age?">Enter Age</button>
  </div>
  <script src="./scripts.js"></script>

</body>

</html>

```

We also have some CSS that Wes will explain to us because we will be using CSS variables for animation, which is pretty nifty. 

```css
.popup {
  background: hsla(0, 0%, 30%, 0.5);
  position: fixed;
  height: 100vh;
  width: 100vw;
  transition: all 0.25s;
  top: 0;
  display: grid;
  justify-content: center;
  align-items: center;
  pointer-events: none;
  --opacity: 0;
  opacity: var(--opacity);
}

.popup fieldset {
  background: var(--grey);
  padding: 2rem;
  border: 3px solid var(--pink);
  border-radius: 5px;
  box-shadow: var(--box-shadow);
  transition: all 0.2s;
  --scale: 0.3;
  transform: scale(var(--scale));
}

.popup.open {
  --opacity: 1;
  pointer-events: all;
}

.popup.open fieldset {
  --scale: 1;
}
```

The buttons on the HTML page are there so that when you click them, they will invoke the prompt.

One more thing we will look at is how to open one prompt after the other and get all three pieces of data back, which is going to be in a **synchronous map**. 

That is pretty tricking to do, so Wes will show us how to do that, how to run something in series when you have promises in async/await.

Open up `scripts.js` in your code editor and open up `index.html` in the browser.

Let's get going on the javascript in our script file. 

Let's start by creating a function, `ask` which will take in some options. 

The options will be 2 things: 
1. What will the text for the prompt be?
2. Are they allowed to cancel it with a cancel button?

Inside of the function we want to first return a new promise. 

Inside of that promise we will have a function that will accept `resolve` as the first argument. (It also accepts `reject`, but we won't be rejecting it in this example.) 

When somebody hits cancel, we will just resolve it with nothing instead of reject because that is how the one built into the browser works.

```js
function ask(options) {
  // First we need to create a popup with all the fields in it
  // check if they want a cancel button
  // listen for the submit event on the inputs
  // when someone does submit it, resolve the data that was in the input box!
  // insert that popup into the DOM
  // put a very small timeout before we add the open class
}
```

Now there are a couple of things that need to happen.

First, we need to create a popup with all the fields in it. 

Then we need to check if they want a cancel button.

Next we need to listen for a submit event on the input, and then when someone does finally submit it, we need to resole the data that was in the input box. 

Let's start sequentially with the popup. 

We will use a form tag for this so we can get the submit. 

Use `document.createElement` because that will immediately return to us a DOM node, which allows us to add event listeners for things like submit on it. 

If we just used backticks and a form tag, we wouldn't be able to add event listeners inside of the function. We would have to wait until that thing was put into the page before we could add event listeners to it. 

```js
const popup = document.createEElement('form');
```

Now we can add a class of `popup` to it, which just makes sure it has position of fixed, a specific background color, that the width and height are 100 percent of the viewport width and height. 

We set the opacity to 0 because we want to fade it in which we will do using a class of open.

```js
popup.classList.add('popup');
```

Now we need to put some HTML inside of the popup. 

We will use backticks in this case because there is nothing inside of it that needs an event listener added to it.  

```js
popup.insertAdjacentHTML('afterbegin', `
  <fieldset>
    <label>${options.title}</label>
  </fieldset>
`)
console.log(popup);
```

Refresh the page to check whether the code still works. 

Call `ask` directly from the console, and pass in an options object as an argument with 1 property in the option, the title.

```js
ask({title:'does this work'});
```

![](../attachments/1077.png) 7:15

As you can see, we have the form, with a fieldset and label containing the title so we know that it works so far.

Now let's check if they want a cancel button using the options object, and if they do, go ahead and create that button. 

You must specify the type of the button or else the browser will just assume it is a submit button and submit the form. 

We also need to listen for a click on the cancel but for now, just add a TODO and come back to that later to keep things more simple. 

```js
if(options.cancel){
  const skipButton = document.createElement('button');
  skipButton.type = 'button';
  skipButton.textContent = 'Cancel';
  //TODO: listen for a click on that cancel button
}
```

We still need to listen for the submit event on the inputs, and resolve the data that was entered into the input box and we need to insert that popup into the DOM.

Let's do that last step first. 

```js
document.body.appendChild(popup);
```

![](../attachments/1078.png) 9:25

Let's get that popup showing up so we have a visual. 

If you go to our CSS, you will see that we have opacity of 0 on the `popup` class. 

The reason Wes has created a **CSS custom property** (or variable as it is referred to in CSS) to store the opacity value which we can then reference using the variable. 

![](../attachments/1079.png) 9:43

Now when we go to the popup with class of `open`, it will know to update the value of the opacity variable everywhere that it is used.

So right after we append our child, we need to take the popup's class list and add a class of `open`. 

```js
document.body.appendChild(popup);
popup.classList.add('open');
```

When we click it, as you see, it is not fading itself in, which is a bit of a problem. That is back to the whole event loop that we talked about a few videos ago. 

![](../attachments/1080.png) 10:20

The reason it is not animating itself in is because it queues up the "add a class of `popup`" and "add a class of `open`" sort of at the same time. 

There is no time for it to transition from regular popup `opacity:0` to popup open `opacity: 1`. There is no A to B to transition itself from one to another.

The solution there is to put a very small timeout before we add the `open` class. 

That will stick the code that is beyond it at the end of the event loop and that is enough to give A and B a little time to transition itself. 

Let's add a timeout of 10 milliseconds and then add the class of `open`.

```js
document.body.appendChild(popup);
//put a very small timeout before we add the open clicks
setTimeout(function(){
  popup.classList.add('open');
}, 10);
```

Sometimes you can even get away with doing a 0 second timeout. 

Why does that work?

As we learned earlier how the event loop works is that when you have a timeout, it runs it, then sticks the callback in the Web APIs which puts it in the queue, and then the event loop will pull it back. 

Sometimes you will see this where somebody puts something at a timeout of 0. All that is doing is it puts that at the end of the event loop so that the other code finishes running by the time we add our class list of open. 

Wes has tested that in a few browsers but it doesn't work too great, so let's change it to 50 milliseconds instead of 0. 

```js
setTimeout(function(){
  popup.classList.add('open');
}, 50);
```

Now one thing we can do is instead of using `setTimeout`, we could use `async/await`. 

Let's code that `wait` function again.

```js
function wait(ms = 0){
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

Go back to where we had added the timeout and replace it instead with the code below. 

```js
document.body.appendChild(popup);
//put a very small timeout before we add the open clicks
await wait(50);
popup.classList.add('open'); 
```

You might notice your code editor yelling at you that you have can only call `await` from an async function modify the function to make it async as shown below. 

```js
function ask(options){
  return new Promise(async function(resolve){
```

The reason we did not mark the `ask` function itself as async is because you have to mark the parent function which is the promise callback. 

Now that should work exactly the same way as it did before when you call `ask({title: ' does this work'})` from the console.  

Try opening Firefox and testing it there to see if it works. 

![](../attachments/1081.png) 13:35

GO back to our fieldset and put the rest of the inputs there. 

First we need an input with type of text, which we will name "input" and a button with type of submit. 

```html
popup.insertAdjacentHTML(
  "afterbegin",
  `
  <fieldset>
    <label>${options.title}</label>
    <input type="text" name="input"/>
    <button type="submit">Submit</button>
  </fieldset>
`
);
```

If you refresh the page, you should see an input with the button. 

![](../attachments/1082.png) 14:09

If you try to enter a value into the input and hit submit, you will see that the page refreshed and that we get the value entered in the query string of the url. 

![](../attachments/submit.gif)

We need to use `preventDefault` to stop the form from submitting. 

Before we do that, add the cancel button onto the popup if the option is passed, which we forgot to do earlier. 

```js
 // check if they want a cancel button
if (options.cancel) {
  const skipButton = document.createElement("button");
  skipButton.type = "button";
  skipButton.textContent = "Cancel";
  popup.firstChild.appendChild(skipButton);
  // TODO: listen for a click on that cancel button
}
```

Run `ask({title:"does it work"})` in the console to ensure the popup still shows up.  

Also try running `ask({title:"does it work?", cancel: true})`. 

We are getting an error.
>Uncaught (in promise) DOMException: Failed to execute 'appendChild' on 'Node': This node type does not support this method.

![](../attachments/1083.png)  15:37

Why is that happening? 

Let's debug by logging the value of `popup.firstChild` before we call `appendChild` on it. 

![](../attachments/1084.png) 16:14 

As you can see, it is returning text node.

If you scroll up to our code, you will see that where we created the fieldset using backticks, we had the fieldset start on a new line. 

![](../attachments/1085.png) 15:53 

If you just modify the code so that the fieldset starts on the same line as the backtick, it will work. 

![](../attachments/1087.png) 16:07

What happened is when we had the fieldset start on a new line, the new line was treated as a text node. 

If you recall `firstChild` will grab all the nodes, not just elements. As Wes has mentioned, if you want to just grab elements, you should use `firstElementChild` instead. 

We were trying to append a DOM node to just blank text, which isn't possible, you can only append it to actual elements. 

Leave the fieldset on the separate line and then modify the code to be `popup.firstElementChild.appendChild(skipButton)`. 

That fixes it! 

![](../attachments/1089.png) 17:09

Let's also fix the fieldset so it's not on it's own line because that was sloppy formatting. 

```js
popup.insertAdjacentHTML(
  "afterbegin",
  `<fieldset>
    <label>${options.title}</label>
    <input type="text" name="input"/>
    <button type="submit">Submit</button>
  </fieldset>
`
);
```

Now that we have both the buttons, let's hook up the event listeners, starting with the submit button and preventing default on the form. 

Pass an anonymous function to the event listener. You could make a separate function but keeping it inside of the `ask` function as an anonymous function is fine. 

```js
// listen for the submit event on the inputs
popup.addEventListener("submit", function(e) {
  e.preventDefault();
  console.log("Submitted!");
});
```

![](../attachments/1090.png) 18:07

Next we want to take the value out of the input and resolve it. We have access to the `resolve` function bcause it passed as a parameter. 

![](../attachments/1091.png) 18:24

Because of the scope of our promise callback, the `resolve` function is available to us in the higher function. 

We will call resovle and pass in `e.target.input.value` but before we do that, let's just log the target to see what we have. 

```js
popup.addEventListener("submit", function(e) {
  e.preventDefault();
  console.log(e.target);
});
```

![](../attachments/1092.png) 19:03

As you can see, the target is the form. 

Now let's see what input is. 

```js
popup.addEventListener("submit", function(e) {
  e.preventDefault();
  console.log(e.target.input);
});
```

As you can see, it returns the input with a name of input. 

![](../attachments/1093.png) 19:14

Remember, anytime an input has a name property, it will be available via the property on the form.

To get the value from that input, we just tack on a `.value` and then resolve that data by passing it to our resolve function like so:

```js
popup.addEventListener("submit", function(e) {
  e.preventDefault();
  resolve(e.target.input.value);
});
```

If you refresh the page and try it by calling `ask({title:'does it work', cancel:true})` in the console, entering a value in the input and pressing submit, you should see the promise in the console with the resolved value. 

![](../attachments/1094.png) 19:39

If we wanted to get the actual data from the input, we could just call `ask` with `await` in front of it from the console, as shown below 👇

```js
await ask({title:'does it work', cancel:true})
```

![](../attachments/1095.png) 19:54

Now if you try pressing the submit button again, it doesn't really do anything, but that event listener is still there. You can tell that it is still there by adding a log of "Submitted" to the handler.  

![](../attachments/1096.png) 20:21

One neat thing about `addEventListener` is you could remove the event listener for submitted as soon as it is resolved. 


#### Running an Event Listener Only Once

There is a shortcut we can use where the third argument of `addEventListener` is an `options` object, and we can pass it `{once:true}`. That will tell the browser to only listen for the submit event once, and then remove the event listener. 

That is very handy for things that you only want to happen once.

We want to remove the popup from the DOM entirely. 

To do that, we will create a function `destroyPopup()` because we need to run it on submit and on cancel. 

For now, in the code let's just call the function which we still need to create and we will pass it the popup. 

```js
popup.addEventListener(
  "submit",
  function(e) {
    e.preventDefault();
    console.log("Submitted!");
    resolve(e.target.input.value);
    // remove it from the DOM entirely
    destroyPopup(popup);
  },
  { once: true }
);
```

Let's create that function above our `ask` function declaration. 

Because `popup` is scoped to a different function, in order to access it within `destroyPopup`, we need to pass it as an argument. 

Within the function, let's remove the class of `open` from the popup and then wait one second because we want to wait for the thing to fade out before we remove it from the DOM.

In order to be able to use `await` within `destroyPopup` we will need to mark it as async. 

```js
async function destroyPopup(){
  popup.classList.remove('open');
  await wait(1000);
}
```

Then we want to remove the popup entirely. Add the code below to the `destroyPopup` function.

```js
popup.remove();
```

Before we had the `.remove()` method, we used to grab the element one level up and call `removeChild` on it and pass the popup, as shown below 👇

```js
popup.parentElement.removeChild(popup);
```

Thankfully there is now just a `.remove()` method that we can use.

If you refresh the page and then click the button and submit a value into the input, you will see the popup fades out.

Let's check one thing. 

If we try to log the `popup` even after we have removed it, is it still there?

```js
popup.remove();
console.log(popup);
```

As you can see, we still have access to the popup even though it has been removed from the DOM. 

That is a potential **memory leak**, because every time you pop something up, you add all these things to it, such as event listeners, and simply removing the element from the DOM does **not** remove it from Javascript's memory entirely (because it is possible you might want to add it back). 

If you do want to get rid of it entirely, just destroy any evidence of it using `popup = null;`.

You may notice in the video that Wes' ESLint is yelling at him because he has a rule to not overwrite parameters.  However, to get around that you could do something as shown below 👇

```js
async function destroyPopup(popup){
  let myPopup = popup;
  popup.classList.remove('open');
  await wait(1000);
  //remove the popup entirely
  popup.remove();
  myPopup = null;
}
```

The reason that works is that it is all references. 

If we wanted to disable that rule in eslint we could wrap it in the following comment 👇

```js
/* eslint-disable no-param-reassign */ 
/* eslint-enable no-param-reassign */
```

The next thing that we need to do is handle the cancel button. Let's hookup the buttons because at this point, Wes is tired of running the code from the console. 

Go to the very bottom of the script and grab all the elements with an attribute of `data-question`. 

```js
// select all buttons that have a question
const buttons = document.querySelectorAll('[data-question]`);
console.log(button);
```

![](../attachments/1097.png) 26:27

As you can see we get a node list of buttons. 

Now for each button, we will listen on the click event and pass it a reference to a function `askQuestion`, which we will make soon.. 

```js
buttons.forEach(button => button.addEventListener('click', askQuestion));
```

Inside of `askQuestion`, just log the event. 

```js
function askQuestion(e){
  console.log(e);
}
```

![](../attachments/1098.png) 27:22

As you can see, when we click the button we get the event. 

Now let's grab the button that was clicked, and then save the answer. 

We will need to use `await` so let's mark the function as `async`.  

For the question, we will want to pass the title whatever the button text is. To do that, we can use `button.dataset.question`. 

```js
async function askQuestion(e) {
  const button = e.currentTarget;
  const answer = await ask({ title: button.dataset.question });
  console.log(answer);
}
```

![](../attachments/1099.png) 27:58

As you can see, when you click the popup for name and enter a name, we get the value back. 

![](../attachments/1100.png) 28:10

Now we need to check if someone has passed the `data-cancel` attribute.  To do this, we need to pass `cancel` to the options object we are passing to `ask`. 

How do we tell if the user has passed a `data-cancel` attribute?
Let's try logging the dataset. 

Add the log within `askQuestion` shown below 👇

```js
const button = e.currentTarget;
console.log(button.dataset);
```   

If you refresh the page and click the age button you will see `button.dataset` logged to the console. 

![](../attachments/1101.png) 28:52 

Why is `cancel` an empty string? 
Because we didn't pass it as `data-cancel="true"`. 

The way HTML attributes work is that simply by existing, they're true. By not existing, they are false. 

In addition, trying to convert a string of "true" and "false" is a bit of a nightmare, so instead we will just pass an attribute with nothing in it if it means we should have a cancel button.

To detect if it is there we can add the code below 👇

```js
const shouldCancel = button.dataset.cancel;
const answer = await  ask({title: butotn.dataset.question, cancel: shouldCancel});
```

If you refresh the page and try that, does it work? 

The answer is no, because `shouldCancel` is going to give us an empty string. 

Is an empty string `true` or `false`?  It is falsy! 

So if we are passing an empty string, it is going to be falsy. 

You might think you could just put a bang in front of it as shown below 👇 but we still have the issue with an empty string being falsy.

```js
const shouldCancel = !!button.dataset.cancel;
```

So how do we detect if there is a `cancel` property within the dataset? We can check using the syntax below, because if it's not true, it won't exist .

```js
const shouldCancel = 'cancel' in button.dataset;
```

What is that syntax? 

Let's say we have an object `const wes = { name: 'wes'}`. 

We want to check if Wes has a name property. We are not checking that it is there, but simply that it has a name property. 

```js
'name' in wes;
```

To check for that, we can use the code above 👆 which would return true.   

If we check for a property that doesn't exist like `'asfdas' in wes`, it would return false.

That is how you check if a property is there on an object.

We cannot use the other methods to check because sometimes a property is set to a falsy value such as an empty string or a 0. Using the `in` syntax solves that issue. 

```js
const button = e.currentTarget;
const shouldCancel = 'cancel' in button.dataset;

const answer = await ask({
  title: button.dataset.question,
  cancel: shouldCancel
});
```

Let's refactor that and rename `shouldCancel` to just `cancel` so we can use the shorthand syntax.

```js
const answer = await ask({
  title: button.dataset.question,
  cancel
});
```

_NOTE: In the video, Wes pauses it to specify that he could have used `button.hasAttribute('data-cancel');` to check for this but he decided to leave this in the video because it is a good lesson on how to check if a property on an object exists, regardless of which value it is set to._

![](../attachments/1102.png) 31:33

If you refresh the page, that should now work.

Let's hook up the cancel button. 

Go back to where we created it and under the TODO comment we will create a callback function which resolves the promise with `null`, and then we will call `destroyPopup` because we want to completely remove the popup. 

```js
skipButton.addEventListener(
  'click', 
  function(){
  resolve(null);
  destroyPopup(popup);
  }, 
  {once:true}
);
```

If you refresh the page, you will see that it is still working.

That is the basics of the pop-up. 

The last thing we will cover is how to use the popup to ask questions in series. 

For example, let's say someone is going through a form and you want to popup something and ask three pieces of data before they can continue. 

Let's say we had an array of questions like you see in the image below. 

![](../attachments/1103.png) 33:22

How would we ask them in series? 

You might assume we could use `Promise.all()`. 

For each one, we want to pass the `ask` a different question from the questions array as shown below 👇

```js
const answers = Promise.all([
  ask(questions[0]);
  ask(questions[1]);
  ask(questions[2]);
]).then(answers=>{
  console.log(answers); 
});
```

This is not an uncommon thing to do, waiting for few promises to resolve and then getting the answers. 

We have to use the promise syntax because we are not in an async function where we are calling `Promise.all()`. 

If you refresh the page and try that, you will see that the questions are asked out of order. What s happening is there are actually three popups on the page at the same time. 

![](../attachments/1104.png) 35:04

That is not a good solution, we do not want to pop them all up at once. 

`Promise.all` will fire them all off concurrently at the same time, which is often what you want but when you want to do it sequentially like we do, you cannot use `Promise.all`.

A better way to do this would be to take your questions and map over each and pass in the `ask` function.

```js
const qPromises = questions.amp(ask);
console.log(qPromises);
```

If you refresh the page and look at that in the console, you will see we have an array of three promises which have not been answered yet. 

![](../attachments/1105.png) 36:16

What we can do is loop over the array and for each one return a promises to get an array of promises. 

Then you can wrap that in a `Promise.all()` as shown below. 

```js
Promise.all(questions.map(ask)).then(data=> {
  console.log(data);
});
```

That will loop over each of the questions, pipe it into the `ask` function (which will return a promise), that will return to us an array. We wrap it in a `Promise.all()` and then listen with a then. This will actually work. 

We still have the problem of the UI popping up all the time so that is not what we want.

What we do want is to map over it, but asynchronously. 

```js
questions.forEach(async function(){
  console.log('Asking a question');
  console.log(question);
  const answer = await ask(question);
  console.log(answer);
})
```

![](../attachments/1106.png) 38:07

That did not wait for anything right? They will resolve, but they all three ran at the same time. 

So how do we make an async map function? 

We use a `for of` loop.

- Make an async function called `askMany`.  

- Within that function, we will have the `for of` loop which loops through all the questions. 

- Inside of the loop we will have `const answer = await ask(question);`. 

- We will log the answer after it. 

```js
async function askMany(){
  for(const question of questions){
    const answer = await ask(question);
    console.log(answer);
  }
}

askMany();
```

Now when you refresh the page, you will see the questions come up one after the other and are submitted sequentially as well.

![](../attachments/1107.png) 39:32

The reason for that is unlike `map` and `foreach`, `for of` allows you to pause a loop by awaiting something inside of it, which is great.

One thing Wes likes to do is make a utility function called `asyncMap` which does exactly what our function does but returns to us an array, like a map does. 

We will be using generic variable names here to make the function as flexible as possible. 

```js
async function asyncMap(array, callback){
  // make an array to store our results
  const results = [];
  // loop over our array
  for(const data of array){
    const result = await callback(item);
    results.push(result);
  }
  //when we are done the loop, return it
  return results;
}
```

Now we should be able to replace the `askMany` code, and make a new function called `go` which we will mark as async to allow us to run an await. 

```js
async function go(){
  const answers = await asyncMap(questions, ask);
  console.log(answers);
}

go();
```

Now when you refresh the page and look at the results, you should see that we get our array back. 

![](../attachments/1108.png) 42:40

We could take things one step further and refactor the function slightly to push the await of the callback directly.

```js
async function asyncMap(array, callback){
  // make an array to store our results
  const results = [];
  // loop over our array
  for(const data of array){
    results.push(await callback(item));
  }
  //when we are done the loop, return it
  return results;
}
```

---

## 73 - Async Typer UI - two ways

![](../attachments/typer.gif) 00:55

In this video we will using **async/await** and **recursion** to create the effect of someone typing at different speeds.

We will do this by taking any element with a `data-type` attribute on it, and figuring out how we can make it look like it is being typed. 

We will also support the ability to pass in a `data-type-min` and a `data-type-max` attribute to specify the amount of time between each letter being typed to make it look a little more human (so instead of always typing a new letter every 10 milliseconds, there is a range).

This is a great example of asynchronous code because if it was synchronous, it would need to wait for one element's text to finish being typed before starting the next one. 

Using `async`, each element can wait for a certain amount of time without interfering with each other.

We will be working out of `73 - async typer` exercise folder. 

Open up the `scripts.js` file and let's start by adding our `wait` function which we have used in the last few videos. 

```js
funciton wait(ms = 0){
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

Next we need a function that will return us a random number between a max and min value. 

We already know that you can calculate a random number using a combination of `Math.floor` and `Math.random` like `Math.floor(Math.random() * 3)`. 

![](../attachments/1109.png) 2:06 

But what if you want a number between 10 and 15, how would we do that? 

It is basically the same thing, we just shift it up by the amount of the min.

Call `Math.random()` and multiply that by `(max - min)` and then add the min to that value. 

Add defaults of 20 milliseconds for the min and 150 for the max. 

```js
function getRandomBetween(min = 20, max = 150){
  return Math.random() * (max - min) + min;

}
```

If you refresh the page and try running the code, you will see that it gives us a random number between 0 and 100.

You can also wrap that in a `Math.floor()` and that will give you a whole number. 

One thing that people do not like about functions that get random numbers is that it is not a **pure function**. Pure functions are functions where every single time that you run the function with certain parameters, you will always get the same result.

A pure function is the idea that a function that takes in arguments will always, always return the exact same value. That makes testing your functions easy.

So how do you write a pure function when the thing you are trying to do is implicitly random?

You can do that by passing in a random number so you can then test it. We will replace where we use `Math.random` in the function to instead use the `randomNumber` parameter we pass in.

```js
function getRandomBetween(min = 20, max = 150, randomNumber){
  return Math.floor(randomNumber * (max - min) + min);
}
```

![](../attachments/1110.png) 4:47

This way, when you pass the arguments to the function, we will always get the same value returned.  

To use this in a production application, you could do `getRandomBetween(0, 100, Math.random())` and pass the random number using `Math.random()`.

One cheat you can do is set the default for `randomNumber` to be `Math.random()` as shown below.

```js
function getRandomBetween(min = 20, max = 150, randomNumber = Math.random()){
  return Math.floor(randomNumber * (max - min) + min);
}
```

Next we want to make a function called `draw` which will take in an element. Let's just log the element within that function for now. 

```js
function draw(el){
  const text = el.textContent;
}
```

Below that, grab the elements with a `data-type` attribute on it. For each one, we will all the `draw` method. 

```js
els.forEach(el=> draw(el));
```

We can refactor that code to be even shorter like so, `els.forEach(draw)`.

That works because it will call the function for us, for each one. We can take that even one step further as shown below. 

```js
document.querySelectorAll('[data-type']).forEach(draw);
```

Next we want to start looping over it. We will do it twice.

The first time we will use an async for of loop and then we are going to do it again with recursion.

The way this `draw` function will work is we are going to erase all the text that is in the element and write it back in letter by letter.

First we will write `T`, then `Th`, then `Thi`, then `This` and so on for all the text within the element.

Make a variable called `soFar` which we will set to an empty string. Then we will loop over every letter of the text. 

Previously for looping over letters we used a spread or we split it. But a `for of` loop has the ability to loop over text one letter at a time.  

We will call the variable that represents each letter in our text variable `letter`. 

```js
for(const letter of text){

}
```

Now within the loop, we will log the letter and then on the next line we will tack the letter onto the `soFar` variable and then log that variable. 

```js
function draw(el){
  const text = el.textContent;
  let soFar = '';
  for(const letter of text){
    console.log(letter);
    soFar += letter;
    console.log(soFar);
  }
}
```

If you take the `data-type` attribute off of the paragraph tag in the HTML and then open the console, it is easier to visualize this and how the text is slowly building up.

![](@attachments/textflow.gif) 9:15

If we tried to set the text content of the element to `el.textContent = soFar`, when you refresh the page it happens so fast that you can barely see it. 

To fix that, let's wait for some amount of time. Make the `draw` function async and then add `await wait(10);`. 

```js
async function draw(el){
  const text = el.textContent;
  let soFar = '';
  for(const letter of text){
    console.log(letter);
    soFar += letter;
    console.log(soFar);
    await wait(10);
  }
}
```

That loops pretty cool but to make it seem more human, we will wait a random amount of time instead of 10 ms every time. 

Let's do that using our random number function. 

```js
const amountOfTimeToWait = getRandomBetween();
await wait(10);
```

We can now pull in the min and max values from the data attributes using `el.dataset` and destructuring. Pass the min and max values to our `random` function. 

```js
const { typeMin, typeMax } = el.dataset;
const amountOfTimeToWait = getRandomBetween(typeMin, typeMax);
await wait(amountOfTimeToWait);
```

We can get rid of all the console logs we have added and put the `data-type` back on our paragraph tag. 

That is how you do it with a `for of` loop. 

Next we will look at how we can do this with **recursion**. 

Recursion refers to this concept of a function calling itself until there is some sort of exit condition that tells it to stop.

Let's make a function we will also call draw `draw`. 

The way this function will work is we will keep an index variable inside of the function and increment it once each time.

```js
function draw(el){
  const index = 1;
  const text = el.textContent;
  const { typeMin, typeMax } = el.dataset; 
}
```

Add another async function, `drawLetter`, within `draw()` to take advantage of closures because we can run a function multiple times while still accessing the variables within the `draw` function. 

So the way this will work is we will start at the index and take 1 letter, then we will take 2 letters, and then 3 letters and so on using slice, and then we will update the element every single time. 

```js
async function drawLetter(){
  el.textContent = text.slice(0,index);
}
```

For a quick refresher of how slice works: you pass it a starting and ending index and it will return the charactres inbetween like so. 

![](../attachments/1111.png) 14:11

```js
function draw(el){
  const index = 1;
  const text = el.textContent;
  const { typeMin, typeMax } = el.dataset; 
  async function drawLetter(){
    el.textContent = text.slice(0,index);
  }
}
```

Now when you run this, nothing actually happens. It doesn't actually do anything but that is because we haven't called `drawLetter`. 

Let's go ahead and do that. 

```js
function draw(el){
  const index = 1;
  const text = el.textContent;
  const { typeMin, typeMax } = el.dataset; 
  async function drawLetter(){
    el.textContent = text.slice(0,index);
  }
  //when this function draw() runs, kick off drawLetter
  drawLetter();
}
```

If you refresh the page you will just see the first letter which is okay because we still need to increment the index using `index = index + 1;` or `index += 1;`. And then we need to call `drawLetter()` again.

How do we do that? 

Just call `drawLetter()` within our async function as shown below. 

```js
function draw(el){
  const index = 1;
  const text = el.textContent;
  const { typeMin, typeMax } = el.dataset; 
  async function drawLetter(){
    el.textContent = text.slice(0,index);
    index += 1;
    drawLetter();
  }
  //when this function draw() runs, kick off drawLetter
  drawLetter();
}

document.querySelectorAll('[data-type]').forEach(draw);
```

This is the recursive part, meaning that part of the logic of `drawLetter` is to call itself. The way the code is now will create an infinite loop and will probably break the browser. 

When Wes ran the code he got the following error..

![](../attachments/1112.png) 15:43

Remember when we discussed the call stack previously? 

What is happening is `drawLetter` is calling itself over and over again and eventually the browser complains that you have added too many things to the call stack. 

What we need to do is add an exit condition: we need to check if the index is less than or equal to the length of our `text` variable, the run it again. 

```js
  async function drawLetter(){
    el.textContent = text.slice(0,index);
    index += 1;
    //exit condition
    if(index <= text.length){
        drawLetter();
    }
  }
  //when this function draw() runs, kick off drawLetter
  drawLetter();
```

Now when there are no more letters to draw, it will stop and the function will end.

If you refresh the page, it still works but it happens so quickly we don't see anything. Let's wait 10 milliseconds using the wait function which we will add above the if statement. 

Now if you refresh the page you will see it's adding the text at a rate of 10 milliseconds. 

We can do the same thing we did in the previous method and grab our min and max and pass it to `getRandomBetween`. 

The reason why we do the calculation for the random amount of time inside of `drawLetter` is that we want every letter to be random. If we added that code at the top, the random value would only be calculated once. 

```js
function draw(el){
  const index = 1;
  const text = el.textContent;
  const { typeMin, typeMax } = el.dataset; 
  async function drawLetter(){
    el.textContent = text.slice(0,index);
    index += 1;
    const amountOfTimeToWait = getRandomBetween(typeMin, typeMax);
    //exit condition
    await wait(10);
    if(index <= text.length){
        drawLetter();
    }
  }
  //when this function draw() runs, kick off drawLetter
  drawLetter();
}
```

If you refresh the page, you will see that it still works. You could probably also do it with a While loop, but Wes would personally choose the `for of` loop but that is just a personal preference. 
