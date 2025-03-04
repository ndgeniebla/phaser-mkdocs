# Creating and Configuring Our Game Instance

## Prerequisites

## Overview

## Configuring the Game Instance
1. Navigate to the **src** folder and open the empty game.js file.
2. At the start of the file, create an empty `config` object:
```JS title="game.js" linenums="1"
const config = {

}
```
3. Add inside of the `config` object the `type` attribute with a value of `Phaser.AUTO`:
```JS title="game.js" linenums="1" hl_lines="2"
const config = {
    type: Phaser.AUTO,
}
```
The `type` attribute tells Phaser to use either [WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API) or [Canvas](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) to render its graphics. Setting it to `Phaser.AUTO` tells Phaser to use WebGL by default.


4. Add the `parent` attribute to the `config` object with a value of `'game'`:
```JS title="game.js" linenums="1" hl_lines="3"
const config = {
    type: Phaser.AUTO,
    parent: 'game',
}
```

    !!! Warning "Warning"

        Remember to add commas at the end of each key-value pair inside of a JavaScript object!
    
    The `parent` attribute tells Phaser the HTML ID of the HTML element that the game will be injected into. We will set that up in the next step.

5. Navigate to the root of the directory and open **index.html** in VSCode.

6. Inside of the body tag in the HTML, create a `div` with an ID of `game`, to match the value given to the `parent` attribute in the `config` object:
```HTML title="index.html" linenums="26" hl_lines="3"
<body>
  <noscript>You need to enable JavaScript to run this app.</noscript>
  <div id="game"></div>
  <script src="./lib/phaser.min.js"></script>
  <script src="./src/game.js"></script>
</body>
```
Now that Phaser knows where to inject the game in the HTML file, we can go back to configuring our Phaser game.

7. Return to editing the **game.js** file in VSCode.
8. Add the `width` and `height` attributes to the `config` object, with `width` having a value of `800` and the `height` having a value of `640`.
```JS title="game.js" linenums="1" hl_lines="4-5"
const config = {
    type: Phaser.AUTO,
    parent: 'game',
    width: 800,
    height: 640,
}
```
The `width` and `height` attributes define the resolution of the Phaser game when rendered in the browser.

9. Insert the following `scale` object inside of `config`, with the `mode` and `autoCenter` attributes and their values:
```JS title="game.js" linenums="1" hl_lines="4-5"
const config = {
    type: Phaser.AUTO,
    parent: 'game',
    width: 800,
    height: 640,
    
    scale: {
        mode: Phaser.Scale.RESIZE,
        autoCenter: Phaser.Scale.CENTER_BOTH
    }
}
```
The `scale` object with its attributes basically tells Phaser to:

    1. Resize the game screen to fit the space of its parent HTML element, regardless of aspect ratio.
    2. Render the game screen in the center of the window.

    !!! Danger "Phaser Attributes are Case Sensitive"

        Any attribute that is part of the `Phaser` object is *case-sensitive*. In this case, this means that the "scale" in `Phaser.Scale` has to start with an uppercase letter. Getting the scale attribute with `Phaser.scale` (scale with a lowercase 's') will *not* work.





