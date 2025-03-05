# Creating Our First Game Objects and Player Characters

## Prerequisites
- Ye have configured your game instance of phaser

## Overview
In this section, we will cover how to preload assets, create game objects, assign them sprites and 
set their locations, and get them moving.

## Preloading Assets

Now that we have our game instance, it's time to add some game assets to give our player something to look at and control

!!! Info "Information"

        Assets have many definitions in the real world. In the context of game developement, assets mean any digital content used by the video game to communicate information to the user about the state of the game. This can include audio, visual elements and animations.

<br>
3. Inside the `preload` function defined inside of `src/game.js` add two function calls to `this` game instances `load.image()` method with the following name parameter and path path paramater.

```JS title="game.js" linenums="1"

function preload() {
    this.load.image('ball', '../assets/images/ball.png') // name, path
    this.load.image('paddle', '../assets/images/paddle.png') // name, path
}

```

!!! Info "Information" 
    
    this function tells the game instance to pre-load the images we want to use in the game itself. If you had other assets you wanted to load in such as music or animations, you would define them here as well using their respective `load` methods. 

<br>
2. Outside the create function define our `ball` variable.

```JS title="game.js" linenums="1"

let ball;

function create() {
};


```

<br>
3. inside the create function, we are going to `add` our first game object: the ball. by calling `this` game instances `add.sprite` method we can add a sprite (our preloaded image asset) to the ball, and place it in the center of our board. We find the center by dividing `this` game instances `width` and `height` properties by two and settign those as the `x` and `y` coordinates for the ball. 

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

    Try setting the sprite to `paddle` and notice where on the paddle the game considers the center. Think about how this would affect our placement of objects - we don't want our characters to clip off screen when they are located at the edge afterall. If you wanted to modify the center point of an object- try calling the setOrigin method. 

<br>
4. Now lets add our paddle. We are going to declare two players outside of the `create` function. When declaring our players, it's important to remember that we won't want our paddles to be pressed up against the edge of the screen. To do this, we will offset the paddles `x` and `y` parameters. 


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

<br>
5. moving to our update function in the same file, we are now going to add some behavior to our game objects. First, let's start by setting the initial velocity for our ball value to get it moving.

```JS title="game.js" linenums="1"

function update() {
    const initialVelocityX = 100;
    const initialVelocityY = 100;

    ball.setVelocityX = initialVelocityX;
    ball.setVelocityY = initialVelocityY;
}

```

<br>
6. Now we need to add collision, currently our ball simply continues in one direction until it dissapears off of the edge of the screen. We can add collision by calling the `setCollisionWorldBounds` method on our 'ball' instance to let the game know this element should detect and react to colliding with the edge of our game instance.

```JS title="game.js" linenums="1"
function create() {
    ball = this.physics.add.sprite( 
        //... 
    )
}

ball.setCollisionWorldBounds(true);

```

<br>
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

<br>
8. Next after setting bounce and collision, we can return to the top of the `game.js` file. Here we will add a `isGameStarted` variable


```JS title="game.js" linenums="1"

let ball;
let player1;
let player2;
let isGameStarted;

```
<br>
9. To ensure the balls location only updates when the game is started, we can reference the variable we created in step eight and wrap it in an if function - we then move all 


```JS title="game.js" linenums="1"

function function update() {
    if (isGameStarted) {
        const initialVelocityX = 100;
        const initialVelocityY = 100;
        ball.setVelocityX = initialVelocityX;
        ball.setVelocityY = initialVelocityY;
        isGameStarted = true;
    }
} 

```

<br>
10. Next, moving back inside our create() function, we are going to add collision to our paddles so that the ball bounces off of them as well. 

``` JS title="game.js" linenums="1"

function create() {
    //...

    this.physics.add.collider('ball', 'player1');
    this.physics.add.collider('ball', 'player2');

}

```

<br>
11. Now that we've added collision to our paddles, you might notice some odd behavior. We need to make it so our paddles while being able to collide with the ball without being moved themselves -  they are `immovable`. We do this by calling the `setImmovable` method on both player objects iniside the create function. We will also give it the same collision with the wporld boundary to make sure are paddles don't fly offscreen.



``` JS title="game.js" linenums="1"

function create() {
    //...

    this.physics.add.collider('ball', 'player1');
    this.physics.add.collider('ball', 'player2');

    player1.setImmovable(true);
    player2.setImmovable(true);

    player1.setCollideWorldBounds(true);
    player2.setCollideWorldBounds(true);
    
}

```
<br>
12. Add a cursors variable at the top of our file, this will represent our arrow keys. we are working on allowing the players to use their keys to move the paddles so we will also want to add an empty object with the necessary keys for player two.

``` JS title="game.js" linenums="1"

let ball;
let player1;
let player2;
let isGameStarted;
let cursors;
let keys = {}

```

!!! Warning "Warning"

    You might be wondering why we declare keys as an object and cursors as an empty variable. This is because of how Phaser recognizes keys - it treats all your arrow keys as one pre-defined set called cursors, other keys have to have their purpose defined individually. You'll notice as you continue through these instructions - we use slightly different language when creating our inputs - make sure to pay attention to the differences as they do not work interchangeably.

<br>
13. we will also add a paddle speed variable so that we can easily change the speed if it doesn't feel right.

```JS title="game.js" linenums="1"

let ball;
let player1;
let player2;
let isGameStarted;
let cursors;
let keys = {}
let paddleSpreed = 350;

```

<br>
14. Back inside our create function, lets add input to our cursor variable and our keys variables by calling `createCursorKeys` and  `addKey` from the game instances input method. 

``` JS title="game.js" linenums="1"

function create() {
    //...

    cursors = this.input.keyboard.createCursorKeys();
    keys.w = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.W); 
    //don't worry! This might look intimidating but it simply lets our game instance know to expect input from the W key

    keys.s = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.S);

}

```

<br>
15. Now inside our update function, we are going to tell the game what to do when these cursors are pressed and what to do when they are not. 


``` JS title="game.js" linenums="1"

function update() {
    //...

    if (cursors.up.isDown) {
        player1.body.setVelocityY(-paddleSpeed);
    }

    if (cursors.down.isDown) {
        player1.body.setVelocityY(paddleSpeed);
    }

        if (keys.w.isDown) {
        player2.body.setVelocityY(-paddleSpeed);
    }

    if (keys.s.isDown) {
        player2.body.setVelocityY(paddleSpeed);
    } 
}

```

!!! Info "Information"

    You might be wondering what the code means as the wording is odd, `cursor.down.isDown`? What this actually means is quite simple. isDown in this context simply means when the key is pressed down. 

!!! Info "Information"

    You might be wondering why we use negative paddle speeds when moving the paddles up. This is because Phaser perceives all positive velocity y values to be moving from up to down, so if we want to move down to up, we have to use a negative value.
    If you wanted to make a game where a character moves left and right, you would have to use the same strategy for the X axis. 

<br>
16. Now we need to make sure that when a key is not being pressed. We can do this by calling the `player1` and `player2` `setVelocityY` methods in the update function and assigning a velocity of 0 to the paddles.

``` JS title="game.js" linenums="1"

function update() {
    //...

  player1.body.setVelocityY(0);
  player2.body.setVelocitY(0);

    if (cursors.up.isDown) {
        player1.body.setVelocityY(-paddleSpeed);
    }

    if (cursors.down.isDown) {
        player1.body.setVelocityY(paddleSpeed);
    }

        if (keys.w.isDown) {
        player2.body.setVelocityY(-paddleSpeed);
    }

    if (keys.s.isDown) {
        player2.body.setVelocityY(paddleSpeed);
    } 
}

```

<br>
17. Now inside our update function, we are going to tell the game what to do when the ball starts moving too quickly or slowly. We can define this by referring to our paddlespeed inside of an if condition, and changing the balls behavior if it gets to fast. By setting both these traits - we lock the ball into moving at one speed- perfect!

``` JS title="game.js" linenums="1"

function update() {
    //...

    player1.body.setVelocityY(0);
    player2.body.setVelocitY(0);

    if (cursors.up.isDown) {
        player1.body.setVelocityY(paddleSpeed);
    }

    if (cursors.down.isDown) {
        player1.body.setVelocityY(paddleSpeed);
    }
    
    if (ball.body.velocity.y > paddleSpeed) {
        ball.body.setVelocityY(paddleSpeed);
    } 

     if (ball.body.velocity.y < -paddleSpeed) {
        ball.body.setVelocityY(-paddleSpeed);
    } 
}

```

!!! Example "Experiment"

    Try playing with the speed of the ball by adding or decreasing its max and min velocity. Notice how when the max velocity is higher, it can put the players in unwinnable situations- where the paddle moves to slowly to meet the ball. How about when it moves slowly? The game get's easier. By changing these values - we can increase and decrease the difficulty of our game!


!!! Success "Success"

    If you have followed along with the tutorial so far, you should currently have a verson of pong that has two controllable paddles using the S and W keys for one player and the up and down arrows for another. 

    
    
    ## Conclusion
    By the end of this section, you will have learned the following:
    
    - How to configure a Phaser game instance
    - How to create a Phaser game instance
    - How to declare a scene and its functions for further development.

    ``` title="game.js" linenums="1"
    
    let ball;
    let player2;
    let player1;
    let isGameStarted;
    let cursors;
    let keys = {}
    let paddleSpreed = 350;


    function create() {

    ball = this.physics.add.sprite(
        this.physics.world.bounds.width / 2,
        this.physics.world.bounds.height / 2,
        'ball' 
    );
        
    player1 = this.physics.add.sprite(
        this.physics.world.bounds.width - (ball.body.width / 2 + 1),
        this.physics.world.bounds.height / 2,
        'paddle',
    );

    player2 = this.physics.add.sprite(
        (ball.body.width / 2 + 1),
        this.physics.world.bounds.height / 2,
        'paddle',
    );

    player1.setCollideWorldBounds(true);
    player2.setCollideWorldBounds(true);
    ball.setCollideWorldBounds(true);
    ball.setBounce(1, 1);
    player1.setImmovable(true);
    player2.setImmovable(true);
    this.physics.add.collider(ball, player1);
    this.physics.add.collider(ball, player2);

    }

    function update() {
        player1.body.setVelocityY(0);
        player2.body.setVelocityY(0);

        if (cursors.up.isDown) {
            player1.body.setVelocityY(-paddleSpeed);
        } else if (cursors.down.isDown) {
            player1.body.setVelocityY(paddleSpeed);
        }
        
        if (keys.w.isDown) {
            player2.body.setVelocityY(-paddleSpeed);
        } else if (keys.s.isDown) {
            player2.body.setVelocityY(paddleSpeed);
        }

        if (!gameStarted) {
            if (cursors.space.isDown) {
                gameStarted = true;
                const initialXSpeed = paddleSpeed;
                const initialYSpeed = paddleSpeed;
                ball.setVelocityX(initialXSpeed);
                ball.setVelocityY(initialYSpeed);
            }
        }
    }

    ``` 
    Well done :partying_face:! Now you can move onto the next step:
    
    **[Adding Win Conditions, Math Resetting, and Score Systems](set-5.md)**
    
    
    