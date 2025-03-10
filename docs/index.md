# Home

##Introduction

Hello and Welcome to PhaserFirst! By following this documentation, you will learn how to create a small [Phaser][1] project and kick off your game development journey. Throughout the document we will guide you step by step towards creating a simple version of the classic video game Pong with the goal of understanding the fundamentals of what makes up a Phaser project.
> **[Phaser.js][1]** (more commonly known as Phaser) is a free open-source framework for developing web based 2D games. Phaser provides a pre-defined project structure and many tools to build the game you want.

##Intended Users

This documentation is intended for:

- intermediate JavaScript developers who want to learn the basics of the [Phaser][1] framework

##Prerequisite Knowledge

This document assumes you know the following:

- Experience using JavaScript to build web based applications
- Basic knowledge of HTML
- Using the terminal to navigate projects and execute commands
- Comfortable using a code editor (like [Visual Studio Code][2])

> For our tutorial we will be using [Visual Studio Code (VSCode)][2]. Be aware that while using another code editor is possible, instructions and methods may not work for them. If you choose not to use [VScode][2], this tutorial may not work for you.

##Software Requirements

- Firefox
- [Visual Studio Code][2]

##Procedures Overview
The instruction sets below are an overview of creating a basic Pong game using Phaser 3.

1. [Setting up a Basic Phaser Project](01-setting-up.md)
2. [Pong: Creating and Configuring Our Game Instance ](02-configuring-creating-game-instance.md)
3. [Pong: Creating Our First Game Objects and Player Characters](03-creating-game-objects.md)
4. [Pong: Adding Win Conditions, Match Resetting, and Scoring System](04-final-features.md)

##Typographical Conventions

1. File names will be formatted like: `filename.js`
2. In code blocks, if you see `//...` it means there is code in that location not currently relevant to this step:

    ```JS
    function f() {
        //...
        //code above is irrelevant

        const relevantCode = "goes here";
        
        //code below is irrelevant
        //...
    }
    ```

3. Commands that are to be run inside of the terminal/command prompt will be formatted like: 

    $ `command to be run`

4. JavaScript variables and their values will be formatted in inline code blocks, e.g: 

    "We will set `variableName` to `variableValue` because ..."
    
5. General actions in the operating system, navigating/clicking user interface elements in a program, and folder names are bolded, like so:

    **File > New File**, **Open in Terminal**, **Folder Name**

    


##Notes and Warning Messages
Throughout this Documentation you will see message blocks that denote important information. Each message block will indicate important information that while not part of the instructions, are important in ensuring you do not run into any obstacles along the way. See below for examples of the message blocks that will be used in this documentation.

!!! Danger "Danger"

    This message block will warn you of dangerous, common mistakes. If you run into an issue, take a look at this message block! 

!!! Warning "Warning"

    This message block will warn you to be aware of certain things for the next instruction. If you find your project not working as expected, take a look at this message block!

!!! Info "Information"

    This message block will mention information that while not necessary for your project, are interesting tidbits that can help expand your understanding. If you're looking for a more in depth understanding, take a look at this message block!

!!! Example "Experiment"

    This message block will mention small experiments/alterations you can try with your project that will help expand your understanding of phaser.js without going in-depth into other topics. If you are looking to experiment with other ways you can use phaser, take a look at this message block!

!!! Success "Success"

    This message block will mention what state your project should be in when you reach it. If you are looking to make sure your project is in the right state, take a look at this message block!
    
!!! Abstract "Code"

    This message block will contain the final code in a given section, and will usually be a collapsible block. You can copy the code inside and paste it into your code editor if you are having trouble getting it all working!
    
## Credits
This documentation is based off of a video created by LogRocket: [How to build pong with Phaser3](https://www.youtube.com/watch?v=itXXERREvx8)

The code we built upon is from the [phaser3-pong](https://github.com/bradydowling/phaser3-pong) repository maintained by Brady Dowling. We modified the code to include the Scoring System and Match Resetting feature that is covered in the [Adding Win Conditions, Match Resetting, and Scoring System](04-final-features.md) instruction set.

[1]: https://phaser.io/
[2]: https://code.visualstudio.com/