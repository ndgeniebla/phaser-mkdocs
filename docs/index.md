#Introduction

Hello and Welcome to PhaserFirst! By following this documentation, you will learn how to create a small [Phaser][1] project and kick off your game developement journey. Throughout the document we will guide you step by step towards creating a simple version of the classic video game Pong with the goal of understanding the fundamentals of what makes up a Phaser project.
> **[Phaser.js][1]** (more commonly known as Phaser) is a free open-source framework for developing web based 2D games with a focus on compact builds and flexible integration. Phaser provides the user with numerous time-tested tools to build the game you want, quickly and efficiently. 

##Intended Users

This documentation is intended for:

- intermediate developers who want to learn the basics of the [Phaser][1] framework

##Prerequisite Knowledge

This document assumes you know the following:

- Experience using Javascript to build web based applications
- Using the terminal to navigate projects and execute commands
- Comfortable using a code editor (like [VScode][2])
- Experience using [Node.js][3] to build Javascript Applications
- Familiarity using NPM (node package manager) to install node.js packages or modules

> For our tutorial we will be using [VScode][2]. Be aware that while using another code editor is possible, instructions and methods may not work for them. If you choose not to use [VScode][2], this tutorial may not work for you.

##Software Requirements

- Node Package Manager v11.x or later
- [Visual Studio Code][2]

##Procedures Overview

1. Setting Up Your Project 
2. Creating Our Game Instance 
3. Building Our First Scene, Game Object and Enemy 
4. Keeping Score and A Final Scene 

##Typographical Conventions

1. File and Package names will be formatted like: `filefilefile.js`
2. In code blocks if you see `//...` this means there is code in that location not currently relevant to this step


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



[1]: https://phaser.io/
[2]: https://code.visualstudio.com/
[3]: https://nodejs.org/en