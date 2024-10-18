# Simple Audio

## Introduction

In this task we will learn to use audio in JavaScript. We will create a simple audio player from which we can play one song with pause and seek functionalities. We will use the audio file `Soft-Background-for-Interview.webm` located in the `audio`.


## Knowledge / Learning
In this task you will use:
- css styling that we have already seen in class
- javascript events to detect when a button is clicked and trigger specific actions
- the javascript [`Audio` object](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement/Audio) to control audio

# Audio Task Guide

## Step One: Create the Structure

Let's begin by adding an html file:

- Create a file named `simple-player.html`.
- Use the shortcut `html:5` to generate the html skeleton.
- Change the title to `Simple Player`

Your initial `html` should look similar to this:

<details>
<summary>Solution</summary>

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Player</title>
</head>
<body>
    
</body>
</html>
```
</details>


Let's now create a css style file:
- Add a new folder named `css`
- Create a new file inside the folder `css` named `simple-player.css`

With these new files created, we are now ready to link the `js` and `css` files to our `html`.

- Add a `link` tag in your html `head` for your `css`:

<details>
<summary>Solution</summary>
You can do so by adding the line below to your html head:

```html
<link rel="stylesheet" href="css/simple-player.css">
```
</details>


- Add a `script` tag in your html `head` for your `javascript`:
<details>
<summary>Solution</summary>
You can do so by adding the line below to your html head:

```html
<script src="js/simple-player.js" defer></script>
```
</details>

## Step Two: Adding Play Button

Let's now move on to creating the body for our `html`:
- Create a `div` with **id** `"container"` - This div element will contain the rest of the body.
- Inside the `div` add an `img` with **id** `"play-pause-button"` and **src** `"images/play.svg"`

<details>
<summary>Solution</summary>

Your html body should now look like this:

```html
<body>
    <div id="container">
        <img id="play-pause-button" src="images/play.svg">
    </div> 
</body>
```
</details>

What happens if you now look at the live page? What's the next thing that we have to fix?

<details>
<summary>Answer</summary>

The play button is gigantic! We need to fix the css. Let's do this on the next step!
</details>

## Step Three: Initial Styling

Let's add some styling and, in the meantime, fix this gigantic image issue:

- Open the `simple-player.css` file
- Create a css selector for the container div through its id
- Give it a `width` of `330px`, a `height` of `50px`, a `background-color` of value `bisque` and a `border-radius` of `10px`
    
    This will createn display the div in an audio bar style.

<details><summary>Solution</summary>

You can add these properties with the following `css`:

```css
#container {
    /* Audio player bar style */
    width: 330px;
    height: 50px;
    background-color: bisque;
    border-radius: 10px;
  }
```

</details>

Let's now fix the play image width:

- Create a css selector for the play image through its id

- Give it a `width` of `20px`, a `height` of `20px`, a `padding-left` of `10px` and a `padding-right` of `10px`
    
    This will make the image smaller and add some padding between the image and the containing div

- Set the `cursor` property to `pointer`. - This will change the cursor when it hovers on to the play button to signify it can be clicked.

<details><summary>Solution</summary>

You can add these properties with the following `css`:

```css
#play-pause-button {
  /* Fix width and height */
  width: 20px;
  height: 20px;

  /* Add padding to give space to left and right */
  padding-left: 10px;
  padding-right: 10px;

  /* Change cursor to pointer style when hovering over image */
  cursor: pointer;
}
```

</details>

If you now look at the website, the play button is aligned to the top, but in an audio player bar usually we want buttons centred.

This is fixable by smartly using the `flex` display property in `css`. On top of giving this property, we wnat to set it in `row` direction, rather than `column`, since any object that we continue adding to the bar should be displayed horizontally. To add this:

- In the `#container` css selector:

    Set the `display` property to `flex` - to give the `div` flex properties

    Set the `flex-direction` property to `row` - to make sure any other elements (such as the seek bar or timer) we add are added horizontally

    Set the `align-items` property to `center` - to make the `play` button vertically align in the middle

<details><summary>Solution</summary>

Your `#container` selector should now look like this

```css
#container {
    /* Audio player bar style */
    width: 330px;
    height: 50px;
    background-color: bisque;
    border-radius: 10px;

    /* Flex display properties */
    display: flex;
    align-items: center;
    flex-direction: row;
}
```

</details>

## Step Four: Play audio from javascript

Let's now introduce the `Audio` object. The  [Mozilla Developer documents](https://developer.mozilla.org/en-US/docs/Web/API/HTMLAudioElement/Audio) tell us that to create an Audio object we can use either of these lines:

```js
new Audio()
new Audio(url)
```

Where `url` is an optional `string` parameter that points to the source of the audio. Because we know which source we are going to use (located in `audio/Soft-Background-for-Interview.webm`), we will use the second option.

To begin:
- Open your `simple-player.js` file
- At the top of this file, create a new constant variable named `audio` and assign it to a new audio object with url `"audio/Soft-Background-for-Interview.webm"`

<details><summary>Solution</summary>
You can do this with the following line:

```js
// audio object that stores the audio file
const audio = new Audio("audio/Soft-Background-for-Interview.webm");
```
</details>

Now, let's create a variable that will represent the play / pause image

- Create a new constant variable named `button` that references the play image
    
    You will have to select the image using it's `id` and the `getElementById` function of the `document` object

<details><summary>Solution</summary>
You can do this with the following line:

```js
// button object that references the image with id "play-pause-button"
const button = document.getElementById("play-pause-button");
```
</details>

Let's now add this button some functionality. If we read through the [W3 School `onclick` documentation](https://www.w3schools.com/jsref/event_onclick.asp), it says that we can use the following syntax to define this event from our javascript:

```js
object.onclick = function(){myScript};
```
Where `myScript` would be the content of the function.

Let's add some functionality to our button:
- Assign the `onclick` event to a function that logs the string `"The play button has been clicked"`

<details><summary>Solution</summary>

You can do so with the following code:

```js
button.onclick = function() {
    console.log("The play button has been clicked");
}
```

As you can see:
- Because we have previously assigned the name variable `button` and not `object` to our variable, we need to change that in our implementation
- Instead of `myScript`, we have added this logging line to perform the action

_
</details>

Now that this is done, head on to your live site. If you open the `Inspect Toolbar` and select the `Console` view, you should see this line logged every time you clicked the button. 

Now that we have successfully linked the javascript button with the html button, we can add the audio player functionality. To do so, we will use the function `audio.play()` that comes with the Audio object:

- Replace the logging line in the `onclick` event function with the line:

    ```js
    audio.play();
    ```

<details><summary>Solution</summary>

Your `onclick` event function should now look like this

```js
// When the play button is clicked, play audio
button.onclick = function() {
    audio.play();
}
```
</details>

## Step Five: Play / Pause functionality

### Play and Pause from the click of the button

Currently, this audio is playing when the button is clicked. But what we want to do is:

- When the `play` button is clicked:
    
    If the audio is not currently playing:

        Start playing audio
    If the audio is currently playing:

        Pause audio

As you can see, we will need to use a **conditional** statement, and figure out whether the audio is playing or not. The audio object has a property that can be accessed with the line `audio.paused` which returns a `boolean` that is `true` if the audio is currently paused (i.e. not playing) and `false` if the uadio is currently not pused (i.e. playing).

Knowing this, insde the `onclick` event function:
- Add an `if` statement to check if the audio is currently paused using the `audio.paused` property
- If the audio is currently paused, invoke the `audio.play()` functiont o start playing the audio
- Otherwise, invoke the `audio.pause()` function to pause the audio

You will have to use the structure:
```javascript
if(certain condition is met) {
    /* Do some actions */
}
else {
    /* Do some other actions */
}
```

<details><summary>Solution</summary>

Your `onclick` event function should now look like this:

```js
// When the play button is clicked, play or pause audio according to state
button.onclick = function() {
    if(audio.paused) { 
        audio.play();
    }
    else {
        audio.pause();
    }
}
```
</details>

Head over to your life site and check that it's working! You should now be able to play and pause the audio!

### Displaying correct image according to audio state

Before moving on to the next step, we still want to add a second functionality related to playing and pausing. We want the button to display the original `play.svg` image when the audio is paused, but it should display the `pause.svg` image when the audio is playing, so that the user knows what action they can do by clicking that button.

To do so, we will use a new type of event that the `Audio` object provides. These are the `audio.onplay` and `audio.onpause`. These events are triggered every time the audio plays or pauses, which means we can use them to change the image source of the button when that happens.

Add the following code to your javascript:
- Assign the `onplay` event to a function that logs the string `"The audio is playing"`
- Assign the `onpause` event to a function that logs the string `"The audio is paused"`

<details><summary>Solution</summary>
You can do so by adding the following code:

```js
audio.onplay = function() {
    console.log("The audio is playing");
}

audio.onpause = function() {
    console.log("The audio is paused");
}
```
</details>

If you now head to your live site and open the console, you should see these logs happening as you play and pause the audio. Let's now modify the code so that instead of logging the source of the button object is changed, thus changing the image:

#### In your `audio.onplay` event:
- Replace the log line with the following line, to modify the `button` image source:
    
    `button.src = "images/pause.svg"`

#### In your `audio.pause` event:
- Replace the log line with the following line, to modify the `button` image source:
    
    `button.src = "images/play.svg"`

<details><summary>Solution</summary>

The audio events code should now look like this:

```js

// Every time audio plays, replace button image to pause.svg
audio.onplay = function() {
    button.src = "images/pause.svg";
}

// Every time audio pauses, replace button image to play.svg
audio.onpause = function() {
    button.src = "images/play.svg";
}
```
</details>

## Step Six: The seek bar

Let's now add a bar that will tell the user where the audio is at. This bar will also be used to change the audio current position.

### The Html

In the `html` add the following elements at the end of the `container div`:

- An `h4` with id `current-time` and text `0:00`. This `h4` will display the time at which the audio is currently at:

```html
<h4 id="current-time">0:00</h4>
```
- An `h4` which contains a forward slash:

```html
<h4>/</h4>
```

- An `h4` with id `total-time` and text `0:00`. This `h4` will display the total time of the song.
```html
<h4 id="total-time">0:00</h4>
```

- An `input` element of `type` `range` like so:

```html
<input id="seek-bar" type="range" min="0" value="0"/>
```

As you can see we are giving an id of `seek-bar` to this element, a minimum value of `0` so that it's not allowed to have a negative value, and an initial value of `0` so that the audio begins at time `00:00`.

Theese elements will be in charge of guiding the user through time control and information. If you head to the live site you should now be able to see a "timer" which displays `00:00 / 00:00` and a seekbar that you can move around, even though it has no effect on the audio playing.


### The css

Let's styile this new elements. In your `css`, apply the following styling:

- To style the `h4` elements displaying the playing time:

```css
/* style for all h4 elements */
h4 {
  /* Set font family, weight and size */
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-weight: 100;
  font-size: 20px;
  /* add padding to the bottom so they are not crammed */
  padding-bottom: 4px;
  /* Remove user-select to aviod mouse changing to signify text is not selectebeale and prevent vertical bar to appear on scroll */
  user-select: none;
}

```

- to style the specific `current-time` and `total-time` elements:

```css
/* current-time element */
#current-time {
  /* give width to space letters out */
  width: 40px;
  /* give paddin to space add space from other elements */
  padding-left: 5px;
}

/* total-time element */
#total-time {
  width: 40px;
  padding-left: 10px;
}
```

### The javascript

Having added and styled these objects, we're now ready to add some functionality to them through the javascript file. In your `simple-player`, add the following:

- At the top of the file, create a new `constant` variable named `trackTime` and assign it to the HTML Element with id `current-time`.

- Add another `constant` variable named `totalTime` and assign it to the HTML Element with id `total-time`.

- Add another `constant` variable named `seekBar` and assign it to the HTML Element with id `seek-bar`.

<details><summary>Solution</summary>

```javascript
// objects to reference seek bar and timing elements
const trackTime = document.getElementById("current-time");
const totalTime = document.getElementById("total-time");
const seekBar = document.getElementById("seek-bar");
```
</details>

We will first add the functionalities to display the total time and track time as we play. To do this, we need:

- The `audio.duration` property, which tells us the total duration of the audio fi.e
- The `audio.onloadedmetadata` event, which is triggered when the website has extracted all relevant information from the audio file (such as length, title etc.)

Let's use them in the code. After the event listeners that we have already set up:
- Add an `onloadedmetadata` - triggered when the audio's information is ready - event listener which will:
    - Set the `trackTime.innerHTML` to `formatTime(0)`, so that it goes back to the beginning as soon as the audio information is loaded.
    - Set the `totalTime.innerHTML` to `formatTime(audio.duration)`, so that it displays the total  time of the track (instead of `00:00` as we initially set).
    - Set the `seekBar.max` to `Math.floor(audio.duration)`, which is the maximum duration in seconds rounded down. (So, for example, if the audio lasts `234.82` seconds, this would return `234`).

<details><summary>Solution</summary>

You should have added these lines to your `javascript` file:

```javascript
// As soon as we have the audio duration loaded, set the totalTime and seekBar
audio.onloadedmetadata = function () {
    // Make sure trackTime is set to zero
    trackTime.innerHTML = formatTime(0);
    // Set totalTime to display the exact audio duration properly formatted
    totalTime.innerHTML = formatTime(audio.duration);
    // Set the seekBar max to the rounded down audio duration - as seekbar values do not understand decimals
    seekBar.max = Math.floor(audio.duration);
    // Make sure seekBar value is set to zero
    seekBar.value = 0;
};
```
</details>

Before continuing, head to your live site to make sure this information is displayed correctly. You should see the timer display the values: `00:00 / 1:52`. **(Bear in mind the second number might change if you are not using the example audio).**

We will now add the functionalities to update the `seekBar` as the audio advances. To do this, we need:

- The `audio.currentTime` property, which tells us the time at which the audio currently is along the track. 
- The `audio.ontimeupdate`, which is triggered every time the audio's `currentTime` changes, i.e., it is continuosly triggered as the track plays along.

In your javascript file:

- Add a listener function for the `ontimeupdate` listener which:
    - Sets the `trackTime.innerHTML` to `formatAudio(audio.currentTime)`
    - Sets the `seekBar.value` to `Math.floor(audio.currentTime)`

<details><summary>Solution</summary>

You should have added the following code: 

```javascript
// Every time the audio time updates, change the trackTime and seekBar to display currentTime
audio.ontimeupdate = function (){
    trackTime.innerHTML = formatTime(audio.currentTime);
    seekBar.value = Math.floor(audio.currentTime);
};
```
</details>

If you now look at your HTML, the seek bar and time display should follow along the audio as it plays. However, when we move the seek bar around the audio is not (yet) updated.

Let's now add functionality to make the seek bar control the time as well. 


For this, we will use the following listeners from the `seekbar` javascript object:
- `seekBar.oninput`, which is triggered every time the user starts dragging the seek bar knob.
- `seekBar.onchange`, which is triggered every time the value of the seekbar changes - i.e., when the user releases the seek bar knob.

Let's begin:
- At the top of your file, after all the `const` variables are defined, create a new variable of type `let` called `seeking`. This variable will store a `boolean` value (i.e. `true` or `false`), which denotes whether the user is moving the seek bar around or not. Initiate the value of `seeking` as `false`.
- After your event listeners, a new `seekBar.oninput` event listener which:
    - Sets the value of `seeking` to `true`
- Add another event listener for `seekBar.onchange` which:
    - Sets `audio.currentTime` to `seekBar.value`
    - With a conditional, if the audio is not paused, calls `audio.play()`. This is to make sure that the audio doesn't accidentally stop after dragging the seek bar knob.
    - Sets `seeking` to `false`
- For this to work, we also need to add a conditional check inside the `ontimeupdate` so that the script only changes the `seekBar` when `seeking` is set to `false`. This is necessary as otherwise the `seekBar` would keep changing value when **both** the user is dragging it and the audio is playing!

<details><summary>Solution</summary>

You should have added the following line after the `const` variables are defined:

```javascript
// Store whether the user is currently dragging the seek bar
let seeking = false;
```

You should have added the following events:

```javascript
// On seekBar input (i.e. when user clicks on the seek bar knob), set seeking to true
seekBar.oninput = function () {
  seeking = true;
};

// On seekBar change (i.e., when the user releases the knob to set a new point in the track), update audio player and set seeking to false
seekBar.onchange = function () {
  
  // Update the audio current time to match the seekBar value that the user has set
  audio.currentTime = seekBar.value;
  
  // If the audio is not currently playing, play it
  if (!audio.paused) {
    audio.play();
  }

  // Set seeking to false
  seeking = false;
};
```

Finally, you should have modified the `audio.ontimeupdate` event listener like so:

```javascript
// Every time the audio time updates, change the trackTime and seekBar to display currentTime
audio.ontimeupdate = function (){
  trackTime.innerHTML = formatTime(audio.currentTime);

  // Only update seekbar when user is not dragging seek bar knob
  if (!seeking) {
      seekBar.value = Math.floor(audio.currentTime);
  }
};
```

</details>

With these new changes, your audio should now be allowing the user to change the audio's time live! - Bear in mind the example audio is very similar along the way. To make sure it's changing, let it play for a bit, then drag bar to the beginning and see if it restarts.

There is one last thing to do for the seek bar. We need to reset all values when the audio has ended playing. We can do this with the `audio.onend` event, which detects when the audio has ended playing. Luckily, the `Audio` object that javascript provides is very intelligent, and will set the `paused` property of the audio to true for us, restart it's time etc. But we still need to make sure the button, track time and seek bar are displayed correctly:

- Add an `audio.onend` event listener which:
  - Sets the `button.src` to `"images/play.svg"`, to allow user to start playing audio again
  - Set `trackTime.innerHTML` to `formatTime(0)` to restart it
  - Set `seekBar.value` to `0` to restart it

```javascript
// Detect when audio finishes playing and restart all necessary values
audio.onended = function () {
    button.src = "images/play.svg";
    trackTime.innerHTML = formatTime(0);
    seekBar.value = 0;
}
```

## The last touches

There are some last changes to make, which are not integral, but ma make the audio player not work properly in very specific environments.

### Making sure the audio loads before we allow the user to play it thorugh

To do this, modify the `HTML` to disable both the  play / pause button and seek bar so that they are `disabled` at the beginning. You can do so by modifying the `img` line like so:

```html
<button id="play-pause-container" disabled><img id="play-pause-button" src="images/play.svg"></button>
```

and add following `css` to style this as invisible:

```css
/*  play-pause-container button style*/
#play-pause-container {
	color: inherit;
	border: none;
	padding: 0;
	font: inherit;
	cursor: pointer;
	outline: inherit;

  /* Give a border radius and height */
  border-radius: round;
  height: 50px;

  /* set grey background at beginning */
	background: grey;
  opacity: 50%;
}
```

Modify the `input` element to describe the `seek-bar` line like so:

```html
<input id="seek-bar" type="range" min="0" value="0" disabled/>
```

Add following listener to your javascript, which will detect when the audio has fully loaded and therefore can be played, to reenable these two elements when that happens:

```javascript
//... AT TOP OF FILE ... //

//select play / pause button container element
const buttonContainer = document.getElementById("play-pause-container");

// ... REST OF CODE ... //

// Enable button and seekbar when audio is ready to play
audio.oncanplaythrough = function() {
  buttonContainer.disabled = false;
  seekBar.disabled = false;
  
  //Remove grey background from button container so user knows they can use it
  buttonContainer.style.background = 'none';
  buttonContainer.style.opacity = 1;
}
```



## Adding another audio file

