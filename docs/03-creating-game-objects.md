# Pong: Creating Our First Game Objects and Player Characters

## Prerequisites
- Configured and created a Phaser game instance.

## Overview
In this section, we will cover how to preload assets, create game objects, assign them sprites,
set their locations, and get them moving.

## Preloading Assets

Now that we have our game instance, it's time to add some game assets to give our players something to look at and control.

!!! Info "Information"

    The word "assets" has many definitions in the real world. In the context of game development, assets mean any digital content used by the video game to communicate information to the user about the state of the game. This can include audio, visual elements and animations.

## Making Our Ball

<br>
1. Inside the `preload` function defined inside of `src/game.js` add two function calls to `this` game instances `load.image()` method with the following name parameter and path path paramater.

```JS title="game.js" linenums="1" hl_lines="2-3"

function preload() {
    this.load.image('ball', '../assets/images/ball.png') // name, path
    this.load.image('paddle', 'assets/images/paddle.png') // name, path
}

```

!!! Info "Information" 
    
    This function tells the game instance to pre-load the images we want to use in the game itself. If you had other assets you wanted to load in such as music or animations, you would define them here as well using their respective `load` methods. 

<br>
2. directly above the `create function`, define some variables and one `keys` object to use inside of our `create` and `update` functions. These variables are used throughout our examples.

```JS title="game.js" linenums="1" hl_lines="1-7"

let ball;
let player1;
let player2;
let paddleSpeed = 350;
let isGameStarted = false;
let cursors;
let keys = {};

function create() {
};


```


!!! Info "Info"

    You might be wondering why we declare `keys` as an object and `cursors` as an empty variable. This is because of how Phaser recognizes keys - it treats all your arrow keys as one pre-defined object called `cursors`, other keys have to have their purpose defined individually. You'll notice as you continue through these instructions - we use slightly different language when creating our inputs - make sure to pay attention to the differences as they do not work interchangeably.

<br>
3. Inside the `create()` function, `add` your first game object: the ball. by calling `this` game instances `add.sprite` method it adds a sprite (our preloaded image asset) to the ball, and places it in the center of our board. Find the center by dividing `this` game instances `width` and `height` properties by two and settign those as the `x` and `y` coordinates for the ball. 

```JS title="game.js" linenums="1" hl_lines="4-7"

let ball;

    function create() {
        ball = this.physics.add.sprite( 
        this.physics.world.bounds.width / 2, // x parameter
        this.physics.world.bounds.height / 2, // y parameter
        `ball` // sprite parameter
    )
};

```

<br>
4. moving to our `update function` in the same file, set the initial velocity for our `ball` to add some behavior to our game object and get it moving.

```JS title="game.js" linenums="1" hl_lines="2-3 5-6"

function update() {
    const initialVelocityX = (Math.random() * 150) + 100;
    const initialVelocityY = (Math.random() * 150) + 100;

    ball.setVelocityX(initialVelocityX);
    ball.setVelocityY(initialVelocityY);
}

```

<br>
5. To ensure the balls location only `updates` when the game is started, add an `if` statement that contains all the code inside of our `update function`. Inside this if statement, reference our `isGameStarted` variable.


```JS title="game.js" linenums="1" hl_lines="2 8"

function function update() {
    if (!isGameStarted) {
        const initialVelocityX = (Math.random() * 150) + 100;
        const initialVelocityY = (Math.random() * 150) + 100;
        ball.setVelocityX(initialVelocityX);
        ball.setVelocityY(initialVelocityY);
    }
} 

```

!!! Warning "Warning"

    At this point your ball will have stopped moving. Don't worry! This is intended behavior at the moment as we have not set our `isGameStarted` variable to true. This means everytime the game calls the `update function` - it sees the `isGameStarted` variable is falsey and skips moving the ball.

<br>
6. To ensure the ball starts moving when the game is started- add an `if` statement that sets `isGameStarted` to true when the game calls the `update` function for the first time. 

```JS title="game.js" linenums="1" hl_lines="7"

function function update() {
    if (isGameStarted) {
        const initialVelocityX = (Math.random() * 150) + 100;
        const initialVelocityY = (Math.random() * 150) + 100;
        ball.setVelocityX(initialVelocityX);
        ball.setVelocityY(initialVelocityY);
        isGameStarted = true;
    }
} 

```


<br>
7. Currently, our `ball` simply continues in one direction until it dissapears off the edge of the screen. Call the `setCollideWorldBounds` method on our `ball` to let the game know this element should detect colliding with the edge of our screen.

```JS title="game.js" linenums="1" hl_lines="6"
function create() {
    ball = this.physics.add.sprite( 
        //... 
    );

    ball.setCollideWorldBounds(true);

};


```

<br>
8. Now that the `ball` is colliding, give it some bounce. Call `setBounce` on the `ball` variable to let the game know that when it does collide with something- it should bounce off instead of sticking to it.

```JS title="game.js" linenums="1"  hl_lines="7"
function create() {
    ball = this.physics.add.sprite( 
        //... 
    )
    
    ball.setCollisionWorldBounds(true);
    ball.setBounce(1, 1);

}

```


## Adding Player Characters: A Tale of Two Paddles

1. Call the `this` game instances `physics.add.sprite` method inside of the `create` function. When declaring our players, it's important to remember that we won't want our paddles to be pressed up against the edge of the screen. To do this, offset the paddles `x` and `y` parameters. 


```JS title="game.js" linenums="1" hl_lines="9-13 15-19"

function create() {
    ball = this.physics.add.sprite( 
        //... 
    )

    ball.setCollisionWorldBounds(true);
    ball.setBounce(1, 1);

    player1 = this.physics.add.sprite( 
        this.physics.world.bounds.width - (ball.body.width / 2), // x parameter with an offset        
        this.physics.world.bounds.height / 2, // y parameter with an offset
        `paddle`
    )

    player2 = this.physics.add.sprite( 
        ball.body.width / 2 + 1, // x parameter with an offset
        this.physics.world.bounds.height / 2, // y parameter with an offset
        `paddle` 
    )
};

```

!!! Danger "Danger"

    Notice how in this step, the name of the sprite is not the same as the name of the variable.
    If your sprites are not rendering, it might be because you used the wrong value for the key of our sprite. While it can be helpful to have your assets share a name with your variables, it can cause confusion in larger projects where you might have to reuse the asset elsewhere.

    ??? Abstract "Click To See An Example"
        ``` JS title="example.js" linenums="1" hl_lines="1 2 12 15 18 21"

        let paddle;
        let paddle;

        ball.setCollisionWorldBounds(true);
        ball.setBounce(1, 1);

        function create() {
            ball = this.physics.add.sprite( 
                //... 
            )

            paddle = this.physics.add.sprite( 
                this.physics.world.bounds.width - (ball.body.width / 2), // x parameter with an offset        
                this.physics.world.bounds.height / 2, // y parameter with an offset
                `paddle`
            )

            paddle = this.physics.add.sprite( 
                ball.body.width / 2 + 1, // x parameter with an offset
                this.physics.world.bounds.height / 2, // y parameter with an offset
                `paddle` 
            )
        };
        ```


<br>
2. Now add collision to the paddles. When adding collision- you have to use seperate methods for collision between game objects and a game object and the world. `this.physics.add.collider` takes two game objects as inputs and creates collision between those two objects. `gameObject.setCollideWorldBounds` adds collision between a game object and your screen.

``` JS title="game.js" linenums="1" hl_lines="17-18 20-21"

function create() {
     ball = this.physics.add.sprite( 
        //... 
    )

    ball.setCollisionWorldBounds(true);
    ball.setBounce(1, 1);

    player1 = this.physics.add.sprite( 
        //..
    )

    player2 = this.physics.add.sprite( 
        //..
    )

    this.physics.add.collider(ball, player1);
    this.physics.add.collider(ball, player2);

    player1.setCollideWorldBounds(true);
    player2.setCollideWorldBounds(true);
}

```

<br>
3. Next, we need to ensure that when the `ball` makes contact with our paddle, the paddle does not move -  they are `immovable`. Call the `setImmovable` method on both player objects iniside the `create function`.



``` JS title="game.js" linenums="1" hl_lines="23-24"

function create() {
     ball = this.physics.add.sprite( 
        //... 
    )

    ball.setCollisionWorldBounds(true);
    ball.setBounce(1, 1);

    player1 = this.physics.add.sprite( 
        //..
    )

    player2 = this.physics.add.sprite( 
        //..
    )

    this.physics.add.collider(ball, player1);
    this.physics.add.collider(ball, player2);

    player1.setCollideWorldBounds(true);
    player2.setCollideWorldBounds(true);

    player1.setImmovable(true);
    player2.setImmovable(true);
}

```

## Input and Control

<br>
1. Inside our `create function`, call `this` game instances `input.keybord.addKey` and `this.input.keyboard.createCursorKeys` to add these keys to our gameInstance. This lets it know to watch these keys for events. 

``` JS title="game.js" linenums="1" hl_lines="4-5 9"

function create() {
    //...

    cursors = this.input.keyboard.createCursorKeys();
    keys.w = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.W); 
    //don't worry! This might look intimidating but it simply lets our game
    //instance know to expect input from the W key

    keys.s = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.S);
}

```

<br>
2. Inside our `update` function, we are going to tell the game what to do when these `cursors` or `keys` are pressed and what to do when they are not. We can do so using `if` statements wrapped around some behavior for our paddles. In this case, we will make it so that triggering these events causes our paddles to gain or lose velocity. Add the if statements.


``` JS title="game.js" linenums="1" hl_lines="4-6 8-10 12-14 16-18"

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
3. Make sure that when a key is not being pressed, the paddles stop. Call the `player1` and `player2` `setVelocityY` methods in the `update function` and assigning a velocity of 0 to the paddles.

``` JS title="game.js" linenums="1" hl_lines="4-5"

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
4. Inside our `update function`, clamp the balls velocity. Do this by referring to our paddlespeed inside of an if condition, and changing the balls behavior if it gets to fast or slow. By setting both these traits - we lock the ball into moving at one speed- perfect!

``` JS title="game.js" linenums="1" hl_lines="15-17 19-21"

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

    Try playing with the speed of the ball by adding or decreasing its max and min velocity. Notice how when the max velocity is higher, it can put the players in unwinnable situations- where the paddle moves to slowly to meet the ball. How about when it moves slowly? The game gets easier. By changing these values, we can increase and decrease the difficulty of our game!

!!! Success "Success"

    If you have followed along with the tutorial so far, you should currently have a verson of pong that has two controllable paddles using the S and W keys for one player and the up and down arrows for another. 

    ??? Abstract "Code"
        ```JS title="game.js" linenums="1"
        
        const config = {
            type: Phaser.AUTO,
            parent: 'game',
            width: 800,
            height: 640,
        
            scale: {
                mode: Phaser.Scale.RESIZE,
                autoCenter: Phaser.Scale.CENTER_BOTH
            },
        
            scene: {
                preload,
                create,
                update
            },
        
            physics: {
                default: 'arcade',
                arcade: {
                    gravity: false
                }
            }
        }
        
        const game = new Phaser.Game(config);
        let ball;
        let player1;
        let player2;
        let isGameStarted = false;
        let cursors;
        const paddleSpeed = 350;
        let keys = {};
        
        function preload() {
            this.load.image("ball", "assets/images/ball.png");
            this.load.image("paddle", "assets/images/paddle.png");
        }
        
        function create() {
            ball = this.physics.add.sprite(
                this.physics.world.bounds.width / 2,
                this.physics.world.bounds.height / 2,
                'ball'
            );
            ball.setCollideWorldBounds(true);
        
            ball.setBounce(1, 1);
        
            player1 = this.physics.add.sprite(
                this.physics.world.bounds.width - (ball.body.width / 2 + 1),
                this.physics.world.bounds.height / 2,
                'paddle'
            );
            player1.setImmovable(true);
            player1.setCollideWorldBounds(true);
        
            player2 = this.physics.add.sprite(
                ball.body.width / 2 + 1,
                this.physics.world.bounds.height / 2,
                'paddle'
            );

            player2.setImmovable(true);
            player2.setCollideWorldBounds(true);
            
            cursors = this.input.keyboard.createCursorKeys();
            keys.w = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.W);
            keys.s = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.S);
            
            this.physics.add.collider(ball, player1);
            this.physics.add.collider(ball, player2);
        }
        
        function update() {
            if (!isGameStarted) {
                const initialVelocityX = (Math.random() * 150) + 100;
                const initialVelocityY = (Math.random() * 150) + 100;
                ball.setVelocityX(initialVelocityX);
                ball.setVelocityY(initialVelocityY);
                isGameStarted = true;
            }
            

            player1.body.setVelocityY(0);
            player2.body.setVelocityY(0);
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
            
            
            if (ball.body.velocity.y > paddleSpeed) {
                ball.body.setVelocityY(paddleSpeed);
            }
            if (ball.body.velocity.y < -paddleSpeed) {
                ball.body.setVelocityY(-paddleSpeed);
            }
        
        }

        ``` 

        
## Conclusion
By the end of this section, you will have learned the following:
    
- How to create game objects
- How to give game objects collision properties
- How to create input to control game objects

Well done :partying_face:! Now you can move onto the next step:
    
**[Adding Win Conditions, Math Resetting, and Score Systems](04-final-features.md)**
    
    
    