# Adding Win Conditions, Restart Feature, and Scoring System

## Overview

## Add Win Conditions
1. Declare variables `p1victoryText` and `p2victoryText` for displaying the victory text:
```JS title="game.js" linenums="26" hl_lines="9-10"
const game = new Phaser.Game(config);
let ball;
let player1;
let player2;
let isGameStarted = false;
let cursors;
const paddleSpeed = 350;
let keys = {};
let p1victoryText;
let p2victoryText;
```

2. At the bottom of the `create()` function, define `p1victoryText` and `p2victoryText` as text added to the screen:
```JS title="game.js" linenums="72" hl_lines="4-18"
    this.physics.add.collider(ball, player1);
    this.physics.add.collider(ball, player2);
    
    p1victoryText = this.add.text(
        this.physics.world.bounds.width / 2,
        this.physics.world.bounds.height / 2,
        'Player 1 wins!'
    );
    p1victoryText.setVisible(false);
    p1victoryText.setOrigin(0.5);

    p2victoryText = this.add.text(
        this.physics.world.bounds.width / 2,
        this.physics.world.bounds.height / 2,
        'Player 2 wins!'
    );
    p2victoryText.setVisible(false);
    p2victoryText.setOrigin(0.5);
} // end of create() function
```
    1. hello
    2. world
    
3. In the `update()` function, add the following checks to see which player has won, as well as make the correct victory text appear:
```JS title="game.js" linenums="92" hl_lines="10-20"
function update() {
    if (!isGameStarted) {
        const initialVelocityX = (Math.random() * 150) + 100;
        const initialVelocityY = (Math.random() * 150) + 100;
        ball.setVelocityX(initialVelocityX);
        ball.setVelocityY(initialVelocityY);
        isGameStarted = true;
    }
    
    if (ball.body.x > player1.body.x) {
        p2victoryText.setVisible(true);
        ball.body.setVelocityX(0);
        ball.body.setVelocityY(0);
    }
    
    if (ball.body.x < player2.body.x) {
        p1victoryText.setVisible(true);
        ball.body.setVelocityX(0);
        ball.body.setVelocityY(0);
    }

    //...
```

    1. hello
    2. world

!!! Success "Proper Win Conditions"

    You should now see victory text appear in the middle of the screen when a player wins the match.

    ![Victory text displayed when a player wins the match.](assets/images/win-screen.png)
    
!!! Info "Note"

## Restarting the Match
1. Inside the `create()` function, add the Spacebar as a valid key in the game:
```JS title="game.js" linenums="68" hl_lines="4"
    cursors = this.input.keyboard.createCursorKeys();
    keys.w = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.W);
    keys.s = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.S);
    keys.space = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.SPACE);
```
2. In the `update()` function, add the following code under the `if (!isGameStarted)` conditional:
```JS title="game.js" linenums="93" hl_lines="3-4"
function update() {
    if (!isGameStarted) {
        ball.body.x = this.physics.world.bounds.width / 2;
        ball.body.y = this.physics.world.bounds.height / 2;
        const initialVelocityX = (Math.random() * 150) + 100;
        const initialVelocityY = (Math.random() * 150) + 100;
        ball.setVelocityX(initialVelocityX);
        ball.setVelocityY(initialVelocityY);
        isGameStarted = true;
    }
    
    //...
}
```

    1. hello
    2. world
    
3. 
```JS title="game.js" linenums="93" hl_lines="24-30"
function update() {
    if (!isGameStarted) {
        ball.body.x = this.physics.world.bounds.width / 2;
        ball.body.y = this.physics.world.bounds.height / 2;
        const initialVelocityX = (Math.random() * 150) + 100;
        const initialVelocityY = (Math.random() * 150) + 100;
        ball.setVelocityX(initialVelocityX);
        ball.setVelocityY(initialVelocityY);
        isGameStarted = true;
    }
    
    if (ball.body.x > player1.body.x) {
        p2victoryText.setVisible(true);
        ball.body.setVelocityX(0);
        ball.body.setVelocityY(0);
    }
    
    if (ball.body.x < player2.body.x) {
        p1victoryText.setVisible(true);
        ball.body.setVelocityX(0);
        ball.body.setVelocityY(0);
    }

    if (ball.body.x < player2.body.x || ball.body.x > player1.body.x) {
        if (keys.space.isDown) {
            isGameStarted = false;
            p1victoryText.setVisible(false);
            p2victoryText.setVisible(false);
        }
    }
    
    //...
}
```




## Creating a Scoring System
1. aaaaa
```JS title="game.js" linenums="26" hl_lines="11-14"
const game = new Phaser.Game(config);
let ball;
let player1;
let player2;
let isGameStarted = false;
let cursors;
const paddleSpeed = 350;
let keys = {};
let p1victoryText;
let p2victoryText;
let scoreAdded = false;
let scoreText;
let p1Score = 0;
let p2Score = 0;
```

2. aaaa
```JS title="game.js" linenums="79" hl_lines="17-22"
    p1victoryText = this.add.text(
        this.physics.world.bounds.width / 2,
        this.physics.world.bounds.height / 2,
        'Player 1 wins!'
    );
    p1victoryText.setVisible(false);
    p1victoryText.setOrigin(0.5);

    p2victoryText = this.add.text(
        this.physics.world.bounds.width / 2,
        this.physics.world.bounds.height / 2,
        'Player 2 wins!'
    );
    p2victoryText.setVisible(false);
    p2victoryText.setOrigin(0.5);
    
    scoreText = this.add.text(
        this.physics.world.bounds.width / 2,
        30,
        `${p2Score} : ${p1Score}`
    );
    scoreText.setOrigin(0.5);
```

3. aaaaa
```JS title="game.js" linenums="103" hl_lines="13-16 23-26"
function update() {
    if (!isGameStarted) {
        ball.body.x = this.physics.world.bounds.width / 2;
        ball.body.y = this.physics.world.bounds.height / 2;
        const initialVelocityX = (Math.random() * 150) + 100;
        const initialVelocityY = (Math.random() * 150) + 100;
        ball.setVelocityX(initialVelocityX);
        ball.setVelocityY(initialVelocityY);
        isGameStarted = true;
    }
    
    if (ball.body.x > player1.body.x) {
        if (!scoreAdded) {
            p2Score++;
            scoreAdded = true;
        }
        p2victoryText.setVisible(true);
        ball.body.setVelocityX(0);
        ball.body.setVelocityY(0);
    }
    
    if (ball.body.x < player2.body.x) {
        if (!scoreAdded) {
            p1Score++;
            scoreAdded = true;
        }
        p1victoryText.setVisible(true);
        ball.body.setVelocityX(0);
        ball.body.setVelocityY(0);
    }
```

4. aaaaa
```JS title="game.js" linenums="114" hl_lines="24"
    if (ball.body.x > player1.body.x) {
        if (!scoreAdded) {
            p2Score++;
            scoreAdded = true;
        }
        p2victoryText.setVisible(true);
        ball.body.setVelocityX(0);
        ball.body.setVelocityY(0);
    }
    
    if (ball.body.x < player2.body.x) {
        if (!scoreAdded) {
            p1Score++;
            scoreAdded = true;
        }
        p1victoryText.setVisible(true);
        ball.body.setVelocityX(0);
        ball.body.setVelocityY(0);
    }

    if (ball.body.x < player2.body.x || ball.body.x > player1.body.x) {
        if (keys.space.isDown) {
            isGameStarted = false;
            scoreAdded = false;
            p1victoryText.setVisible(false);
            p2victoryText.setVisible(false);
        }
    }
```

5. aaaaa
```JS title="game.js" linenums="134" hl_lines="10"
    if (ball.body.x < player2.body.x || ball.body.x > player1.body.x) {
        if (keys.space.isDown) {
            isGameStarted = false;
            scoreAdded = false;
            p1victoryText.setVisible(false);
            p2victoryText.setVisible(false);
        }
    }

    scoreText.setText(`${p2Score} : ${p1Score}`)
```

!!! Success "Congratulations!"

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
    let p1victoryText;
    let p2victoryText;
    let scoreAdded = false;
    let p1Score = 0;
    let p2Score = 0;
    
    function preload() {
        this.load.image("ball", "../assets/images/ball.png");
        this.load.image("paddle", "../assets/images/paddle.png");
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
        keys.space = this.input.keyboard.addKey(Phaser.Input.Keyboard.KeyCodes.SPACE);
        
        this.physics.add.collider(ball, player1);
        this.physics.add.collider(ball, player2);
        
        p1victoryText = this.add.text(
            this.physics.world.bounds.width / 2,
            this.physics.world.bounds.height / 2,
            'Player 1 wins!'
        );
        p1victoryText.setVisible(false);
        p1victoryText.setOrigin(0.5);
    
        p2victoryText = this.add.text(
            this.physics.world.bounds.width / 2,
            this.physics.world.bounds.height / 2,
            'Player 2 wins!'
        );
        p2victoryText.setVisible(false);
        p2victoryText.setOrigin(0.5);
        
        scoreText = this.add.text(
            this.physics.world.bounds.width / 2,
            30,
            `${p2Score} : ${p1Score}`
        );
        scoreText.setOrigin(0.5);
    }
    
    function update() {
        if (!isGameStarted) {
            ball.body.x = this.physics.world.bounds.width / 2;
            ball.body.y = this.physics.world.bounds.height / 2;
            const initialVelocityX = (Math.random() * 150) + 100;
            const initialVelocityY = (Math.random() * 150) + 100;
            ball.setVelocityX(initialVelocityX);
            ball.setVelocityY(initialVelocityY);
            isGameStarted = true;
        }
        
        if (ball.body.x > player1.body.x) {
            if (!scoreAdded) {
                p2Score++;
                scoreAdded = true;
            }
            p2victoryText.setVisible(true);
            ball.body.setVelocityX(0);
            ball.body.setVelocityY(0);
        }
        
        if (ball.body.x < player2.body.x) {
            if (!scoreAdded) {
                p1Score++;
                scoreAdded = true;
            }
            p1victoryText.setVisible(true);
            ball.body.setVelocityX(0);
            ball.body.setVelocityY(0);
        }
    
        if (ball.body.x < player2.body.x || ball.body.x > player1.body.x) {
            if (keys.space.isDown) {
                isGameStarted = false;
                scoreAdded = false;
                p1victoryText.setVisible(false);
                p2victoryText.setVisible(false);
            }
        }
    
        scoreText.setText(`${p2Score} : ${p1Score}`);
    
        
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