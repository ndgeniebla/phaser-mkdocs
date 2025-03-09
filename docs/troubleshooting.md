# Troubleshooting

| Symptoms | Probable Cause | Action |
| -------- | -------------- | ------ |
| Blank White Web Page | The HTML parent element that Phaser is looking to hook the game onto is missing. | Check that `<div id="game">` element exists inside of the body of the `index.html` file. |
| | The HTML parent element's ID does not match with the parent ID given in the Phaser `config` object. | Make sure that the id of your `<div>` matches with the `parent` attribute set inside of the `config` object in `game.js`. |
| | Wrong letter casing when accessing attributes from the Phaser Object | Make sure that any attribute that you're accessing on the `Phaser` object (i.e. `Phaser.AttributeName`) matches the case inside of the instructions. |
| | Syntax errors | Open Developer Tools (press F12 or Right-click and select **Inspect**) and open the Console. JavaScript errors will be displayed there. |
| Web page not displaying at `localhost:XXXX` | The live server is not running. | Press the **Go Live** button at the bottom right of the VS Code window to start the live server. |
| | The port number in the URL is incorrect. | Ensure that the port number in the URL matches the Live Server port at the bottom right of the VS Code window. |
| Paddle/Ball images not visible | The file path to the image assets is incorrect. | Make sure that the file path in the `this.load.image(...)` methods in the `preload()` function match with the path for the image assets. |
| Paddle/Ball go offscreen | Collision with world bounds was not set for the game objects. | Make sure that `setCollideWorldBounds(true)` is called for the `ball`, `player1`, and `player2` objects. |
| Paddles get thrown off course when hit by the ball | The `setImmovable()` property of the player paddles was not set to `true`. | Make sure that `player1.setImmovable(true)` and `player2.setImmovable(true)` is called inside the `create()` function. |
| Ball goes through player paddles | The physics collider was not set between the ball and the player paddles. | Check if `this.physics.add.collider` was set between the ball and each player paddle (e.g. `this.physics.add.collider(ball, player1)`) |
