---
attachments: [731.png, 732.png, 733.png, 734.png, 735.png, 736.png, 737.png, 738.png, 739.png, 740.png, 741.png, 742.png, 743.png, 744.png, 745.png, 746.png, 747.png, 748.png, 749.png, 750.png, 751.png, 752.png, 753.png, 754.png, 755.png, 756.png, 757.png, 758.png, 759.png, 760.png, 761.png, 762.png, 763.png, 764.png, 765.png, 766.png, 767.png, 768.png, 769.png, 770.png, 771.png, 772.png, 773.png, 774.png, 775.png, 776.png, 777.png, 778.png, 779.png, 780.png, 781.png, 782.png, 783.png, 784.png, 785.png, 786.png, 787.png, 788.png, 789.png, 790.png, 791.png, 792.png, 793.png, 794.png, 795.png, 796.png, 797.png, 798.png, 799.png, 800.png, 801.png, 802.png, 803.png, 804.png, 805.png, 806.png, 807.png, 808.png, 809.png, 810.png, 811.png, 812.png, 813.png, 814.png, 815.png, 816.png, 817.png, 818.png, 819.png, 820.png, 821.png, 822.png, 823.png, 824.png, 825.png, 826.png, 827.png, 828.png, 829.png, 830.png, 831.png, 832.png, 833.png, 834.png, 835.png, 836.png, 837.png, 838.png, 839.png, 840.png, 841.png, 842.png, 843.png, 844.png, 845.png, 846.png, 847.png, 848.png, 849.png, 850.png, 851.png, 852.png, 853.png, 854.png, 855.png, 856.png, 857.png, 858.png, 859.png, 860.png, 861.png, 862.png, 863.png, 864.png, 865.png, 866.png, 867.png, 868.png, 869.png, 870.png, 871.png, 872.png, 873.png, 874.png, 875.png, 876.png, 877.png, 878.png, 879.png, 880.png, 881.png, 882.png, 883.png, 884.png, 885.png, 886.png, 887.png, 888.png, 889.png, 890.png, 891.png, 892.png, 893.png, 894.png, 895.png, 896.png, 897.png, 898.png, 899.png, 900.png, 901.png, 902.png]
title: 'Module 10: Harder Practice Exercises'
created: '2020-04-20T11:16:46.618Z'
modified: '2020-09-15T22:41:20.892Z'
---

- [Module 10: Harder Practice Exercises](#module-10--harder-practice-exercises)
  * [55 - Face Detection and Censorship](#55---face-detection-and-censorship)
  * [56 - Sarcastic Text Generator](#56---sarcastic-text-generator)
    + [The modulo operator](#the-modulo-operator)
  * [57 - Shopping Form with Custom Events, Delegation and localstorage](#57---shopping-form-with-custom-events--delegation-and-localstorage)
    + [`localStorage`](#-localstorage-)
    + [Event Delegation](#event-delegation)
  * [58 - Building a Gallery Exercise](#58---building-a-gallery-exercise)
    + [Closures](#closures)
      - [`tab-index`](#-tab-index-)
  * [59 - Building a Slider](#59---building-a-slider)

---

# Module 10: Harder Practice Exercises

## 55 - Face Detection and Censorship 

This exercise is going to be a bit more fun then our previous lessons. 

We are going to build a face detection that will detect and blur your face from a video element into a canvas element. 

This exercise is stepping a little bit ahead because there are a couple of things we need to learn a more about like promises and async/await, and bundling tools, specifically one called Parcel. 

![](../attachments/731.png) 00:22

The first thing we need to check is that we are on a browser that supports face detection. 

At the time of this recording, there is a proposal for an API, meaning it's not finished yet and might change.

Ideally it will get into all of the browsers but currently it is only in Chrome and Android. 

The way you can tell if your browser supports it is you can go to the console on any page and type `FaceDetector`, or `typeof FaceDetector`. 

![](../attachments/732.png) 1:40

If you get `undefined` or an error returned, that means your browser does not support it. If you are on Chrome, you likely have to go to the flags page in Chrome and turn it on. 

Often new features in the browser are not given to the masses because they are not ready yet. In order for us to play with those features, we need to enable them. 

The way you turn flags on in Chrome is you navigate to `chrome://flags`.

![](../attachments/733.png) 3:30

This page contains all kinds of features that are still experimental in Chrome. You want to search for "Experimental Web Platform features" and enable it. 

You will probably have to restart your browser, so go ahead quit it, and restart it, and then you should see `typeof FaceDetector` work. 

If you do all that and still cannot get `typeof FaceDetector` to return "function" it's possible that your computer does not support it. 

But from everyone Wes has tested with, it works well.

The second thing is we need to use a server in order to run this. That is because accessing a user's webcam is a security issue _(you don't want to give everybody access to your webcam)_, so in order to do it you must first you have to ask the user first for access to their webcam.  

You've probably been to a million websites where they ask for permission to send notifications or they request to know your location. Those are permission-based APIs in the browser, and accessing someone's webcam is no different than that. 

That sort of preference and permission, it allowed or not, is tied to the origin.

An **origin** in Javascript is just a fancy way of saying a **domain name**. 

So in Wes' case, he is currently allowing the camera on localhost, but you might allow the camera on New York Times or Facebook or all these different websites. 

![](../attachments/734.png) 3:54

Everytime you visit a new origin, a new domain name, you're going to have to ask the user for access to their webcam and it will pop up. 

So in order for us to do that, we cannot just open up `face.html` (from the  `/53 - Face Detection Censorship` folder) in the browser like we have been doing up until now.

![](../attachments/735.png) 4:27

The reason for that is the file path that you see in the url browser above is not an origin. If security stuff is tied to an origin, it won't be able to do it from a local file.

You might notice the X next to the camera. If you take a look, you will see that the camera is blocked.

![](../attachments/736.png) 4:35

If you try to allow it by clicking "always allow", it still won't work. 

So you cannot open the HTML file directly in your browser, it must run through a server. So how do we run a server? 

One server that Wes likes is a **bundler**, called Parcel, which we will learn more about when we get to the modules section. 

**Parcel** will give us a little development server where when we change something on the page, it will automatically refresh the page for us. If we change any of our CSS, it will automatically re-load the CSS on the page without actually having to do a full page refresh. 

To get that running, we need to open up a terminal. If you need a refresher, go back to video 2 where Wes goes over the different types of terminals. 

Once you have the terminal open, go into the folder that contains the `face.html` file. 

To do that, you need to use the command `cd` to go into the correct directory.

If you don't know where you are starting in the terminal, you can type `pwd` and it will tell you where you are on your computer. 

![](../attachments/737.png) 6:11

What is probably easier than that is if you are using VSCode, you can just right click the folder and select "Open in Terminal". 

![](../attachments/738.png) 6:20

That opens the terminal up in the built in terminal in VSCode.

![](../attachments/739.png) 6:23

In the second video, Wes had us install **NodeJS** and **NPM**. You can check if you have both installed by typing `node -v` and `npm -v` in the terminal. That will return to you the version you have installed, as shown below 👇

![](../attachments/740.png) 7:01

If you need to check what the latest NodeJS version is, you can go to `nodejs.org` and find the LTS version which stands for long term support -- that is the most stable version. 

![](../attachments/741.png) 7:04

Once you have confirmed you have both of those and you are in the right directory, go ahead and type `npm install`.

Wes will cover this all more in the  future, but what that does is it will take all our dependencies and install them for us. 

In our case we are installing Parcel. 

![](../attachments/742.png) 7:45

You should completely ignore the versions in this file, because that will likely change in the future and Wes will be keeping the files up to date. 

While we wait for that to finish installing, let's take a look at the `face.html` structure to see what we are working with. 


```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>Censorship</title>
  <link rel="stylesheet" href="../../base.css">
</head>

<body>
  <div class="wrap">
    <video class="webcam"></video>
    <canvas class="video"></canvas>
    <canvas class="face"></canvas>
  </div>
  <script src="./pixelated-face.js"></script>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
    }

    .wrap {
      position: relative;
      min-height: 100vh;
      display: grid;
      justify-content: center;
      align-items: center;
    }

    .wrap>* {
      grid-column: 1;
      grid-row: 1;
    }
    
    .face {
      position: absolute;
    }
  </style>
</body>
</html>
```

We have our base CSS which is just the blue background. 

Then we have our wrapper, which has a video element, a canvas element, and another canvas element. 

One canvas is for the video and one is for our face.

Then we are linking up the `pixelated-face.js`. 

_(Note: Wes is using a different file than you in the video so he can demonstrate how the finished result works)_. 

After that we have a few styles that just center things on the page, nothing too interesting. 

If you look at the terminal, the package should be done installing. 

![](../attachments/743.png) 8:56

You may notice in the terminal something like "found 39 high severity vulnerabilities". That will pop up when you `npm install` things. What happens there is that some dependencies have security vulnerabilities that need to be fixed and what happens is the people who create Parcel will fix that eventually. So if you see that, don't freak out. It's totally fine, hopefully NPM will hopefully find a better way to deal with those warnings. 

Create a new file `pixelated-face.js` and inside of it log "it works!".

Go back to the terminal and in the same directory type `npm start`. 

That will run Parcel against the `face.html` file and it will run the server at some URL. 

![](../attachments/744.png) 10:45

If you go to that URL in the browser and open the console, you should see "it works!". 

![](../attachments/745.png) 11:03

Sometimes you will see weird warnings like the yellow one above, and that is related to a Chrome extension that you have installed, and that is annoying because it gets in the way of writing our actual code. 

That can be annoying because there is no way to get rid of them. 

One trick Wes has found it typing into the Filter `-DevTools` as shown below 👇

![](../attachments/746.png) 11:20

Now that we have everything up and running, let's dig into some code.

The first thing we want to do is select all the elements that are on our page. We have our video, our canvas, and then another canvas.

We are going to access the user's webcam, dump it into the canvas element with the class of video. 

Then we are going to take the frames of that video, put a square around the person's face. 

In the canvas element with class of face, we will pixelate the person's face. 

The canvas element work could be done on one canvas, but Wes prefers to keep them separate in case he ever wants to only pull one of those images out.

Go ahead and grab those three classes, `webcam`, `video`, and `face`. 

Let's page them into our `pixelate-face.js` file. 

_Note: in the video, at this section, Wes is able to paste all three classes like this on the page 👇_

```js
webcam
video
face
```

_In VSCode, he is able to press the shortcuts `CMD + A` and then `CMD + Shift + L`, and that gives him a cursor on every single line._ 

![](../attachments/747.png) 12:35

Add the following code 👇

```js
const video = document.querySelector(".webcam");
const canvas = document.querySelector(".video");
const faceCanvas = document.querySelector(".face");
```

We need to pull the context out of each canvas element now. 

We talked about that in our Etch-a-Sketch exercise but that is where we do the drawing. 

Modify the code as shown below 👇

```js
const video = document.querySelector(".webcam");

const canvas = document.querySelector(".video");
const ctx = canvas.getContext("2d");

const faceCanvas = document.querySelector(".face");
const faceCtx = canvas.getContext("2d");
```

Now make a new face detector, and then let's log everything we have so far. 

```js
const faceDetector = new FaceDetector();
console.log(video, canvas, faceCanvas, faceDetector);
```

![](../attachments/748.png) 14:12

_Note: you might notice in VSCode that it says "FaceDetector is not defined" if you hover over `new FaceDetector()`._

![](../attachments/749.png) 14:18

_That is because it is looking for a function called `FaceDetector`. The way we can solve that is to say `const faceDetector = new window.FaceDetector()`. That is fine to do (Wes told us not to do it in looping) here because this FaceDetector API does not exist in NodeJS land._

The next thing we need to do is write a function that populates the user's video. 

To do that, grab the stream from the user's webcam. 

```js
function populateVideo(){
  const stream = navigator.mediaDevices.getUserMedia();
}
```

You need to pass `getUserMedia()` some options, specifying if you want video or audio (we just want video). You can just pass `video:true` or you can ask for a specific size from it. 

Modify the code as shown below and get rid of the log we added earlier.

```js
function populateVideo() {
  const stream = navigator.mediaDevices.getUserMedia({
    video: { width: 1280, height: 720 },
  });
  console.log(stream);
}
```

If you refresh the HTML page and try to run `populateVideo()`, you will see an error as shown below. 

![](../attachments/750.png) 15:50

Now that we are running things through a bundler, we no longer have the ability to access our functions globally via the console. 

If you ever do want to do that, you can do `window.populateVideo = populateVideo;`. 

That will surface it for you, but that is not a great way to do it. 

The best way to do it would just be to add a log in your javascript file and you can see it. 

If you do ever need to access it from the chrome dev tools, you can right click it, and click store as global variable.

![](../attachments/751.png) 16:48

That will store it in a global variable called `temp1`. 

If you try calling `temp1()`, you will see something returned to us called a **promise**.  

![](../attachments/752.png) 16:57

There are a couple things going on here. First, it might show you a little recording icon on the chrome tab (it might not, we will go over that in a sec.). 

![](../attachments/753.png) 17:03

As mentioned, we are returned a promise when we call `temp1()` in the console (which is our `populateVideo()` function stored as a global variabe). 

What that means is we have not been returned the actual stream of video, instead it's just something called a promise that it will get the stream of the webcam eventually. 

We will get more into promises in future videos, but for now just know that `navigator.mediaDevices.getUserMedia()` is a special kind of function that returns this thing called a promise.

In order to wait for the stream to come back from the webcam, because that takes some time, we need to first mark the function as `async` by typing the word `async` in front of it, and add the keyword `await` before we call `navigator.mediaDevices.getUserMedia()`. 

Add a call to `populateVideo()` where we used to log it. 

```js
async function populateVideo() {
  const stream = await navigator.mediaDevices.getUserMedia({
    video: { width: 1280, height: 720 },
  });
  console.log(stream);
}
populateVideo();
```

If you refresh the page and look at the console, you may see the following 👇

![](../attachments/754.png) 18:09

If you do not, you may see a little red X on your video camera icon in the browser tab. 

To fix that, you need to click on it and select "continue" or "always allow access". 

Click done, then reload the page, and then you should see a media stream in the console.

![](../attachments/755.png) 18:18

How is what is returned to us via the `MediaStream` useful?

We can now put the stream into our video which we have already selected. 

You would normally pass the video something like `video.srcObject = "dog.mp4";` but instead you will be passing the video the stream then calling `play()` on it.

Put an `await` in front of where you call `video.play()` because sometimes it takes a few seconds to start playing and that will wait for it.

```js
video.srcObject = stream;
await video.play();
```

If you refresh the page, you should see it worked. 

So what did we do there? 

We made a function called `populateVideo()`, where we grabbed the feed off the user's webcam, and then we set the object to be the stream, and then played it. 

Another thing we need to do is size the canvases to be the same size as the video.

If you were to log `video.videoWidth, video.videoHeight` you should get 1280 x 720. 

If you change one line of code from `navigator.mediaDevices.getUserMedia({video: { width: 1280, height: 720 }});` to `navigator.mediaDevices.getUserMedia({video: true});`, and refreshed the page, you should see the sixes 640 x 480. After you test that, switch it back.

_Note: these sizes might not be the same on your computer, depending on your webcam._

So you need to size the canvases to match the video, which you can do like so:

```js
canvas.width = video.videoWidth;
canvas.height = video.videoHeight;

faceCanvas.width = video.videoWidth;
faceCanvas.height = video.videoHeight;
```

Now we have two canvases that are the same size as the video feed.

The next thing we need to do is work with the FaceDetection API. 

We will call it `detect` and it also needs the `async` keyword in front of it (we will cover why in future video). 

We want to detect faces that are in the shot.

Then we will use the `faceDetector` variable we created earlier and call `.detect()` on it. 

You pass `detect()` reference to three things:
- an image
- a video
- or a canvas

In our case, pass it access to the video. 

```js
async function detect(){
  const faces = await faceDetector.detect(video);
  console.log(faces);
}
```

We need to run the `detect()` function once, but after the video has been populated. If you run `detect()` when there is no video, it will not find any faces.

The way you can do that is by tagging a `.then()` onto `populateVideo` like so 👇

```js
populateVideo().then(detect);
```

This is promise-based, which we will cover in more detail in future videos. 

If you refresh the page and open the console now, you should see a face detected. It will tell you exactly where the eyes, the nose, and the mouth are. 

![](../attachments/756.png) 23:24

It also gives us the `boundingBox` which is the square around the user's head.

The way we are calling `detect()` right now, it will only run once after `populateVideo()` is done playing. So we need to call `detect()` over and over again. 

You might be thinking we can use an interval for this. That is the way we used to do this stuff, but there is a better way, that allows you to do things as fast as possible, which is to use something called **request animation frame**.

**Request animation frame** allows the browser to tell us when we should repaint or redo something. 

Instead of us trying to do something every 60 milliseconds, because computers vary in speed, request animation frame will repaint or rerun the stuff on the screen a lot less frequently on a computer that isn't as fast. 

Ask the browser when the next animation frame is, and then tell it to run `detect`, like so 👇 

```js
async function detect() {
  const faces = await faceDetector.detect(video);
  console.log(faces);
  // ask the browser when the next animation frame is and tell it to run detect for us
  requestAnimationFrame(detect);
}

populateVideo().then(detect);
```

If you refresh the page, you should see lots of `DetectedFaces` logged in the console. 

What we did there is instead of calling `requestAnimationFrame(detect)`, we could have just called `detect()` and that works pretty well, but because of performance reasons, it's better to call `requestAnimationFrame()`.

What we have just done there is a concept called **recursion**. 

**Recursion** is when a function calls itself. It will run forever, and ever, until something stops it, such as an exit condition. Recursion is when a function calls itself, inside of itself. 

`detect` is being called from `detect` which allows us to run it infinitely.

Let's take a look at the `DetectedFace`. 

![](../attachments/757.png) 26:24

As you can see, it gives us an array with one item. Log `faces.length`. 

![](../attachments/758.png) 26:44

As you can see, it only logs one face until Wes holds up the queens face on a dollar bill to the webcam. 

![](../attachments/759.png) 27:35

When Wes holds up a picture, Face Detection detects all four faces.

Next up, we need to do 2 things:
- draw triangles around the faces that are found
- censor the face by pixelating the area that is around their face

Make a function `drawFace` which will take in the user's face. The function will need to know how wide and high is the user's face, because the further away the subjects are from the camera will affect that. 

We also need the X and Y coordinate from the top. For example over 400 pixels and down 300 pixels is where the head starts.

Start by just logging the faces and calling `drawFace()`.  Loop over all the faces in a `.forEach` and call `drawFace` for each. 

```js
async function detect() {
  const faces = await faceDetector.detect(video);
  console.log(faces);
  // ask the browser when the next animation frame is and tell it to run detect for us
  faces.forEach(drawFace);
  requestAnimationFrame(detect);
}

function drawFace(face) {
  console.log(face);
}

populateVideo().then(detect);
```

When you refresh the page and look at the console, you should see many faces logged. 

Let's get the bounding box from one of those. We need the `top` and `left`, `width`, and the `height`. 

![](../attachments/760.png) 29:17

```js
function drawFace(face) {
  const { width, height, top, left } = face.boundingBox;
  console.log(width, height, top, left);
}
```

If you refresh the page, you should see lots of logs like the following 👇

![](../attachments/761.png)

One trick you can do is if within the log, you just wrap the items in curly brackets as shown below, it will log the property names and values.

```js
console.log({width, height, top, left});
```

The reason that works is because you are essentially making an object.

![](../attachments/762.png) 30:34

Now we want to draw a box onto our canvas element that is down in the part of the page that is highlighted in the image below.

![](../attachments/763.png) 30:47

We are going to overlay it with the video in order to do that. 

Let's set a couple of defaults at the top of the page. 

```js
const ctx = canvas.getContext("2d");
ctx.strokeStyle = "#ffc600";
ctx.lineWidth = 2;
```

Within `drawFace` function and call `ctx.strokeRect()`, which is the API for drawing a rectangle. 

```hs
function drawFace(face) {
  const { width, height, top, left } = face.boundingBox;
  ctx.strokeRect(left, top, width, height);
}
```

![](../attachments/764.png) 31:45

As you can see, it does work. if you move your face around, the boxes should move around as well. 

We need to fix a few things though. One of those things is that our rectangles are not overlaid on top. 

_Note: if the rectangles are overlaid for you, you can ignore these instructions._

Let's take a look at `face.html`. It seems like it's ignoring the style tag. Try moving the styles to the head, as shown below.

```html
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
    }

    .wrap {
      position: relative;
      min-height: 100vh;
      display: grid;
      justify-content: center;
      align-items: center;
    }

    .wrap > * {
      grid-column: 1;
      grid-row: 1;
    }

    .face {
      position: absolute;
    }
  </style>
</head>

<body>
```

If you refresh the page now, it should work. This likely happened because we are using a beta version of Parcel.

![](../attachments/765.png) 32:29 

The next thing to fix is that the stroke that the rectangle is created in is not yellow. Try moving where you set `strokeStyle` and `lineWidth` into the function right before you draw the rectangle like so 👇

```js
function drawFace(face) {
  const { width, height, top, left } = face.boundingBox;
  ctx.strokeStyle = "#ffc600";
  ctx.lineWidth = 2;
  ctx.strokeRect(left, top, width, height);
}
```

The next thing to fix is that they are not clearing. Fix that by calling `ctx.clearRect` before we draw the rect. 

```js
ctx.clearRect(0,0, canvas.width, canvas.height)
```

That clears the amount, the width and the height, based on starting at the top left hand corner, every time it runs, it clears the canvas for us.

It is working pretty well. It is a bit jumpy right now, it used to be a lot better, they're still working on it. The eyes, nose, and mouth values were working very well for Wes for a while, but currently they're really weird.

The next thing we want to do is pixelate the user's face on top of it. Lets go ahead and do that. 

Create a function called `censor` which will take in a `face`. In our case, we don't care about anything but the bounding box, so instead of doing something like below 👇

```js
function censor(face){
  const faceDetails = face.boundingBox;
}
```

Destructure the bounding box properties directly like so 👇

```js
function censor({boundingBox}){
}
```

Now we just have a variable called `boundingBox`, which we could have rename to a variable called `face` like so 👇

```js
function censor({boundingBox: face}){
 console.log(face);
}
```

![](../attachments/766.png) 35:28

As you can see, we have bounding box. 

Now the question is how do you censor something? 

There are a couple of different ways you can do it. 

The best way Wes has found is to take a snapshot of the user's face, scale it down very very small, and then paint it to the canvas. And then immediately after that, pull it off the canvas, stretch it back up and put it back in. 

So essentially you make it really small and then save it and lose all the pixel quality, and then you take it out, stretch it back up again, and that's how you get the pixelation look. 

Let's first write out comments for what we plan to do. 

```js
function censor({boundingBox:face}){
  //draw the small face
  // take that face back out and draw it back normal size
}
```

Now the way we are going to do this is we are going to take our second canvas context, `faceCtx` and call `drawImage()` on it. 

`drawImage` takes in a lot of arguments, let's look it up on MDN.

![](../attachments/767.png) 37:01

(t takes a few set of options. You can either pass in 3 (`image`, `dx`, `dy`), 5(`image`, `dx`, `dy`, `dWidth`, `dHeight`), or it takes 9 (`image`, `sx`, `sy`, `sWidth`, `sHeight`, `dx`, `dy`, `dWidth`, `dHeight`). 

We will be using all 9, and Wes will do his best to explain what each parameter is.

Let's get started.  

The first argument `drawImage` takes is the image you want to draw to it, so we will pass in our `video`, `faceCtx.drawImage(video);`

Then it wants the `x` and the `y` coordinates of where it should start drawing the image so we will pass `0,0`, like so `faceCtx.drawImage(video, 0, 0);`.  Save the file. 

If you just look at the HTML page, it might look like nothing has changed but if you inspect it, you will see that what we are actually seeing is the canvas, not the video. 

If we add a `display:none` CSS style to the video, you will notice that you can still see yourself. The video is being painted onto the canvas.

![](../attachments/768.png) 37:48

Now this isn't exactly what we want to do. We want to take the square that is painting on Wes' face and throw it on there.  

Comment out the `faceCtx.drawImage()` line of code for a second to make sure you have the square painting. If you do, that is good.  

Now let's go through every single of the 9 arguments, one by one. 

5 are source args, which means they are about how we pull data out of this video, and then 4 arguments about how we want to paint it into. 

We only want the inside of the square to be painted onto it.

The first argument is where does the source come from, which in this case is our video tag. 

The next two are `face.x` and `face.y`, which are where do we start the source pull from? We are trying to pull the square out so we want to start at the top left corner of the square. 

If we have where we start from, we need to know how wide and how high it needs to go, so we pass `face.width` and `face.height`. That is all the pulling out arguments. 

```js
function censor({boundingBox:face}){
  //draw the small face
  faceCtx.drawImage(
    //5 source args
    video, //where does the source come from?
    face.x, //where do we start the source pull from?
    face.y, 
    face.width,
    face.height,
    //4 draw args
  )
}
```

Now the next four arguments are related to drawing it into the face canvas that we have. We have to ask "where do we start drawing it at?" 
The answer is `face.x` and `face.y`. 

The next arguments are how wide and how high should I paint it to? 
You might think, okay we can just use `face.width` and `face.height`.  However if you try that, you will see a really weird effect where your face is almost delayed. 

What is actually happening there is that it's just painting Wes' face to the square, and then everything you see outside of the square is the video element, and then everything inside the square is the canvas. 

There is a bit of a delay there. 

So the way it will work is we are going to take 10 pixels by 10 pixels and then peel it back up once we have done it. Instead of passing `face.width` and `face.height`, we will pass `10,10`. 

```js
//4 draw args
face.x, //where should we start drawing the x and y?
face.y,
10,
10 
```

![](../attachments/769.png) 40:29

You can see in the very top corner there is a tiny little Wes. 

Make a variable `size` instead of hard coding the values 10,10, so we can quickly reference that whenever we need it.  

Add the following towards the top of the file: `const SIZE = 10;`. 

Why did we do it in all caps? it's a common practice in the graphics canvas world, any variables that are constant throughout the application, they do them in all caps. 
 
```js
faceCtx.drawImage(
  // 5 source args
  video, // where does the source come from?
  face.x, // where do we start the source pull from?
  face.y,
  face.width,
  face.height,
  // 4 draw args
  face.x, // where should we start drawing the x and y?
  face.y,
  SIZE,
  SIZE
);
```

Now we need to draw the small image back on but scaled up. Remember -- the whole reason we draw it small was so we can pull it back out, stretch it back up, and then paint it overtop. Saving it small lets us get that pixelated look that we are going for here. 

To do that we will use `drawImage`. 

The source is the `faceCanvas` itself, and we want to start from the top left corner so we pass `face.x` and `face.y`. 

For how wide and how high we want to go, it's no longer the width of the face, it's the width of the tiny one, so we can pass `SIZE` for both width and height.

Next we have our drawing arguments. 

Where should we start drawing the x and the y? 
`face.x` and `face.y`.

And then for how wide and high should we do it, we want `face.width` and `face.height`.

```js
// draw the small face back on, but scaled up
faceCtx.drawImage(
  faceCanvas, // source
  face.x, // where do we start the source pull from?
  face.y,
  SIZE,
  SIZE,
  //drawing args
  face.x,
  face.y,
  face.width,
  face.height
);
```

If you refresh the page, you might notice it's not working. 

Wes spent 20 minutes debugging this to figure out why is it not painting his face once it is scaled up? Wes' debugging mindset went through and said it looks like it's not actually drawing anything there because if you comment that entire small face `drawImage`, it works the exact same. 

If you give it a separate `src`, like the `video` to pull from instead of `faceCanvas`, you will see it works. 

```js
// draw the small face back on, but scaled up
faceCtx.drawImage(
  video, // source
  face.x, // where do we start the source pull from?
  face.y,
  SIZE,
  SIZE,
  //drawing args
  face.x,
  face.y,
  face.width,
  face.height
);
```

So why is it not painting to the `faceCanvas`? 

Wes switched the source back and then went to the element and set `display:none` on the canvas element with class of `face`, and nothing changed. 

So that's when Wes thought maybe we are drawing to the wrong canvas. But then he thought we have two canvases. 
The first canvas is the regular canvas with `ctx`. 
The second canvas is the canvas with the `faceCtx`.  

So what is wrong with the variables?!

It was right here... 

```js
const faceCanvas = document.querySelector(".face");
const faceCtx = canvas.getContext("2d");
```

We grabbed the `faceCanvas` element correctly, but then we assigned `faceCtx` the wrong canvas! We used `canvas` instead of `faceCanvas`.

```js
const canvas = document.querySelector(".video");
const ctx = canvas.getContext("2d");
const faceCanvas = document.querySelector(".face");
const faceCtx = canvas.getContext("2d");
```

Modify the code above as shown below 👇

```js
const canvas = document.querySelector(".video");
const ctx = canvas.getContext("2d");
const faceCanvas = document.querySelector(".face");
const faceCtx = faceCanvas.getContext("2d");
```

![](../attachments/770.png) 44:27

Now it is finally working! It is taking our faces and spreading it all over. There are few things we can do to fix some of that stuff. 

Go into the `censor` function.  In the first line of the function add `faceCtx.imageSmoothingEnabled = false`.  

If you don't have that, the image is just kind of blurry so what the browser does is it says "oh this is pixelated!, let me try to smooth it out".  But if you turn that off, you get the real pixelated values. 

![](../attachments/771.png) 45:04
![](../attachments/772.png)

We also want to clear the canvas before we do any of this so add `faceCtx.clearRect(0, 0, faceCanvas.width, faceCanvas.height)`.

Now the canvas should clear when we move. 

One other thing is it doesn't do a great job at getting Wes' whole face. What Wes will do is go to the top of the file and create a scale variable like so `const SCALE = 1.5;`

![](../attachments/773.png) 45:33

Go to our second draw and make a few variables that are scaled up. 

First we will make a width and height:

```js
const width = face.width * SCALE;
const height = face.height * SCALE;
```

Then we will go down to the `drawImage` function and replace the last two values with the `width` and `height` variables like so 👇

```js
// draw the small face back on, but scaled up
const width = face.width * SCALE;
const height = face.height * SCALE;

faceCtx.drawImage(
  faceCanvas, // source
  face.x, // where do we start the source pull from?
  face.y,
  SIZE,
  SIZE,
  // drawing args
  face.x,
  face.y,
  width,
  height
);
```

![](../attachments/774.png) 46:18

That makes a bigger scaled up face. Now we need to move the canvas over a bit based on the scale. For that we need a bit of math. 

We will take our drawing args from `faceCtx.drawImage()` and do the following 👇

```js
// Drawing args
face.x - (width - face.width) / 2,
face.y - (height - face.height) / 2,
```

![](../attachments/775.png) 46:51

Now you can play around with the size and scale variables. If you change the size to `const SIZE = 100;`, you will see something like 

![](../attachments/776.png) 47:11
![](../attachments/777.png)

You can feel free to stop the video here, but if you want to continue, we will create some sliders that will change these `SIZE` and `SCALE`  values. 

Make an `options` variable that is an object with properties of `SIZE` and `SCALE` like so 👇

```js
const options = {
  SIZE: 10,
  SCALE: 1.35
}
```

Then everywhere in the code we are calling those variables, modify the code so instead of passing just `SIZE` we pass `options.SIZE`.

```js
// draw the small face back on, but scaled up
const width = face.width * options.SCALE;
const height = face.height * options.SCALE;
```

Go back to the `face.html` and make some controls. 

Give ourselves an input of type "range", with a minimum value of 0.3 and a max of 3 and the step will be 0.1. Then we need to add a label. 

```html
<div class="controls">
  <label for="SCALE">
    SCALE:
    <input type="range" name="SCALE" min="0.3" max="3" step="0.1" />
  </label>
</div> 
```

![](../attachments/778.png) 50:05

Let's make the defaults line up with what we set.  Add `value="1.35"` to the input range. 

![](../attachments/779.png) 50:18

As you can see now the default value is set on the scale slider. 

Duplicate that code and let's do the same for size. Size will start at 10 and go from 1 all the way to 100, and the step will go up by 1. 

```html
<label for="SIZE">
  SIZE:
  <input type="range" name="SIZE" min="1" max="100" step="1" value="10" />
</label>
```

Now we need to add some event listeners. 

Select the inputs first by selecting every input within the `controls` class with a type of "range" 👇

```js
const optionsInputs = document.querySelector('.controls inputs[type="range"]);
console.log(optionsInputs);
```

If you refresh the page and inspect the console, there is nothing! We did make a mistake, we should have used `querySelectorAll`. If you modify the code to that, you will see that it still doesn't give us anything. 

![](../attachments/780.png) 51:46

Oh we have a typo! It should be `.controls input[type="range"]` not `inputs` plural. Modify the code accordingly. 

Make an event listener for each of those. Add the event listener on the `input` so it will run whenever the input changes and then call `handleOption`. 

```js
optionsInputs.forEach(input => input.addEventListener('input',  handleOption));
```

Above that, add the `handleOption` function.

```js
function handleOption(event){
  console.log(event.currentTarget.value);
}
```

Now when you move the slider, you should see the values changing in the console. 

Next we need to pull out the value and name of the input. Log `event.currentTarget.name` as well. 

![](../attachments/781.png) 53:07

Destructure the `value` and `name` variables. 

```js
function handleOption(event){
  const { value, name } = event.currentTarget;
  options[name] = value;
}
```

Inputs always come in as strings so tiy need to convert that back to numbers like so 👇

```js
options[name] = parseFloat(value);
```

Now you can play with the inputs and scale and resize up and down!

That was a long video, but hopefully it was fun for you. 

---

## 56 - Sarcastic Text Generator

This is a quick and fun exercise. You can try this yourself to see how you would structure it.

What we will be doing is building a sarcastic text generator where you can enter some text and then select one of 3 options: 
- sarcastic, 
- funky, or 
- unable to structure a sentence

Based on your selection, the text you entered will be modified to match the style option you selected.

The sarcastic option gives us "sponge bob case" as it's often called, which is depicted in the image below. 

![](../attachments/783.png) 00:34

![](../attachments/782.png) 00:26

![](../attachments/784.png) 00:45

_Note: the funky option gives us those weird characters but you should never use these characters in a real world situation because they are inaccessible to someone with a screen reader._

We will be working out of the `56 - Sarcastic Text` folder. Open up `index.html`. 

The page already contains some base styles so we can center it on the page, then we have a div with a bunch of inputs.

```html
<body>

  <div class="typer">
    <label for="sarcastic">
      <input type="radio" value="sarcastic" id="sarcastic" name="filter" checked>
      Sarcastic
    </label>
    <label for="funky">
      <input type="radio" value="funky" id="funky" name="filter">
      Funky
    </label>
    <label for="unable">
      <input type="radio" value="unable" id="unable" name="filter">
      Unable to Structure a Sentence
    </label>
    <textarea name="text">so I was thinking about going to the store.</textarea>
    <p class="result"></p>
  </div>

  <script src="./text.js"></script>
</body>
```

The only thing we need to know about the inputs is they all have the same `name` attribute value. That allows us to only select one of the radio buttons at a time. We are going to be using their values (sarcastic, funky, or unable) to pull the specific filters. 

First thing you want to to do is select a few things. 

We need the text area that the person will input their text into, the paragraph where we display the result and then all the inputs.

Grab the text area. Use an attribute selector to specify the textarea in case in the future you add more than one to the page.

```js
const textarea = document.querySelector('[name="text"]');
```

Then you need the result.

```js
const result = document.querySelector('.result');
```

Then tiy need the inputs. Use `querySelectorAll` to select all the inputs with a name of "filter" on them. 

```js
const filterInputs = document.querySelectorAll('[name="filter"]');
```

Log them all the make sure they are working.

![](../attachments/785.png) 2:50

Next we need a handler that will output the text. 

Make a new function called `transformText`. It will take in some text and then output the result.

Add an event listener on the input event and call `transformText` every time the event fires. 

To get the text out of the text area to pass to the function, use `e.target.value`. 

```js
function transformText(text){
  result.textContent = 'Transformed Text';
}
textarea.addEventListener('input', e => transformText(e.target.value));
```

Check that it is working by simply logging the text within the `transformText` function. When you refresh the html page, open the console and type into the text area, you should see the text you are typing being logged. 

Now we need to write some filters. 

We have 3 filters, and we will start by writing the sarcastic filter. 

One thing Wes likes to do when we have a few related things like these filters is to stick them in an object instead of having them all as their own function.

Name the object `filters` and each property will be the filter name like so 👇

```js
const filters = {
  sarcastic: function(){

  },
  funky: function(){

  },
  unable: function(){

  },
}
```

You will notice when you save the file that it refactors the object as shown below, which is just a shortcut. It's not the same thing as an arrow function, it's just a shorter way to write functions in objects. 

```js
const filters = {
  sarcastic() {},
  funky() {},
  unable() {},
};
```

Now you need to take the text and loop over every letter, because for "sarcastic text", every other letter is a different case. 

```js
const transformText(text){
  //take the text, and loop over each letter
  const mod = Array.from(text);
  console.log(mod);
  result.textContent = text;
}
```

Now every time you type in the textarea, you should get an array of every single letter that the person has in there. 

![](../attachments/786.png) 5:54

We want to loop over that array and uppercase and lowercase every other letter. 

To do that, we will use `map` and pass it our `filters.sarcastic` function. 

Since this is just a map function, our sarcastic method on the filters can take in all the arguments that a regular map can do. 

Let's use the parameters `letter` and` index` and log those to make sure it's working correctly like so 👇

```js
const filters = {
  sarcastic(letter, index) {
    console.log(letter, index);
    return letter;
  },
  funky() {},
  unable() {},
};

function transformText(text) {
  // take the text, and loop over each letter
  const mod = Array.from(text).map(filters.sarcastic);
  console.log(mod);
  result.textContent = text;
}

textarea.addEventListener("input", (e) => transformText(e.target.value));
```

![](../attachments/787.png) 6:54

Now when you type, as you can see, we are logging the letter and the index. What we can do is say if it's an even number, lowercase it, and if it's an odd number, uppercase it. 

How do you know if a number is even or odd? 

### The modulo operator

There is a neat way of doing that with the **modulo** operator.  Let's do a little aside to go over how the modulo operator works. 

![](../attachments/788.png) 7:41

Let's say Wes he has a pack of 10 smarties (which are a candy in Canada) and three kids. 

If you try to divide 10 by 3 you get `10 / 3 = 3.33333333335`. Well you can't really split a smartie into thirds. You might think we can use `Math.floor(10/3)` which does return 3. 

![](../attachments/789.png) 8:21

So each kid gets 3 smarties. 

If we have a pack of 10, each kid gets 3, if we had a pack of 20, each kid will get six. 

Now the question is, how many are leftover that Wes gets? 

You could try to figure it out using math but it's not the best way. 
[](@attachment/790.png) 8:50

What you can do is you can use the modulo operator. Let's say you have 10 smarties, and 2 kids. The modulo operator will tell us after they are evenly divided, how many are left.

```js
10 % 3 = 1
```

![](../attachments/791.png) 9:17

So if we have 10 smarties that we divide by 3, there will be `one` leftover. 
If we have 6 smarties, there will be 0 leftover.

The modulo operator is great for knowing how much is left after you have evenly divided. 

We can use this operator to check if something is even or not. 

`10 % 2` will be 0, because 10 is even. 
If you do `11 % 2` you will get 1 returned. 

So anytime that 1 is returned with the modulo operator you know it's odd and if 0 is returned, then it's even. 

We can use this to upper/lowercase every other letter in our sarcastic filter. 

```js
const filters = {
  sarcastic(letter, index) {
    // if it is od, it will return 1 which is truthy.
    if (index % 2) {
      return letter.toUpperCase();
    }
    // if it is even, it will return 0 and we will lowercase it.
    return letter.toLowerCase();
  },
```

If you refresh the page and start typing, you will see that every other letter is uppercase. 

![](../attachments/792.png) 12:02

Set the result to be `mod.join(' ')`. 

```js
function transformText(text) {
  // take the text, and loop over each letter
  const mod = Array.from(text).map(filters.sarcastic);
  console.log(mod);
  result.textContent = mod.join("");
}
```

Now if you type in the textarea and select the sarcastic filter, you should see something like this 👇

![](../attachments/793.png) 12:15

So that is our first filter, and we are just hard coding it in our `transformText` function right now. But it would be great if we can use it based on the radio selection that we have.

How could we do that? 

We can modify the first line of `transformText` to grab the filter by finding the input with name of filter that is also checked, and then grabbing it's value. 

```js
const filter = document.querySelector('[name="filter"]:checked').value;
console.log(filter);
```

![](../attachments/794.png) 13:04

Now when we type in it, we get the selected filter type logged in the console. 

![](../attachments/795.png) 13:19

Another way we could have done the filter is because we already have the inputs, we could use the find method to find the input that is checked like so 👇

```js
filterInputs.find(input => input.checked);
```

![](../attachments/796.png) 13:49

If you try that, you should notice an error in the console that says
>filterInputs.find is not a function. 

That is because `filterInputs` is a NodeList, not an array. We could wrap it in `Array.from` and then call `find` like so 👇

```js
Array.from(filterInputs).find(input => input.checked);
```

![](../attachments/797.png) 14:05

This is actually a better approach because why rerun the query selector if we have already selected all of the inputs!

Change the code to use that instead. 

```js
function transformText(text) {
  const filter = Array.from(filterInputs).find((input) => input.checked).value;
```

With the way the code is written now, we will be transforming our `filterInputs` into an array every time the person types. That is not ideal. 

Let's instead turn it into an array once on page load because it is unnecessary to have to keep doing that. 

Modify the code like so 👇

```js
const filterInputs = Array.from(document.querySelectorAll('[name="filter"]'));
```

Let's do some cleanup and get rid of the logs within the `transformText` function. 

Take the `filter` variable and use it as a property lookup instead of hard coding the value.

```js
const mod = Array.from(text).map(filters.sarcastic);
```

Replace the line of code above 👆 with the code below 👇

```js
const mod = Array.from(text).map(filters[filter]);
```

Because filter is stored in a variable, we need to use square brackets to look up the property. 

If you refresh the page, the sarcastic option should still work but nothing should happen when you select the other 2 options because we haven't hooked them up yet.

Let's do funky now. Add the parameter `letter` to the function, like so 👇

```js
funky(letter){},
unable() {},
};
```

We need some sort of dictionary or lookup of funky letters. If you open the `text-DEMO` or `text-FINISHED` file, you will see an object of funky letters.

Copy that variable along with the `/* eslint-disable */` and `/* eslint-enable */` comments into our text.js file.  

Paste it towards the top of the file, after our `filterInputs` declaration. 

![](../attachments/798.png) 16:15

This object is just a lookup of letters that match to funky letters. 

We kept the ESLint disable comments because otherwise when you save the javascript file, it formats the object so each property is on it's own line, which makes it hard to work within the file because it becomes so long. 

Back to our funky function logic, we need to do the following:
- Check if there is a funky letter for this case
- If there is no funky letter for this case, check if there is a lowercase version. 
- If there is nothing, return the regular letter

You have the `letter` argument, which you can use to look up inside of `funkyLetters`. For example if someone types `T`, we know there is a t for us to use. 

![](../attachments/800.png) 17:43

Add the following code 👇

```js
let funkyLetter = funkyLetters[letter];
```

What we are doing there is we are looking up the letter in our `funkyLetter` object and assigning the value to our `funkyLetter` variable. 

If there is a funkyLetter, we will return it. 
If there is not, we will return the original letter. 

```js
funky(letter) {
  // first check if there is a funky letter for this case
  const funkyLetter = funkyLetters[letter];
  if (funkyLetter) return funkyLetter;
  // if there is not, check if there is a lowercase version
  // if there is nothing, return the regular letter
  return letter;
},
```

If you refresh the page and try typing something while selecting the funky radio button, you should see it start working. 

![](../attachments/801.png) 18:27

If no `funkyLetter` is returned, we want to check for the lowercase version of it because some letters have a funky version for both lower and uppercase, like `f`.

![](../attachments/803.png) 18:37

To do that, we will modify `funkyLetter` to be a `let` instead of a `const`, and then after the comment where we check if there is a lowercase version, we will try to grab the lowercase version by lowercasing the letter and looking it up in the `funkyLetters` object and then assigning the value to  `funkyLetter`. 

If a value is found, we will return it, otherwise we will just return the letter as is. 

```js
funky(letter) {
    // first check if there is a funky letter for this case
    let funkyLetter = funkyLetters[letter];
    if (funkyLetter) return funkyLetter;
    // if there is not, check if there is a lowercase version
    funkyLetter = funkyLetters[letter.toLowerCase()];
    if (funkyLetter) return funkyLetter;
    // if there is nothing, return the regular letter
    return letter;
  },
```

The last one is `unable`. It will take in a letter, and what we will do is one-in-three spaces, we will use the dot dot dot. 

So we need a random number between 0 and 2, such as 1, 2, or 3 or 0, 1, 2. 

The way that we can do that is using `Math.random() * 3`. That returns a number with decimals so we need to wrap it in a `Math.floor()`. 

![](../attachments/804.png) 20:06 

Now we will get 0, 1, or 2 returned. Grab that random number within the `unable` function. 

```js
const random = Math.floor(Math.random() * 3);
```

Next you are going to check whether the letter is equal to an empty space, and that the random is equal to 2 (so 1 in 3), then return `"..."`. 
Otherwise, we just return the letter. 

```js
unable(letter) {
  const random = Math.floor(Math.random() * 3);
  if (letter === " " && random === 2) {
    return "....";
  }
  return letter;
},
```

Now if you refresh the page, select the unable option and try typing into the textarea, there is a one in three chance that the space will be turned into a `...` 

![](../attachments/805.png) 21:13

The last thing we want to do is when you click on the radio button options, it should trigger that filter and show you the result. 

To do this, take `filterInputs` and loop over each one of them. 

Add an event listener that listens for the input event, and then when there is an input event, we will call another function which calls `transformText` and passes the text from the textarea. 

```js
filterInputs.forEach((input) =>
  input.addEventListener("input", () => {
    transformText(textarea.value);
  })
);
```

Now each of our filter inputs have an event listener that listens to the input event, and when that fires, it triggers the `transformText` event and passes the value of the text. 

If you refresh the page, you should be able to select the different radio buttons and the text formatting will change based on the filter you select.

The main thing Wes wanted to get across in this lesson is that you can store methods inside of an object, to keep them together, as well as look them up on that object with a variable that is populated from some external input. 

---

## 57 - Shopping Form with Custom Events, Delegation and localstorage 

In this lesson we will build a shopping list, where you can add items, check them off, and delete them.

![](../attachments/806.png) 00:24

Although you may have written something like this before, Wes has baked a lot of things that we need to learn about Javascript into this simple example.  

We will be learning about emitting **custom events**, such as the one highlighted in the image below (if you don't know what a custom event is, don't worry, we will be learning about it). 

![](../attachments/807.png) 00:40

We will also be learning about **event delegation**, how do you listen for clicks on things that happen in the future, as well as **DOM events**, and **local storage**.

If you open up the `index.html` file in the `exercises/57 - Shopping List` directory, let's go over the code that we are starting with. 

We have a div with a class of `shopping-list` which contains a form element and an empty `ul`. Within that ul, we will be outputting the shopping list items. 

The form has input and submit buttons.

```html
<body>
  <div class="shopping-list">
    <form class="shopping">
      <input type="text" name="item" id="item">
      <button type="submit">+ Add Item</button>
    </form>

    <ul class="list"></ul>
  </div>

  <script src="./shopping.js"></script>
</body>
```

With this exercise, you can right-click and open the file in the browser and everything should still work. However if you do want the live reloading, and instant CSS changes, we can use Parcel, which will give us a server, live reloading and module bundling (which we have yet to learn about). 

There are 2 ways to install Parcel on your machine. You can:
1. install it once, to each project, which is what we did in the last exercise, or 
2. install it globally on your machine so that anytime you need it you can get a little server up and running. 

To install Parcel globally on your machine, open the terminal and type `npm install -g parcel-bundler`. That will globally install Parcel for you, so that anytime you are in a terminal, Parcel will be available to you. 

![](../attachments/810.png) 3:00

If you are on a Mac and you have trouble installing global modules on your command line, type `sudo` in front of the command like so `sudo npm install -g parcel-bundler`.  That will ask you for a password first. 

To check if it worked, you can type `parcel --version` into the terminal and it will tell you what version you have.

Now in the terminal, cd into the Shopping List directory and then type `parcel index.html` in the terminal and hit enter. 

There will be a message in the terminal telling on which server it is running (usually localhost:1234).

![](../attachments/811.png) 3:59

 ![](../attachments/812.png) 

 Let's get started. Open the `shopping.js` file, which should contain nothing. 

 There are a couple of things that need to happen. We need to:
 - listen for when someone types into the input and hits the submit button
 - keep track of all of the shopping list items and whether or not they are complete
 - render out a list of all of the shopping items

_Note: you may notice when you focus into the input to enter a shopping list, all these values of everything you have ever typed show up, like in the picture below. To fix that, you can go to the HTML, you can set autocomplete to false on either the input or the whole form. There is also an `autocapitialize` attribute which you can switch on or off._ 

![](../attachments/813.png) 5:17

```html
<form class="shopping" autocomplete="off">
```

Back to our javascript, let's start by grabbing the shopping form and the list elements. 

```js
const shoppingForm = document.querySelector(".shopping");
const list = document.querySelector(".list");
```

Next we need an array to hold our **state**. 

```js
//We need an array to hold our state
const items = [];
```

What does **state** mean? 

The definition changes from framework to framework, but generally what people are saying is that state is a bunch of data that reflects the state of your application. 

But what does that mean? Let's use this finished shopping list screenshot below as an example. 

![](../attachments/814.png) 7:09

In this example, state is going to contain a list of all of your items, a list of those item ids, and whether they have been completed. 

If it was a shopping cart, state would be a list of all the items in the card, how many of each item was in the shopping cart, how expensive is each item, etc. 

You should always be able to recreate the visual part of your application given just the data. 

All of the current state of your application, meaning how it currently is, should always be reflected in some sort of object or array of data and that is what we refer to as **state**. 

Next we need to listen for a submit event on the form. 

If you refresh the page and try to type an item in the input and hit submit, you will notice that the form submits, it puts `?item=Egg` in the URL bar. 

However that is not what we want. 

![](../attachments/815.png) 8:01

![](../attachments/816.png) 8:13

Let's make a submit handler for that. 

The first thing the handler needs to do is prevent the form from submitting so add `e.preventDefault()`. 

```js
function handleSubmit(e){
  e.preventDefault();
}
```

Grab the `shoppingForm`, add an event listener on the submit event and pass it the `handleSubmit` callback. 

Remember, for forms, we don't use click or enter events because it's much easier to just listen to the submit event. That way, if you submit by clicking, you submit by hitting enter, something else triggers a submit of the form, all of those use cases are covered by a single event called `submit`. 

```js
shoppingForm.addEventListener('submit', handleSubmit);
```

If you refresh the page, type in eggs and hit enter, nothing should happen, which is good. 

Log "submitted" in the `handleSubmit` function. 

Next we need to pull the data out of the input. How can we get that? 

Within the `handleSubmit` function, add the following code after we log "submitted".

```js
function handleSubmit(e) {
  e.preventDefault();
  console.log("Submitted!!!!");
  const name = e.currentTarget.value;
  console.log(name);
}
```

If you refresh the page now, type in eggs and hit enter, you should get something like below in the console. 

![](../attachments/817.png) 10:00

Why are we getting `undefined`? 

Let's do a bit of debugging. 

Log of `e.currentTarget` in our handler, and then refresh the page. You should see the form element logged. 

![](../attachments/818.png) 10:13

The reason we are getting `undefined` is because the `currentTarget` is the form, not the input and we want to get the text out of the input.  There are a couple ways we could do this. 

We could write another query selector to grab it. However, because the input has a name, it's actually accessible via the form dot the name of the input. 

```html
<input type="text" name="item" id="item>
```

![](../attachments/819.png) 10:34

Take the form and store it as a global variable, called `temp1`, then add `console.dir(temp1)` to get every property inside of it.

![](../attachments/820.png) 10:56

Somewhere inside of all those properties is `item`. 

Wes is having trouble finding it but we will demonstrate it with code. 

Modify the log of `console.log(e.currentTarget)` to `console.log(e.currentTarget.item)`. 

![](../attachments/821.png) 11:04

As you can see, we now get the item, not the entire form itself. 

Modify the name declaration to `e.currentTarget.item.value` like so 👇

```js
function handleSubmit(e) {
  e.preventDefault();
  console.log("Submitted!!!!");
  const name = e.currentTarget.item.value;
  console.log(name);
}
```

As you can see, now we can capture the value of eggs. 

![](../attachments/822.png) 11:20

Next step is to store the data about the shopping item in the `items` array, but we cannot just store the straight up string, because we need to be able to store a bit more info about that item. 

The other two things we need to know are:
- is it completed (have you bought it or not?) 
- what is the ID of the item?  

Any time you have a list of items, it's best to give every single one a unique identifier, so you can easily find it from within the list. 

That is what we are going to do now. 

The name of the item is going to be our name variable. 

The id of the item just needs to be something unique. One trick that Wes likes to use is to use `Date.now()` as an ID, which works if you aren't creating more than one item per millisecond, which works for our case.  

![](../attachments/823.png) 12:17

The third property will be `complete` which we will set to false when the item is added to the list.  

```js
function handleSubmit(e) {
  e.preventDefault();
  console.log("Submitted!!!!");
  const name = e.currentTarget.item.value;
  const item = {
    name: name, 
    id: Date.now(),
    complete: false
  }
}
```

_Note: when you save the code above, it might refactor it due to prettier to look more like what you see below, which is fine._ 

```js
const item = {
  name,
  id: Date.now(),
  complete: false,
};
```

Next we need to push these items to our state, which we will do by adding the following code to the `handleSubmit` function. 

```js
items.push(item);
console.log(`There are now ${items.length} in your state`);
```

If you refresh the page and try adding a few items, you should see the count in our log increasing. 

![](../attachments/824.png) 13:32

Next we need to clear the form. There are a few ways we can do this. 

One way is to set the item's value to nothing like so 👇

```js
event.currentTarget.item.value = '';
``` 

Another way you can do it, and this works if there are multiple inputs, is to call `e.target.reset()`. 

That will clear all of the inputs in a particular form. 

Notice that we used `e.target` not `e.currentTarget`. If we used `e.currentTarget` it would still work the same in this scenario. 

```js
function handleSubmit(e) {
  e.preventDefault();
  console.log("Submitted!!!!");
  const name = e.currentTarget.item.value;
  const item = {
    name,
    id: Date.now(),
    complete: false,
  };
  // push the items into our state
  items.push(item);
  console.log(`There are now ${items.length} in your state`);
  // clear the form
  e.target.reset();
}
```


When we have a form event, it will only actually ever fire on the form, it doesn't bubble like our clicks and hovers do. 

In this case, there is no upside or downside to using `target` vs `currentTarget` to reset the form using the `.reset()` method. 

So far we have written code to enter an item and push that item up to state. 

Next, we need to display the items that are in our state. Create a function called `displayItems` which will loop over each item in the array and return a list item for each. 

What is the best method to loop over an array and return some HTML for each one? Map! 

Why? 

Let's go over a little demonstration in the console. Let's say you have an array of names like `const names = ['wes','kait'];`. 

You can call `map` on the `names` array which will go over each of them and then you can just wrap each one in a list item tag as a string using interpolation and then you can call `.join('')` on the returned array to join all the list item strings like in the image below. 

That is what we will be doing with the `items` array. 

![](../attachments/825.png) 16:01

```js
function displayItems() {
  console.log(items);
  const html = items.map((item) => `<li>${item.name}</li>`);
  console.log(html);
}
```

Now how do we run `displayItems`? You might be thinking that we need to display them after we submit, right? 

We could just add `displayItems()` right after the `e.target.reset()` call within the `handleSubmit` function. That is okay for now, but Wes will show us a better way to do it, and why, with custom events. For now, just add it to our `handleSubmit()` function. 

Refresh the page and test that out by adding a few items: egg, milk and then beer, and you should see something like what is displayed below in the console. 

We pushed the item into state, and then once that is finished `displayItems` run and that loops over each item and returns a list item with each of them. 

![](../attachments/826.png) 17:12

A couple of problems there... 

First, the list items returned to us are in an array, not in an HTML string. 

To fix that, add a `.join('');` on the `html` variable declaration like so:

```js
const html = items.map(item=>`<li>${item.name}</li>`).join('');
console.log(html);
```

Now as you can see, we are returned one string. 

![](../attachments/827.png) 17:41

Take the list and set the innerHTML of it, within the `displayItems` function. 

```js
function displayItems() {
  console.log(items);
  const html = items.map((item) => `<li>${item.name}</li>`);
  list.innerHTML = html;
}
```

Now when you type in an item and enter submit, you will see it displayed.
  
![](../attachments/828.png) 18:00  

We need to add a bit more to our HTML like a delete button and a complete checkbox. Let's scaffold the HTML out a bit more for each item. 

Add a class of `shopping-item` to each list item. 

We also need to add a checkbox as well as a button with `&times;` which should give us an x. 

```js
function displayItems() {
  console.log(items);
  const html = items
    .map(
      (item) => `<li class="shopping-item">
    <input type="checkbox">
    <span class="itemName">${item.name}</span>
    <button>&times;</button>
    </li>`
    )
    .join("");
  list.innerHTML = html;
}
```

If you refresh the page and try entering items, you should see something like the following 👇

![](../attachments/829.png) 19:35

We need to fix a few things here. 

The button that we added is currently not accessible to people who are using screen readers. If the screen reader were to read to the user what is currently on the page, it would read the item's name and then the multiplication sign, which makes no sense. 

What we can do to fix that is to add an `aria-label` attribute to it. 

For sighted users, nothing changes, but for people using a screen reader, when they tab over to it, it will tell them "remove bananas" instead. 

```js
<button aria-label="Remove ${item.name}">&times;</button>
```

Another thing we need to do is when you check one of the items, we need to add the item to our state and update the checked property. 

First, let's fix the problem happening now where if you don't type anything into the input and hit enter, you will see we are able to submit a lot of blanks. 

One way to fix that would be to add the required attribute to the input, as shown below. 

```js
<input type="text" name="item" id="item" required>
```

That is an example of **client-side validation**. 

Another thing we can do is say if there is no name, return within our `handleSubmit` function like so 👇

```js
function handleSubmit(e) {
  e.preventDefault();
  console.log("Submitted!!!!");
  const name = e.currentTarget.item.value;
  //if it's empty, then don't submit it. 
  if (!name) return;
  const item = {
    name,
    id: Date.now(),
    complete: false,
  };
```

Now if you try to submit a blank input, you will see that no item is added because we just return from the function. 

If you try entering any of the following: `0, null, undefined, false` in the input, it will still get added to the list instead of being returned, even though they are falsy. 

Why is that? Because they are all strings, and not types. 

Let's go back to how we are calling `displayItems` each time the `handleSubmit` function is called. The reason Wes doesn't love that approach is because it tightly couples the `handleSubmit` with the displaying of the items. 

What will happen is that we will also need to display the items when they are restored from local storage (when we refresh the page, we want the items to still be there) so we would need to call it again. 

We also need to display the items when we mark them as complete. 

When we delete an item we will need to re-run `displayItems` because there is now one less item. And we call `displayItems` from a couple of other spots. 

Having those functions so tightly coupled now isn't a big deal but what happens in larger JS applications is you may need to do more things after you display the items, and then sometimes you won't want to run all those other things after displaying the items. So what people end up doing is copy and pasting the function and modifying it slightly which causes duplicated logic. 

Instead, what we are going to do is use the event system in Javascript to fire off our own events, and then listen for them.

We are going to listen to an item updating event, and then anyone who cares about that event can listen for it, just like if it were a click or a hover. 

That allows us to decouple it, and you will see this pattern a lot in Javascript applications. 

Let's do that right now. 

Instead of displaying our items, we will fire off a custom event which will tell anyone who cares that our items have been updated. 

We will be using the term **dispatch** which means an event happens. 

When you click on something, the browser dispatches a click event. 

We need something to fire off an event about that data and we need to attach it. 

If we look at our HTML, we will probably fire off the event from this list. You could also fire it off from the form or the body, it doesn't matter that much. 

![](../attachments/830.png) 25:44

At the bottom of the `handleSubmit` function, run `list.dispatchEvent()`. The `dispatchEvent` method lives on all DOM elements. You provide it a `CustomEvent`, which is a constructor in the browser.

As you can see, it's just a function. 

![](../attachments/831.png) 26:12

```js
new CustomEvent('PIZZAS HERE')
```

If you were to run it by passing the name of your event, as shown above, you should see something like the image below in the console. 

![](../attachments/833.png) 26:45

It gives us the type of events, as well as any details about when it is fired. 

So when we want to dispatch a custom event, we must first create a new `CustomEvent`, by passing the constructor the name of the event. 

```js
list.dispatchEvent(new CustomEvent('itemsUpdated'));
```

If you try to add an item now, nothing happens, it just dispatched that event. No one is listening for `itemsUpdated` so no one cares, but if we go down to the bottom of the javascript file, where we have added our event listeners, we can listen for that event like so...

```js
list.addEventListener('itemsUpdated', displayItems);
```

Now when you add an item, you will see it in the list. That is because we are dispatching the `itemsUpdated` event and also listening to it, and then calling `displayItems` when it fires. 

You can add as many event listeners to the same event as you want.

If we were to add the following code and refresh the page and add an item, we can see the details of the event. 

```js
list.addEventListener('itemsUpdated', e=> {
  console.log(e);
});
```

![](../attachments/834.png) 28:17

You can see all sorts of details such as the path, which is pretty neat because it shows you the path at which the events have bubbled through. It was first triggered on the `ul`, then bubbled up to the shopping list, then the `body`, `html`, `document` and then the `window`.  

That is a **custom** event, which Wes uses often when working with vanilla javascript to keep concerns separate, instead of tightly tying them together. 

Remove the second event listener where we are just logging the event. 

### `localStorage`

Next, we want to mirror the data to **local storage**. 

Local storage is kind of like a mini database that lives in your browser. It allows users who are using your website to come back with the same browser and pickup from where they last left. It does not send data to a server. It's just the ability to save some data in the user's browser. 

If you go to the "Application" tab of the chrome developer tools and look at Local Storage, and then click on the domain name, you won't see anything. However Wes has already completed it so he has values there. There is all this information in his local storage about the items. 

![](../attachments/835.png) 29:25

So what we want to do now is create a function that will mirror our data to local storage.

```js
function mirrorToLocalStorage(){
  console.info('Saving items to localstorage');
}
```

When we add something, we need to listen for the event, and then mirror all the items to local storage.  Let's duplicate our event listener and call `mirrorToLocalStorage` when the `itemUpdated` event is triggered. Add the following code where we call the rest of our event listeners..

```js
list.addEventListener("itemsUpdated", mirrorToLocalStorage);
```

See how nice having a custom event is? 

Anyone who cares about items updating can listen in on the event. 

If you try typing in an item, you should see logged in the console "Saving items to local storage". 

How do you save items to local storage? 

The API is pretty simple. 

If you type in `localStorage` in the console, it will return to you everything that is in local storage.

![](../attachments/836.png) 30:34

To set an item in local storage, you can use `localStorage.setItem()` where you pass in the key and the value.

To get an item from local storage, you can use `localStorage.getItem()` to which you pass the key that you are looking for. 

If something funky is happening with local storage, it's best to just clear it out and start fresh which you can do by clicking this button in the Applications tab. 

![](../attachments/837.png) 31:05

So how are we going to save items to local storage? 

What if we do something like the following 👇

```js
function mirrorToLocalStorage() {
  localStorage.setItem(items, items);
  console.info("Saving items to localstorage");
}
```

If you take a look, you will see `[object Object]`.. what is that? If you try to open it up, you can't, it's just the word object.

![](../attachments/838.png) 31:39

Why is that? That is because local storage is text only. That means if you have an object or an array or a boolean, it will try to convert that item to text first before it puts it in. 

Every single type has a `.toString()` method, which will convert it to a string.

![](../attachments/839.png) 32:37

If you have an object, and you call `.toString()` on it, it just gives you `"[object Object]"`, which is not helpful at all. 

![](../attachments/840.png) 32:56

That is what is happening here, because we are passing it an object, it is trying to convert it to a string which isn't very helpful because there is no data for that.

So how do you convert objects to strings? 
Using JSON. 

If you call `JSON.stringify()`, you can pass it an object, and it will convert that object to a string representation of that object. 

At a later point in time, we can do the opposite which is `JSON.parse()`. If you pass it a string, it will convert it back to an object. 

That is exactly what we will do here. Before we put the object into local storage, we will convert it to a string and when we pull it out of local storage, we can convert it back to an array of objects.

Modify the code as shown below. 

```js
function mirrorToLocalStorage() {
  localStorage.setItem(items, JSON.stringify(items));
  console.info("Saving items to localstorage");
}
```

If you try to add some items now, you will see those changes reflected in local storage. 

![](../attachments/841.png) 34:18

In order to mirror everything to local storage, we need another function that restores from local storage when you load the page.

```js
function restoreFromLocalStorage(){
  console.log('Restoring from local storage');
}
```

We will run that on page load so you can add the call `restoreFromLocalStorage()` to the end of the javascript file. 

If you refresh the page, you should see the message in the console. 

Now we need to pull the items from local storage. 

To do that, call `localStorage.getItem()` which will bring us back a large string of text. Convert it back into an object by wrapping the `getItem` method around `JSON.parse()` which will convert the text back into an array of objects 👇

```js
function restoreFromLocalStorage() {
  console.info("restoring from LS");
  const lsItems = JSON.parse(localStorage.getItem("items"));
}
```

Next we want to check if there are any items in the `lsItems` array, because it could be that this is the first time the user is loading the application, and there isn't even an empty array yet. 

If there is something in local storage, we will assign the value to the `items` variable and then dispatch the `itemsUpdated` event. 

```js
if(lsItems.length){
  items = lsItems;
  list.dispatchEvent(new CustomEvent('itemsUpdated'));
}
```

However if you refresh that you will see an error in the console that "items" is ready only. 

Why? Because it's a const variable. 

We can fix that a few ways. We can change the variable from a `const` to a `let`, or push all the items into the items array like so 👇

```js
lsItems.forEach(item=> items.push(item));
```

We could also use a combination of push and the spread operator as shown below. 

```js
items.push(...lsItems);
```
 
Why does that work? 

That works because push takes unlimited arguments. We could have called `items.push(lsItems[0], lsItems[1])` and that would have worked fine, but using the spread operator it takes each item in the array and spreads it into the method as an argument.

Two more things we need to do. We need to handle: 
1. the clicking of the checkboxes. As it stands right now, you can check the item but when you refresh the page, it will no longer be checked. It is not being mirrored to the state
2. The deleting of items 

Let's start with deletion. 

You might think we could select the buttons on the page, loop over them and listen for a click, and when that happens, remove it from our array. That is kind of right, but let's show you why that doesn't exist. 

Add the code below to the very bottom of the javascript file/

```js
const buttons = list.querySelectorAll('button');
console.log(buttons);
```

You should get 5. 

![](../attachments/842.png) 39:30

However, if you move that code further up, above the event listener declarations, we get none. 

![](../attachments/843.png) 39:34

Why is that? 

Because when we run the code from a bit further up in the file, none of the rest of the code below it has been executed and thus all those event listeners have not yet been created. So that means we have not yet created any of the items. 

If you throw a `debugger;` after  `console.log(buttons);` and refresh the page, you will see that when the debugger hits, there are no items yet. 

![](../attachments/844.png) 40:10

That happen a bit later. So you may think it's safe to leave that code at the very bottom of the page. Let's try that. 

Create a function `deleteItem` which takes in an `id` and for now simply logs that it is deleting an item. 

```js
function deleteItem(id){
  console.log("DELETING ITEM!");
}
```

If you try pressing all the delete buttons, you will see that it works. 

However, if we were to add a new item, if you click on the x, it doesn't say deleting item. 

If you try to click any of the delete buttons that worked before we added the item, you will notice that it no longer works. 

Why?? There are 2 things going on. 

If you try to listen for clicks on things that do not exist on the page, it will not attach an event listener to that element. That is why the code behaved so differently when we moved it above the event listeners. 

The second problem is that when we add a new item, it re-renders the entire list. 

If you have the console open while you add an item, you will notice that for a second the `ul` disappears and is added back, because it is re-rendering. 

That is because we have re-run the `displayItems` function, and it's actually creating a brand new list item each time. 

When you remove an item from the DOM, and replace it with a new item, all of those event listeners are lost. 

We would have to manually add them back, which is a pain.

So what do we do?   

### Event Delegation

We can use a concept called **event delegation**. 

What that means is instead of listening for clicks on things that might not exist yet, or things that will come in the future, what we do is listen for clicks on things that we do know will be there, and then we check if the things that they actually clicked on is a lower item. 

Let's demonstrate this. 

Get rid of the button log and query selector, but keep the `deleteItem` function. 

Let's listen for a click on the list, and then in the event handler log both `e.target` and `e.currentTarget`. 

```js
list.addEventListeners('click', function(e){
  console.log(e.target, e.currentTarget);
});
```

If you refresh the page and then click anywhere on it, you will see that it thinks we are click on the span, even though we listened on the list. 

![](../attachments/845.png) 43:55

Now if you click on the x next to an item, we listened on the list but we actually clicked on the button. 

`currentTarget` is the thing that you listened on and the `target` is the thing that you actually clicked on.

![](../attachments/847.png) 44:00

Now we need to check if what was clicked matches the button, using `e.target.matches('button')`. That will check if an element matches a CSS selector, which in this case is `button`, then we will delete the item by passing the delete method the id of that item. 

```js
// event delegation: We listened for the click on the list <ul> but then delegate the click over to the button if that is what was clicked.
list.addEventListeners('click', function(e){
  if(e.target.matches('button')){
    deleteItem();
  }
});
```

Now, when you click on any X next to an item, you should see "DELETING ITEM". 

If we add a new item and then click on it's X button, we should still see "DELETING ITEM", because we are simply just listening on the `ul` and delegating the event to the delete button. 

One more thing we should mention is that whenever we add an item to the list, we re-render the entire list. We are basically deleting the existing list and adding a brand new one. This happens so quick you can't even see it happening but on large applications, that can slow down how your application works. 

That is where frameworks like Angular, React, Vue come in handy. They know how to instead of re-rendering the entire list, only update a specific piece of it. 

Just changing part of the DOM rather than wiping it out leads to better performing applications. That is hard to do in just Vanilla JS. For our purposes, the way we are doing it is fine. 

Next, when someone clicks on the x, we need to figure out which item id is it related to. Give the button a value of the item's id upon creation, as shown below  👇

```js
function displayItems() {
  console.log(items);
  const html = items
    .map(
      (item) => `<li class="shopping-item">
    <input type="checkbox">
    <span class="itemName">${item.name}</span>
    <button 
      aria-label="Remove ${item.name}"
      value="${item.id}"
    >&times;</button>
  </li>`
    )
    .join("");
  list.innerHTML = html;
}
```

Now when you look at the HTML, you should see the id is in the button. 

Pass that value to the `deleteItem` function. 

![](../attachments/848.png) 47:11

Modify the code like below.

```js
list.addEventListener("click", function(e) {
  if (e.target.matches("button")) {
    deleteItem(e.target.value);
  }
});
```

Add a log for the id in the `deleteItem` function.

![](../attachments/849.png) 47:35

That works now, because when you click on the button, you take the value of the button and pass it as an argument to `deleteItem`, which then logs that argument. 

How can we update our `items` array to remove that one item? 

It's actually pretty simple. Filter for every item that is not the one with the ID.

```js
const newItems = items.filter(item => item.id === id);
```

That is the opposite, but we will flip it in a second. 

Now if you press the delete button next to an item, we get nothing. 

![](../attachments/850.png) 48:35

If we change the code from `===` to `==` will it work? 

Let's try that. Modify the code like below.  

```js
const newItems = items.filter(item => item.id == id);
```

Why does it work with double equals? 

That is because the `id` is being stored as a number, but when you pull it out, it is returned as a string. 

```js
deleteItem(parseInt(e.target.value));
```

When you pass the value to the `deleteItem` function, you can wrap it in `parseInt` as shown above, which will convert it to a number for us. 

Now you can add back the triple equals. 

Now when you click the button, you will get the item that needs to be removed. 

![](../attachments/851.png) 49:13

```js
const newItems = items.filter(item => item.id !== id);
```

We actually want the opposite so modify the line of code as shown above 👆.

If you were to click the delete button for an item now, and you had 12 items, you would only get 11 returned. 

![](../attachments/852.png) 49:21 

We need to get the new items into our items array. How can we do that?

In our case, we just want to overwrite the entire list. To do that, change the declaration of the `items` array from a `const` to a `let`. 

In `deleteItem`, modify the code so instead of assigning the filter to a variable `newItems`, you will assign it to `items` instead so it overwrites whatever the previous value was. 

```js
function deleteItem(id) {
  console.log("DELETING ITEM!!!", id);
  items = items.filter((item) => item.id !== id);
}
```

Now if you click the items, you can tell they are deleting because the array that is being logged keeps getting smaller but if you refresh the page, you will see they are all still there. 

There are 2 things we need to do. We need to:
1. re-render everything
2. localStorage

You might notice that both of those things are bound to the `itemsUpdated` event. That means you can just fire another `itemsUpdated` event as shown below 👇

```js
function deleteItem(id) {
  console.log("DELETING ITEM!!!", id);
  items = items.filter((item) => item.id !== id);
  list.dispatchEvent(new CustomEvent("itemsUpdated"));
}
```

Now it should just work, and when you click the item, it should be removed as you do it. 

Why? 

Because your event listener is listening for the items to be updated and then will do the respective work, mirroring them to the page and updating.

The last thing we need to do is handle the checking and un-checking of the data. 

If we have 3 items and 2 were checked, that information should persist when we refresh the page.

Create another function, `markAsComplete`, which will take in an `id`. 

What do we listen for in our case? We want to listen for a check of the checkbox. 

We can use event delegation for that as well. We could add another event listener or do it inside of our existing click event listener. 

Let's do it inside of the existing one. 

```js
list.addEventListener("click", function(e) {
  if (e.target.matches("button")) {
    deleteItem(parseInt(e.target.value));
  }
  if (e.target.matches('input[type="checkbox"]')) {
    markAsComplete();
  }
});
```

Our checkbox input currently does not have an `id` on it, so let's fix that.

Go to where we make the HTML and modify the code as shown below. 

```js
const html = items
  .map(
    (item) => `<li class="shopping-item">
  <input type="checkbox" value="${item.id}">
  <span class="itemName">${item.name}</span>
  <button 
    aria-label="Remove ${item.name}"
    value="${item.id}"
  >&times;</button>
</li>`
  )
  .join("");
```

Now, we have the value of the `id` in the input so we can go to our event delegation and pass the id like so 👇

```js
if (e.target.matches('input[type="checkbox"]')) {
  markAsComplete(parseInt(e.target.value));
}
```

Now when you check them, you should see "marking as complete" with the id logged to the console. 

![](../attachments/853.png) 53:17

We are repeating ourselves a bit in our event delegator so refactor it as shown below 👇

```js
list.addEventListener("click", function(e) {
  const id = parseInt(e.target.value);
  if (e.target.matches("button")) {
    deleteItem(id);
  }
  if (e.target.matches('input[type="checkbox"]')) {
    markAsComplete(id);
  }
});
```

Back to the `markComplete` function, we have to actually find the item that we need to set as completed. 

How do we look for it? We can use `find`. 

Look for an item whose `id` matches the `id` that was passed in, using the code below. 👇

```js
function markAsComplete(id) {
  console.log("Marking as complete!", id);
  const itemRef = items.find((item) => item.id === id);
  console.log(itemRef);
}
```

The reason we called it `itemRef` because if we change a value on the objet, it will be reflected in the array of items. So we can update the value of the item's `complete` property easily. 

```js
itemRef.complete = 
```

This function will be used to check the item on and off. 

You could have an if statement that says if it's true, set to false and if false, set to true. 

Or you can just set it to itself, but the opposite, as shown below 👇

```js
itemRef.complete = !itemRef.complete;
```

That should work because the opposite of true is false and vice versa. Thus, setting it to the bang version of itself should work. 

![](../attachments/854.png) 55:00

Now all you have to do is dispatch the `itemsUpdated` event because after updating the items. 

```js
itemRef.complete = !itemRef.complete;
list.dispatchEvent(new CustomEvent('itemsUpdated'));
```

You will notice that if you try to enter an item and the check it, it looks like nothing is happening. 

However if you go to the application tab, you will see that the local storage values are updating. 

![](../attachments/855.png) 55:38

What is going on? 

What is happening is the value is toggling true to false, but the checkbox is never working because we have not yet supplied the "checked" attribute to it when we rendered our HTML.

Modify the code as shown below to add the checked attribute 👇

```js
const html = items
  .map(
    (item) => `<li class="shopping-item">
  <input 
    type="checkbox" 
    value="${item.id}"
    checked="true"
  >
  <span class="itemName">${item.name}</span>
  <button 
    aria-label="Remove ${item.name}"
    value="${item.id}"
  >&times;</button>
</li>`
  )
  .join("");
```

Now all the items will be checked by default. 

One of the things about the checked attribute is if you do `checked="false"`, they will still maintain checked. Even just passing `checked` as shown below works. 

```js
<input 
  type="checkbox" 
  value="${item.id}"
  checked>
```

The absence of the checked attribute marks something as unchecked. 

If the checked attribute is true, you need to add the checked attribute, otherwise we will pass nothing. 

Do that by modifying the code as shown below 👇

```js
const html = items
  .map(
    (item) => `<li class="shopping-item">
  <input 
    type="checkbox" 
    value="${item.id}"
    ${item.complete ? 'checked' : ''}
    >
  <span class="itemName">${item.name}</span>
  <button 
    aria-label="Remove ${item.name}"
    value="${item.id}"
  >&times;</button>
</li>`
  )
  .join("");
```

We could have also used the `&&` operator instead like so 👇

```js
${item.complete && 'checked'}
```

Now if you refresh, the check marks should stay as they were.

That was a lot, but that is how all of those frameworks work. 

You basically have some state, you write a bunch of handlers to update state and to modify it, filter it, change it. When that state changes, you re-render out the HTML that is on the page. 

One last thing is that security, which we will go over in future lessons in more details.  Right now, if you wanted, you could submit an image as a list item input, which is a security issue. When you take input from a user and then display it in the HTML, we need to clean all the data the user types in. 

---

## 58 - Building a Gallery Exercise

In this exercise we will be building a gallery.

![](../attachments/856.png) 
00:11

We are going to be building it in a standard way, and then come back and refactor it for prototypes once we understand what those are. Then we are going to come back to this exercise a third time and refactor the gallery for classes.

Hopefully that gives you a good idea about why we need prototypes and what classes are. 

This is an interesting example already because we want the ability to use this javascript many times over. A lot of the javascript we have written so far assumes that things are on the page and that there is only ever one of them.  

![](../attachments/gallery.gif)

This gallery allows you to tab through the images when they are tiled and select an image and have it open up larger with an overlay. The image has arrows on each side, allowing the user to navigate back and forth by clicking them or using the arrow keys, you can press the escape key to close the overlay view. It is basically a full featured gallery. 

However, if we were to have another completely separate gallery below, we should be able to re-use the same code and have it function in the same way, while keeping both galleries separate. 

So in this video we will be building the gallery from the ground up, multiple times, with the ability to re-use it multiple times.

We will be working from the exercises directory, specifically `58 - Gallery`. Open up the `gallery.js` file to get started. 

### Closures

The first thing we need to do is create a closure. 

We learned a couple lessons back that a closure is the ability to create a function, and that functions have scope. 

```js
function Gallery(gallery){

}
```

For example, the function shown above will have scope. 

If inside of that function you were to make some variables, such as a variable to hold all the buttons, and also create another function called `showNextImage` which references those button variables, then you have created a closure. 

```js
function Gallery(gallery){
  const buttons = gallery.querySelectorAll('button');
  function showNextImage(){

  }
}
```
 
That means that the gallery function will run when we create it, and the function `showNextImage` will exist for things like click handlers. The variables (`buttons`)  that have been created in between the 2 functions (`Gallery` and `showNextImage`) will still be accessible even after the `Gallery` function has closed and stopped running.

We are going to use that concept to allow us to create scope for each of the galleries, so that they don't interfere with each other but they can reuse the same code. 

If you added any of the code, clear out everything within the `Gallery()` block. 

The idea with the Gallery is that at the end of writing the code, we have built almost like a plugin and we can go ahead and use it on the page. 

The idea is to be able to do something as shown below. 

```js
const gallery1 = Gallery();
```

Soon there will be a `new` keyword before we do ` = Gallery()` but for now we don't need that. 

If we go to the `index.html` that is on the Gallery exercises directory, you will see that we have a `div` with class of `gallery1`, and then a secondary gallery. 

![](../attachments/860.png) 4:02

Pass the gallery function reference to the gallery we want, which is the first one. 

```js
const gallery1 = Gallery(document.querySelector('.gallery1'));
const gallery2 = Gallery(document.querySelector('.gallery2'));
```

From the beginning we will be running these examples with 2 different galleries so that we know that every line of code that we are writing is safe for re-use over time. 

The first thing we want to do is log the gallery from within the `Gallery` function. When you refresh the page, you should see both `gallery1` and `gallery2` logged. 

![](../attachments/861.png) 4:35

One helpful thing we can do is if no gallery argument was provided, throw an error that says "No Gallery Found". 

By throwing an error like that, it will be logged to the console.

```js 
function Gallery(gallery){
  if(!gallery){
    throw new Error('No gallery Found!');
  }
}
```

![](../attachments/862.png) 4:58

If instead you want the function to gracefully degrade, you can simply return without throwing anything. That will break and exit the function without throwing any errors in the console. 

Keep the code you added above. 

Next you need to select the whole bunch of images. 

Previously, Wes has been selecting everything at the top of the file, however, since we need to select these things for each of our instances, we will be selecting the images from _within_ the `Gallery` function.

The first thing you need is a list of all of the images. Instead of using `document.querySelector` however, you need to make sure it's scoped to the gallery element that was passed in to the function. 

![](../attachments/863.png) 6:25

Use the `gallery` variable as our selector. For the list, use `Array.from()` because you will need to loop over it at some point. 

Add the following code 👇

```js
const images = Array.from(gallery.querySelectorAll('img'));
console.log(images);
```

![](../attachments/864.png) 6:47

If you add that code and look at the console, you will notice it is empty. 

Let's debug that. 

Start by logging `gallery` before we declare the `images` variable. 

![](../attachments/865.png) 6:54

As you can see, the gallery is showing up.

![](../attachments/866.png) 6:57

If we look inside of the gallery, we can see lots of image elements. 

![](../attachments/867.png) 7:06

The next thing you need is the modal, with the next and previous buttons. 

If you take a look at the HTML Wes has provided us with, he has scaffolded out the HTML for showing the modal. 

```html
<div class="modal">
  <div class="modalInner">
    <button aria-label="Previous Photo" class="prev">←</button>
    <figure>
      <img src="./images/kith-hoodie.jpg" />
      <figcaption>
        <h2>Test Title</h2>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolor
          dignissimos obcaecati nisi placeat eaque voluptate,
          exercitationem eius? Non, iusto provident itaque, voluptate
          labore a alias officia, amet sunt pariatur praesentium tenetur
          voluptatibus dolores mollitia quasi aliquid assumenda possimus
          maiores exercitationem!
        </p>
      </figcaption>
    </figure>
    <button class="next" aria-label="Next Photo">→</button>
  </div>
</div>
```

So we have a `figure` with an `img`, a `figcaption`, an `h2`, a paragraph. 

WHen someone clicks on an image in the gallery, that will open the modal and we will swap the text content of the modal out with the content associated with that image. 

Start by selecting the modal. Do that with the `document` selector because in this instance, the markup for the modal will be shared between the galleries because we can only ever have one modal open at a time. 

After that, look inside of the modal for the previous and next buttons. 

Add the following code to do so 👇

```js
const modal = document.querySelector('.modal');
const prevButton = modal.querySelector('.prev');
const nextButton = modal.querySelector('.next');
```

For the rest of this exercise, we will be chunking up the functionality into a bunch of little functions. 

Those functions will be responsible for showing the image, opening and closing the modal, listening for clicks... there is a lot going on! 

This is a great example of how you can take a javascript app and make it simpler by breaking it into smaller, little functions.

Let's start with the showing of the image. 

When someone clicks on one of the images, you need to update that modal with the associated images, as well as pop open the modal.

Name the function `showImage`. It will take a reference to an image element as a parameter which we will call `el`.

Within that function, check whether a reference to an image was passed. 

We are adding these checks because sometimes if for some reason something is broken when the function is run, having those safety checks will prevent the application from breaking on your page.

If a reference was not passed, log the message "no image to show" and return from the function. 

Otherwise, we will update the modal with that image's information but for now just log `el`. 

The function should look like below.

```js
function Gallery(gallery) {
  if (!gallery) {
    throw new Error("No Gallery Found!");
  }

  const images = Array.from(gallery.querySelectorAll("img"));
  const modal = document.querySelector(".modal");
  const prevButton = modal.querySelector(".prev");
  const nextButton = modal.querySelector(".next");
  function showImage(el) {
    if(!el){
      console.info("no image to show");
      return;
    }
    // update the modal with this info
    console.log(el);
  }
```

Next, take the images and loop over each of them to add an event listener on the click event. 

When the image is clicked, the callback function `handleImageClick` will be run, which takes in the event as an argument. 

```js
function handleImageClick(event){

}

images.forEach(image => image.addEventListener('click', handleImageClick));
```

Inside of `handleImageClick`, call `showImage` and pass it the image tag that was clicked by using `event.currentTarget`.

Now that you have added a bunch of different functions, let's check that it works and refactor it out to another arrow function. 

If you refresh the page, you should see that when you click an image, that image element is logged to the console. 

![](../attachments/868.png) 11:42

Refactor the code so instead of having a separate `handleImageClick` function, you can just do the same functionality with an arrow function. 

Remove the `handleImageClick` function and refactor the code as shown below.

```js
images.forEach(image => image.addEventListener('click', (e)=> showImage(e.currentTarget)));
```

If you run the code now, everything should work exactly the same.

Back to `showImage`, there are a few things that need to happen. 

When someone clicks the image, you need to update the source of the image element in the modal and the `h2` and `p` content.

![](../attachments/869.png) 12:37

Add the following code 👇

```js
console.log(el);
modal.querySelector('img').src = el.src;
```

Now if you refresh the page and click on an image, you should be able to go into the elements tab and look inside the modal to check the `img` src. It should be the source of the image that you clicked. 

Go ahead and duplicate the last line of code you added and switch the selector to be the `h2` instead. 

Instead of setting the `src`, update the `textContent` of the `h2` to be `el.title`. 

```js
modal.querySelector('h2').textContent = el.title;
```

Why do you need to do that? 

If you take a look at the image elements, you will see a couple of attributes on them. 

![](../attachments/871.png) 13:37

One of those is the `title`. Take the title from the image and then duplicate it again and grab the paragraph. 

The description is a data attribute on the image element, and you will need to use `dataset` to grab that value. 

```js
modal.querySelector('figure p').textContent = el.dataset.description;
```

Finally, you want to keep track of what the currently opened image is.  Underneath where you declare the next button, add the code below. 

```js
let currentImage;
```

At the very bottom of the `showImage` function, add `currentImage = el;`

If you refresh the page, then click on an image with the dev tools elements tab open, you should see the modal values being swapped out. 

![](../attachments/872.png) 14:55

_Note: the demo text is the same for each image, but you can tell it's being swapped because the first time you load the page, and then click, the value will be different._ 

Let's work on actually opening the modal now. 

Add a function `openModal`, and inside of it log "Opening Modal". 

At the bottom fo the `showImage` function, run `openModal()`.  

Within `openModal` function, we need to check if the modal is already open. _(We need to perform this check because Wes has added some animations that will animate it in and out.  We don't want to be triggering those animations if the modal is already open for some reason.)_ 

We can do that using `modal.matches('.open')`, which will take in the modal and check whether it matches the CSS selector we have passed it. In our example, we are checking whether the modal is open or not by the presence of the CSS class `open`. 

If it is open, log that it's already open and return from the function. 

If it's not already open, add a class of "open" to it, as shown below 👇

```js
modal.classList.add('open');
```

Your open modal function should look like the following 👇

```js
function openModal() {
  console.info("Opening Modal...");
  // First check if the modal is already open
  if (modal.matches(".open")) {
    console.info("Modal already open");
    return;
  }
  modal.classList.add("open");
}
```

If you refresh the page, when you click on an image, the modal should now open.

The previous and next buttons won't work in the modal, and neither will closing the modal by hitting escape on the keyboard or clicking outside of it. 
But it does slide down from the top when we click an image.

Why does that work? 

If you look at the `gallery.css`, you will see that by default, the modal has an opacity of 0 and pointer-event of none. 

![](../attachments/873.png) 17:29

However the modal with the class of `open` has opacity of 1 and pointer-event of all. 

![](../attachments/874.png) 17:22

The CSS style `opacity:0` will hide the element from the user, and setting `pointer-events:none` will ignore all the clicks on the element. 

![](../attachments/875.png) 17:57

There is also the `modalInner` which is currently off the page, via the CSS style `transform: translateY(-100vh);`. 

If we comment that CSS style out and also set `opacity:1` by default on the modal, you will see that the modal is actually open and visible on the page by default. -100 viewport will move it off the screen. 

When there is an open property on the parent, `.modalInner` gets a `translateY` of 0. 

![](../attachments/876.png) 18:23

Make a function `closeModal` which will remove the `open` class from the modal. Add a TODO comment to remind you to add event listeners for clicks and keyboard like the escape key later. 

```js
function closeModal(){
  modal.classList.remove('open');
  //TODO: add event listeners fro clicks and keyboard
}
```

If you click outside of the modal, you want to be able to run the `closeModal` function. 

How can you do that?

![](../attachments/877.png) 15:37

We only want the modal to close when someone clicks outside of `modalInner`. If you click within the modal, it should not close. 

Make a new function `handleClickOutside`, which takes in an event. 

Go down to where we have our event listeners and add a comment of `//These are our Event Listeners` and then add `modal.addEventListener('click',handleClickOutside);`. 

Inside of `handleClickOutside`, check whether the `event.target` is equal to the `event.currentTarget`. If it is, run `closeModal()`. 

```js
function handleClickOutside(e){
  if(e.target === e.currentTarget){
    closeModal();
  }
}
```

The code above checks whether the thing the user clicked matches the thing that you are listening for a click on. If they are the exact same thing, that means the user has clicked outside, and not within the modal. 

So if you clicked within the modal, that would return false but if you clicked outside of it, it would return true. 

![](../attachments/878.png) 21:01

Refresh the page and open the modal and click outside of it, to ensure it works. (It should.)

Next, let's wire up the escape key on our keyboard.  Make another function `handleKeyUp`, which takes in an event. 

Inside of the function, add an if statement that checks if the key that was pressed matches "Escape", and if it does, run `closeModal()`. 

This if statement is a good use case for a blockless if statement because it is a clean one liner. 

```js
function handleKeyUp(event){
  if(event.key === 'Escape') closeModal();
}
```

The `keyup` event will fire for any key that is pressed, so we will add more logic to only listen for the keys we care about in the future. 

Go down to our event listeners and add an event listener on the window. Listen for the `keyup` event and pass it the `handleKeyUp` function. 

```js
window.addEventListener('keyup', handleKeyUp);
```

If you refresh the page, you will see that when you open the modal, you can hit the escape key and that will work. Try the second gallery to make sure it's still working too.

Next we need to hook up the next and previous buttons and arrow keys to show the next and previous images.

Let's start with the button. Add the following event listener in the event listener section. 

```js
nextButton.addEventListener('click', showNextImage);
```

Notice that we have all these small little functions already? It doesn't necessarily matter in which order you put each function, but Wes likes to group them. 

Further up, above the `showImage` function, add the function `showNextImage`.

To be able to display the next image, we need to know which image is next. 

When an image is opened, set it to be equal to the variable `currentImage` we created earlier. 

Now when we run `showNextImage` we will have access to the current image by referencing the `currentImage` variable.

To grab the next image, you should able to use the `nextElementSibling()` method of the `currentImage` variable. 

Log the value of that within `showNextImage` for now. 

```js
function showNextImage(){
  console.log(currentImage.nextElementSibling); 
}
```

![](../attachments/879.png) 24:36

It gives Wes the suitcase which is correct but we get an error.

>gallery.js:37 Uncaught TypeError: Cannot read property 'nextElementSibling' of undefined
>    at HTMLButtonElement.showNextImage

Why is that happening?

That is a frequent problem that you will run into when you listen for clicks on things for multiple instances. 

In our case, what happened is we are listening for a click on the `nextButton`. We are listening for a keyup on the `window`. 

Because we have 2 galleries, there are 2 event listeners tacked onto the `window`, and onto the `nextButton`.

So what happened is it worked fine for the first instance and it errored out after the second one. 

To fix that, we will take those 2 event listeners and move them the end of the `openModal` function. 

```js
function openModal() {
  console.info("Opening Modal...");
  // First check if the modal is already open
  if (modal.matches(".open")) {
    console.info("Modal already open");
    return;
  }
  modal.classList.add("open");

  //Event listeners to be bound when we open the modal
  window.addEventListener("keyup", handleKeyUp);
  nextButton.addEventListener("click", showNextImage);
}
```

In the `closeModal` function we now need to do the exact opposite, which is to perform some cleanup when the modal closes. 

```js
window.removeEventListener("keyup", handleKeyUp);
nextButton.removeEventListener("click", showNextImage);
```

That makes sure that we are only ever listening for `keyup` and `click` on the things once, and then when the modal closes, we cleanup after ourselves and remove the event listeners. 

If you refresh the page and open the console and click the image and then hit next, you should see that works. If you go to the other gallery and try it, you should still see it works and isn't duplicating or anything. 

Now instead of logging it, we will instead pass it to our `showImage` function. 

```js
function showNextImage() {
  showImage(currentImage.nextElementSibling);
}
```

Now when you click one and then click the next one, it will automatically just change to the next one because we are passing the reference to the next image to our `showImage` function.

Now you probably see why we checked if there is no image passed in. When you hit the last image and click the next arrow, there is no next image, so it shouldn't work.

Let's actually write a function where if we are on the last image we show the first image.

Modify the code like so 👇

```js
function showNextImage(){
  showImage(currentImage.nextElementSibling || gallery.firstElementChild);
}
```

Now when you hit the last one, the first image will be shown. 

Onto the back button now.  Duplicate the function we just wrote and modify it as shown below. 

```js
function showPrevImage(){
  showImage(currentImage.prevElementSibling || gallery.lastElementChild);
}
```

In the open modal, duplicate the `nextButton` line of code and modify it like so 👇

```js
prevButton.addEventListener('click', showPrevImage);
```

If you refresh the page and try that, you will notice clicking next works but previous doesn't work. It's always wrapping around.

Go back to the `showPrevImage` function. We should have called `currentImage.previousElementSibling` not `prevElementSibling`. If you fix that it should now work.

The next step is to hookup the arrow keys. Let's piggyback on our `handleKeyUp` event handler. 

```js
if(event.key === 'Escape') closeModal();
if(event.key === 'ArrowRight' ) showNextImage();
if(event.key === 'ArrowLeft') showPrevImage();
```

Now if you try using the arrow keys, you will see it works beautifully.

One thing you could do is type `return` after each if statement. Although we aren't actually returning anything, the return makes the function stop running. If it was escaped, there is no point in checking if arrow right or arrow left were clicked 

```js
if(event.key === 'Escape') return closeModal();
if(event.key === 'ArrowRight' ) return showNextImage();
if(event.key === 'ArrowLeft') return showPrevImage();
```

The last thing we need to do is the enter key. 

Images by default are not keyboard focus-able, and in order to make the gallery accessible to keyboard users, we need to ensure that when they tab through it, they highlight and when you hit enter, it opens it up.

#### `tab-index`
If you look at the HTML page, you will see that all the images have a `tab-index` of 0. 

![](../attachments/880.png) 31:32

By giving it a `tab-index` of 0, you are telling the browser that this is an element that you can tab through, just like an input or links. Giving them all a tab-index of 0 will allow the tab to just naturally go in the flow of the document. 

If you added an input as a sibling of one of the images, you would see that we could tab from the input to the image with no problem. 

On some elements when you tab to them and hit enter, like a button, it will fire a click event but that is not the case for an image that has a tab index.

Let's listen for a keyup  or keydown event and check if the user had hit enter when its' focused.

G down to our event listeners and take all the images, and loop over them again.

Note: you could do it in the same loop but for sanities sake, let's keep them separate.

```js
//loop over each image
images.forEach((image) => {
  //attach an event listener for each image
  image.addEventListener("keyup", (e) => {
    //when that is keyup check if it was enter
    if (e.key === "Enter") {
      //if it was, sho that image.
      showImage(e.currentTarget);
    }
  });
});
```

Now when you tab through, you can hit enter and it will open the modal and you can press escape and it will close it.

There is a lot going on but we are at only 91 lines of javascript code for a full featured gallery, which is pretty cool.

We will be coming back to this video and refactoring it after we learn about **prototypes**. 

The one thing about having all these `closeModal` and `openModal` functions inside of the gallery function is that those functions are not actually shared between the two galleries, they are just duplicated. 

We basically have double functions that do the exact same thing. 

When we learn about prototypes in classes, we will learn about how to share the functionality between galleries as well as open up the functionality so we can call them manually ourselves. 

--- 

## 59 - Building a Slider

In this video, we will be building a slider.

![](../attachments/881.png) 00:16 

A slider may seem simple, but once you dive into it, it starts to get pretty complex. We will build the basics of the slider together and then you can feel free to add any functionality you want to it.

Similarly to the last lesson, we will be writing everything in the same Javascript file, and then later we will revisit this exercise and refactor it twice to use **prototypes** and **classes**.

We have 2 sliders on the page, so we can be sure that our code can be used more than once on the same page. 

If we look at the HTML structure of the slider within the element tab of the dev tools, you will see that we have all 20 slides. Now as we hit the next button and previous buttons, the classes are actually changing on the sliders depending on what button you press.

![](../attachments/882.png) 1:31

In this lesson we will use **SASS**, just to demonstrate that it is possible. Wes will show us how to get that up and running. 

We are starting with the CSS shown below. 

```css
.slide {
  position: absolute;
  background: var(--pink);
  height: 100%;
  width: 100%;
  display: grid;
  align-content: center;
  justify-content: center;
  color: white;
  font-size: 100px;
  font-family: sans-serif;
  border: 5px solid white;
  transition: all .25s;
  transform: translateX(-200%);
}
```

The `slide` class positions the slide absolutely, using `display: grid`. 
Then we take the slides and put them off the screen like so 👇

```css
.slide.prev {
  z-index: 10;
  transform: translateX(-100%);
}
.slide.current {
  z-index: 10;
  transform: translateX(0);
}
.slide.next {
  z-index: 10;
  transform: translateX(100%);
}
```

Our current slide has `translateX(0)`, which puts it in the middle. As we modify the value that we pass to `translateX`, you will see the slide is moving.

![](../attachments/883.png) 2:41

By translating something 100%, we are essentially just putting it outside the slides `div` and we have an `overflow:hidden` on it so you cannot see what is outside of it.

Have the previous, current and next slide on translateX -100, 0 and then 100% makes for that animation. Wes has added a transition on the animation to make it look smooth. 

Back to the SASS, in the SASS file we aren't actually using any special SASS syntax, so you could change the file extension to `.css` and it would work. However, Wes wanted to demonstrate that the Parcel bundler is able to recognize a SASS file if you add it via a stylesheet tag.

![](../attachments/884.png) 03:52

The Parcel bundler detects that the file is a `.scss` extension and it will compile it SASS for us before it puts it into the browser. 

Let's get started. Navigate in our terminal to the `exercises/59 - Slider` folder. Run `npm install` once you are in that directory. 

While that installs, open up the `package.json` file and take a look. 

![](../attachments/885.png) 4:40

You will notice that we have 2 dev dependencies, one for Sass and one for Parcel. When we type `npm start`, that will run the `parcel index.html` command. 

![](../attachments/886.png) 4:35

You should see the server is running on a specific port indicated in your terminal. Nothing should be happening on the page because haven't added any Javascript yet. 

Our javascript file lives in the `src` directory of our current exercise folder. Putting scripts in a `src` or `lib` folder is a pretty common thing to do. There is nothing special there, it's just a way to organize your files.

Let's start writing some code. Create a function called `Slider` which will take in an argument, `slider` which will be the reference to the slider element that was passed as an argument. 

_(Sometimes you will see people naming elements with an "El" at the end, just to specify that it is an element, but we won't do that.)_ 

Let's create 2 variables, one for each of the sliders we have on the page.

```js
function Slider(slider){

}
const mySlider = Slider(document.querySelector('.slider'));
const dogSlider = Slider(document.querySelector('.dog-slider'));
```

Within the slider function, add a check for whether someone has passed a slider in or not. 

```js
if(!slider){
  throw new Error('No slider passed in'); 
}
```

Now if you were to run the function and pass in anything instead of a reference to an element like `const mySlider2 = Slider(12322)`, it would not error out, because we are just checking whether we are getting anything. 

How can we check whether the function was passed in an actual HTML element? Like Wes has mentioned before, if we look at the docs for `document.querySelector()`,  you will see that it returns an element. 

The element is the most general base class from which all objects in a document inherit.  That may not be very interesting to you, but wh at that means is when we create a div or a span, it inherits all of it's base attributes from the Element in the browser. 

If you open up your dev tools and type `Element`, you will see that it is a function. 

![](../attachments/887.png) 8:25

This means that we can use `document instanceof Element` to check whether something is an instance of the Element base class.

![](../attachments/889.png) 9:30 

Modify the code as shown below 👇

```js
if(!(slider instanceof Element)){
  throw new Error('No slider passed in');
}
```
 
As we move through the slider, we will need to keep track of what is the current, next and previous slides. Create some empty variables that we will use to keep track of that.

```js
let current;
let prev;
let next;
```

We will set those values when the slider starts, and when the user navigates with the previous and next buttons. 

Next, we need to select the elements needed for a our slider. If you look at the HTML code, it consists of all the slides and then the next and previous buttons. 

```js
const slides = slider.querySelector('.slider');
const prevButton = document.querySelector('.goToPrev');
const nextButton = document.querySelector('.goToNext')
```

Just like we did in the last lesson, we will be adding a whole bunch of functions to add and remove CSS classes and figure out what is next.

Create a function called `startSlider`. Within that function we will be populating those variables. 

![](../attachments/890.png) 12:51

We want to update the `current` variable from within this function. The reason we are creating the variable outside of the function is that it needs to be accessible by other functions we will create in the future like move next functionality. 

If we created the variable inside of the `startSlider` function, that would make it scoped only to the function, and it would not be accessible elsewhere. By creating the variable at the top, all of the functions that live inside of our slider will have access to it.  

That is the concept of what a **closure** is. We have these variables that existing within our `Slider` function that other functions will be able to grab onto. They are not global variables, they are variables that live inside the closure of the `slider` function.

We will set the `current` variable to be either the first slide that is in the slider, or where the slider has the class of `current` (so you could set the slider to start at a specific image on page load). 

In one of the sliders on our HTML page, Wes has set the starting slide by passing a class of current to one of the slides and in the second slide there is no current class on load.

We will set the value of current to be the slide that contains the class of "current" or if no slider has a class of current, we will get the first element child of `slides`. 

```js
function startSlider(){
  current = slider.querySelector('.current') || slides.firstElementChild;
  console.log(current);
}
```

![](../attachments/891.png) 14:45

When we create the slider, we now have to run the `startSlider` function.  Add it to the bottom of the `Slider` function. 

```js
//when this slider is created, run the start slider function
startSlider();
```

That is often what we refer to as a **constructor**, which we will be getting into more when we hit classes.

If you refresh the page you will see that we now have both of our slides logged in the console. The first slide starts at 16 because it has the class current on it and the slider had no class of current on any of the slides so it started on the first slide.

![](../attachments/893.png) 18:30

For the previous one we will grab the element that is behind the current one using `previousElementSibling`. 

Let's demo how that works by going to the HTML page in the browser, selecting slide #2 in the elements tab and then going back to the console and typing `$0.previousElementSibling`. You will see that the slide that says 1 will be returned. 

![](../attachments/894.png) 18:57

If you were to do the same thing but with #1 slide, you would get `null` because because there is nothing next to one. 

![](../attachments/896.png) 19:13

So we want to set the previous slide to be the `previousElementSibling`, or if that doesn't exist, we can fall back to the last slide within our slides div.

```js
prev = current.previousElementSibling || slides.lastElementChild;
```

Why is Wes using the Element version of the methods instead of using `current.previousSibling` or `slides.lastChild`? What is the difference between `lastElementChild` and `lastChild`?

Let's demonstrate with an example. 

Add a paragraph at the top of the HTML page such as `<p>I <strong>love</strong> to eat <strong>pizza</strong></p>` and inspect it.

![](../attachments/897.png) 20:07

Click on "love", and then go into the console and try the following 👇

```js
$0
$0.nextSibling;
$0.nextElementSibling;
```

![](../attachments/898.png) 20:24

What is the difference? `nextSibling` gives us a Node, and a node can be text or an element, whereas `nextElementSibling` will only return elements. Always use `elementSibling` when you are looking for an element. 

Next will be `next = current.nextElementSibling || slides.firstElementChild;`.  Then we will add `console.log({current, prev, next });`

```js
function startSlider() {
  current = slider.querySelector(".current") || slides.firstElementChild;
  prev = current.previousElementSibling || slides.lastElementChild;
  next = current.nextElementSibling || slides.firstElementChild;
  console.log({ current, prev, next });
}
```

![](../attachments/899.png) 21:27

If you open the console, you will see we have `current, prev, next`. 

Now we need to start applying classes to those to make them show up. 

Make a function `applyClasses` and we will take the current, add the class of current to it and then do the same the prev and next.   

```js
function applyClasses(){
  current.classList.add('current');
  prev.classList.add('prev');
  next.classList.add('next');
}
```

Now when the code runs, we will just run `applyClasses` as well. 

```js
startSlider();
applyClasses();
```

If you were to inspect the code you would see that now the appropriate slides have classes.

![](../attachments/900.png) 22:35

Next we need a method called `move` that takes in a direction like back or forwards.

```js
function move(direction){

}
```

When we call the `move` function it will move the classes around to switch which the current, next and previous slides are. You could manually edit the classes yourself in the element panel to do that.

The first thing this function will do is strip all the current classes off the slides. 

Make an array of classes to remove and put the classes that we want to remove inside of the array. Then take the previous element and call `remove()`.  Remove will take in as many arguments of classes that you want to remove as you want. 

We will have to do that with current and next as well which is kind of annoying. 

```js
prev.classList.remove("prev", "current", "next");
current.classList.remove("prev", "current", "next");
next.classList.remove("prev", "current", "next");
```

What is even better is we can take the array of classes to remove and spread it into the remove method, like so 👇 

```js
function move(direction){
  //first strip all classes off the current slides
  const classesToRemove = ['prev', 'current', 'next'];
  prev.classList.remove(...classesToRemove);
  current.classList.remove(...classesToRemove);
  next.classList.remove(...classesToRemove);
}
```

We could even make that shorter by putting our elements into an array and then calling `forEach` on them and then within the `forEach` calling `remove` and spreading the `classesToRemove` array into it. 

```js
[prev, current, next].forEach(el => el.classList.remove(...classesToRemove));
```

Let's go with the approach where we have three lines instead of the one liner to make it more readable instead however.

Now we need to figure out which direction the slides are going. 

If the slides are going backwards, the need to take our `current`, `previous` and `next` variables and shift them by one. If we are going backwards previous will become current, current will become next. We are basically shifting everything to the left.

There is a bit of a problem when you are assigning variabels to be each other. Let's say we tried the code below 👇

```js
if(direction === 'back'){
  prev = prev.previousElementSibling;
  current = prev;
}
```

We have run into this problem where we have already updated what previous is. How do we access the old previous? We could do have a variable called `oldPrev` and then assign the value of prev to that before we reassign it but that is not the best way. 

What Wes will show us instead is how to use **destructuring** to switch variables easily.

We will destructure the `[prev, current, next]` variables and make an array of their new values and destructure them over and into the prev, current and next variables. 

That means the first thing we put into the array will be assigned to `prev`. Then next item will be `current` and the last will be `next`. 

The first thing will be `prev.previousElementSibling`. Then the current will be the `prev` and the `next` will become the current. 

```js
[prev, current, next] = [prev.previousElementSibling, prev, current];
```

Now we will do the opposite if the direction is forward.

```js
if (direction === "back") {
  [prev, current, next] = [prev.previousElementSibling, prev, current];
} else {
  [prev, current, next] = [current, next, next.nextElementSibling];
}
```

That seems confusing but all we are doing is shifting them all one lower. 

Next we will just run the `applyClasses()` function which will in turn add the current, previous and next classes.

Now we can take our previous button and our next button and hook up click events.

Let's do it at the very bottom of our `Slider` function. 

Call the  move   function from the event listener handlers and pass `'back'` to when the previous button is clicked using an arrow function. When the next button is clicked, we will just pass reference to `move` since unless you pass the string "back", it will move in the forward direction.

```js
//Event Listeners

prevButton.addEventListener('click', ()=> move('back'));
nextButton.addEventListeners('click', move);
```

If you need to pass an argument to a function, you need to use an arrow function here. Or, you use **call and apply** which you will learn about in the next video. 

Now when you click it, you will see the slider works. 

One error is when you get to the very end or very beginning, we will get an arrow because we lose our `next` class.

![](../attachments/901.png) 31:08

Now we need to say when we have the edge case where a previous element or next sibling doesn't exist you will add an or condition and get the `slides.lastElementChild` or `slides.firstElementChild` for the next button. 

```js
if (direction === "back") {
  [prev, current, next] = [
    // get the prev slide, if there is none, get the last slide from the entire slider for wrapping
    prev.previousElementSibling || slides.lastElementChild,
    prev,
    current,
  ];
} else {
  [prev, current, next] = [
    current,
    next,
    //get the next slide or if its at the end, loop around and grab the first
    next.nextElementSibling || slides.firstElementChild,
  ];
}
```

Now if you refresh the page you will see the slider is working but the second one is not. Why not? Let's debug. 

The reason is that the buttons are not working for the second slider. 

Why is that? 
Because if you look back at where we grab the buttons in our code, we are using `document.querySelector()` instead of `querySelectorAll()` to grab the buttons, which means both sliders are being moved by the same button. `querySelector` just finds the first element on the page and binds to that. It shouldn't be `document`, it should be `slider` because we need to look for the buttons within the slider itself.

If you refresh the page you will see they now run on their own.

![](../attachments/902.png) 33:35

63 lines of code for a slider! 

It would be cool to get the arrow keys working but only when someone is focused in on one of the dev. That would be an interesting exercise to give a shot yourself if you're interested. 

We will be revisiting this exercise in our prototype lesson. The functions, `move`, `applyClasses` and `startSlider` are going to be moving to what are called **the prototype**.

