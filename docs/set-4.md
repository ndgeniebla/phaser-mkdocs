# Creating Our First Scene, Game Object and Player Characters

## Prerequisites
placeholder

## Overview
placeholder or something i'll do this later

## Preloading Assets

Now that we have our first game instance, it's time to add some game assets to give our player something to look at

!!! Info "Information"

    Assets have many definitions in the real world. In the context of game developement, assets mean any digital content used by the video game to communicate information to the user about the state of the game. This can include audio, visual elements and animations.

1. Inside the preload function defined inside of `src/game.js` add two function calls to `this` game instances `load.image()` method with the following name parameter and path path paramater
```
function preload() {
    this.load.image('ball', '../assets/images/ball.png') // name, path
    this.load.image('paddle', '../assets/images/paddle.png') // name, path
    }

```

!!! Info "Information" 
    
    this function tells the game instance to load the images we want to use in the game itself. If you had other assets you wanted to load in such as music or animations, you would define them here as well using their respective `load` methods. 