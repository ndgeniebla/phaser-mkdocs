# Creating Our First Game Objects and Player Characters

## Prerequisites
1. We have configured our game instance of phaser

## Overview
In this section, we will cover how to preload assets, create game objects, assign them sprites and 
set their locations, and get them moving.

## Preloading Assets

Now that we have our first game instance, it's time to add some game assets to give our player something to look at

!!! Info "Information"

    Assets have many definitions in the real world. In the context of game developement, assets mean any digital content used by the video game to communicate information to the user about the state of the game. This can include audio, visual elements and animations.

1. Inside the `preload` function defined inside of `src/game.js` add two function calls to `this` game instances `load.image()` method with the following name parameter and path path paramater.

```JS title="game.js" linenums="1"
function preload() {
    this.load.image('ball', '../assets/images/ball.png') // name, path
    this.load.image('paddle', '../assets/images/paddle.png') // name, path
    }

```

!!! Info "Information" 
    
    this function tells the game instance to load the images we want to use in the game itself. If you had other assets you wanted to load in such as music or animations, you would define them here as well using their respective `load` methods. 

2. Outside the create function define our ball

```JS title="game.js" linenums="1"

let ball;

function create() {
};


```

3. inside the create function, we are going to `add` our first game object: the ball. We will add a sprite (our preloaded image asset) to the ball, and place it in the center of our board by dividing `this` game instances `width` and `height` properties by two and settign those as the `x` and `y` coordinates for the ball. 

```JS title="game.js" linenums="1"

let ball;

function create() {
    ball = this.physics.add.sprite( 
    this.physics.world.bounds.width / 2, // x parameter
    this.physics.world.bounds.height / 2, // y parameter
    `ball` // the `key` for our sprite we created in step 1
    )
};

```

!!! Example "Experiment"

    Try setting the sprite to `paddle` TODO: add a section here where they set sprite to paddle to show that phaser autosets our anchor to the middle of a sprite, note a developer might not want to do this in other types of games like platformers and to experiment with different anchor placements.


4. Now lets add our paddle. We are going to declare two players outside of the `create` function. When declaring our players, it's important to remember that we won't want our paddles to be pressed up against the edge of the screen. To do this, we will offset the paddles by referencing the balls width. 

```JS title="game.js" linenums="1"

let ball;
let player1;
let player2;
let isGameStarted;

function create() {
    ball = this.physics.add.sprite( 
        //... 
    )

    player1 = this.physics.add.sprite( 
        this.physics.world.bounds.width - (ball.body.width / 2),
        // x parameter placed at the right edge of the screen and offset by half of the balls width.
        
        this.physics.world.bounds.height / 2, // y parameter
        `paddle` // the `key` for our sprite we created in step 1
    )

    player2 = this.physics.add.sprite( 
    ball.body.width / 2 + 1, 
    // x parameter placed at the left edge of the screen a little over half the width of the ball

    this.physics.world.bounds.height / 2, // y parameter
    `paddle` // the `key` for our sprite we created in step 1
    )

};

```

!!! Danger "Danger"

    Notice how in this step, the name of the sprite is not the same as the name of the variable.
    If your sprites are not rendering, it might be because you used the wrong value for the key of our sprite. While it can be helpful to have your assets share a name with your variables, it can cause confusion in larger projects where you might have to reuse the asset elsewhere.
    For example, if we called both variables `paddle` the game would get confused as to which player we are referring to.

5. moving to our update function in the same file, we are now going to add some behavior to our game objects. First, let's start by setting an initial velocity for our ball value.

```JS title="game.js" linenums="1"

function update() {
    const initialVelocityX = 100;
    const initialVelocityY = 100;

    ball.setVelocityX = initialVelocityX;
    ball.setVelocityY = initialVelocityY;
}

```

6. Now we need to add collision, currently our ball simply continues in one direction until it dissapears off of the edge of the screen. We can add collision by calling method on our 'ball' instance to let the game know this element should detect and react to colliding with the edge of our game instance.

```JS title="game.js" linenums="1"
function create() {
    ball = this.physics.add.sprite( 
        //... 
    )
}

ball.setCollisionWorldBounds(true);

```

7. Now that our ball is colliding, we need to give it some bounce when it does or else it will stay wherever it lands once colliding with the edge of the screen. 

```JS title="game.js" linenums="1"
function create() {
    ball = this.physics.add.sprite( 
        //... 
    )
}

ball.setCollisionWorldBounds(true);
ball.setBounce(1, 1);

```

8. Next after setting bounce and collision, we can return to the top of the `game.js` file. Here we will add a `isGameStarted` variable


```JS title="game.js" linenums="1"

let ball;
let player1;
let player2;
let isGameStarted;

```

9. To ensure the balls location only updates when the game is started, we can reference the variable we created in step eight and wrap it in an if function - we then move all 


```JS title="game.js" linenums="1"

function update {
    if (isGameStarted) {
        const initialVelocityX = 100;
        const initialVelocityY = 100;
        ball.setVelocityX = initialVelocityX;
        ball.setVelocityY = initialVelocityY;
        isGameStarted = true;
        }
    } 

```

10. Next, moving back inside our create() function, we are going to add collision to our paddles so that the ball bounces off of them as well. 

``` JS title="game.js" linenums="1"

 create {
    //...

    this.physics.add.collider('ball', 'player1');
    this.physics.add.collider('ball', 'player2');

    
    }

```
