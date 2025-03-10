# Overview of Express User Documentation

Welcome to our documentation for re-creating the famous game Pong. This documentation will guide you through creating a basic [Phaser](https://phaser.io/) project.

The goal of this documentation is to provide you with enough information to re-create pong using the Phaser game engine. We will also provide an understanding of what each step does for the project.

These are the topics of this document:

1. [Setting up a Basic Phaser Project](./docs/01-setting-up.md)
2. [Pong: Creating and Configuring Our Game Instance ](./docs/02-configuring-creating-game-instance.md)
3. [Pong: Creating Our First Game Objects and Player Characters](./docs/03-creating-game-objects.md)
4. [Pong: Adding Win Conditions, Match Resetting, and Scoring System](./docs/04-final-features.md)


## How We Collaborated Together

We communicated over discord and in person.

We used Git and GitHub to collaborate on the documentation. Originally we created a new page per section but quickly realized it was easier to have one person work on the main branch and the other on a separate one to ease merge conflicts.

## How We Created Our Guide

Our guide was created by learning from a pre-existing youtube video that [teaches the basics of Phaser 3](https://www.youtube.com/watch?v=itXXERREvx8&t=1662s&pp=ygUNcG9uZyB0dXRvcmlhbA%3D%3D). We helped each other with misunderstandings regarding the Phaser framework and integrated data insights collected from our in-person beta test.

### Using Markdown

Both of our group members were familiar with using Markdown to create notes. Working with Mkdocs Material provided a number of new functionalities that we had to learn to optimize our projects readability and flow.

### Using VS Code

Our group used Visual Studio Code (VS Code) to edit and create our markdown files. To view them, we served the files locally and viewed them in the browser.

### Using a Style Guide

We used codeblocks to represent code. We also used inline code annotations to represent variables and file names. Inside code blocks, we used both highlighting and inline comments to further enhance readability and concreteness for our users.

We used admonitions frequently for warnings, additional information, experiments and dangerous errors.

#### Readability

We aimed our document at users who are new to Phaser but have a fundamental grasp of Javascript and Object Orientated Programming (OOP). Our instructions were created with the intent to support the learning of the individual and to provide them with clear use cases for Phaser methods.

We ensured that every instruction set had pre-requisites to notify a user that the previous step must be completed and an overview that gave a player a summary of the topics covered in this instruction set. At the end of each set, we included a conclusion to summarize what the reader would have accomplished from following them.

We used MkDocs' admonitions to highlight any information we wanted to stand out to the reader.


#### Chunking

When learning a new framework, it is hard not to be intimidated. As such, we separated each set of instructions using subheadings to indicate what was being worked on in each portion. By doing so, we hope to not overwhelm the reader, and allow them to gradually follow through step-by-step.

#### Tone

This documentation is intended for the following users:

- Intermediate developers looking to learn the Phaser Framework

This allowed us to focus on writing documentation specific to the Phaser Framework without having to explain medium-complexity javascript topics such as the `this` keyword.

## Conclusion

By writing this documentation, we had a chance to learn the Phaser framework for ourselves, understand it's core concepts, and share it in an easy-to-consume manner. Doing so allowed us to practice writing clear and complete documentation for topics that we are not extremely knowledgeable on.

Thank you for reading our documentation for a basic Phaser App! Enjoy! :tada:


This document was built on: [Material for MkDocs](https://github.com/squidfunk/mkdocs-material)
