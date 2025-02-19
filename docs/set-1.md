# Setting up a Basic Phaser Project

## Prerequisites (maybe cover this in overview?)
- have the following installed on your machine:
    - Node.js
    - TypeScript
- have super basic knowledge of the git clone command (literally just running the thing)

## Overview
- Using TypeScript and the Vite bundler for bundling all of source files into one file.
- Phaser 3.88.2
- add details of what the expected result should be
    - at the end you should get a starter project with all the necessary files and libraries to start on your Phaser Project

## Installation
1. Navigate to directory where you want to have your game
    - note that a new directory will be made, so you may make a redundant directory
    - show image of result
2. Open Command Prompt.
3. Copy and paste the following command into the Command Prompt and press Enter:

    `$ git clone https://github.com/phaserjs/template-esbuild-ts.git`

    This will create a new directory with the files for the template.
    
    The current directory should look like this: (show image)

4. Open Visual Studio Code.
5. Go to **File > Open Folder** and select the newly created Phaser folder
    - Now you should see VS Code like this, with the project open (show image)
6. Open the terminal in VS Code
    - Use a hotkey like Ctrl-J or go to **Terminal > New Terminal** to create a new terminal instance.
    - make sure that the path is set to be inside of the project folder
7. Run the command in the terminal `$ npm install`
    - after waiting for everything to install, your project structure should look like this: (show image)

## Starting the Game
1. With the terminal still open in VS Code, run the following command: 

    `$ npm run dev`

2. Open a browser (Chrome, Firefox, Edge, etc.)
3. In the URL bar at the top, copy + paste in the following URL and press Enter: 

    `http://localhost:8080`
    
    You should now see this page pop up: (show image)

Congratulations!