---
layout: post
title:  "Don't get hit"
date:   2021-05-05 12:19:54 -0300
categories: jekyll update
---
## About this project
This is my first project ever. When I finished doing the *full python course*, I wanted to get into some real project. I had no experience at all, so I started from where I thought it would be easier, a game. I looked at some tutorials on youtube and found out that creating a simple game of a spaceship and asteroids, was perhaps the best way to start. 

As it is my first project ever, I didn't know a lot of stuff I know nowdays, like to name the main script `main.py`, to use more and better *classes*, etc... Despite all these things I can correct now, I decided to keep the project as it was, this means not changing anything the way I would do things today. The reason for this is beacause I belive the project has more value as it is to show the progress, and to help others understand how the code of a real beginner is.

## The Main Menu
![image](/Images/main_menu_nave_espacial.png){: width="500" }

As my first project, for some reason, the idea of just making a game with no menu, made no sense. So I learnt different things while triyng to accomplish what I wanted. First of all, I learnt how to do a working button from scratch, and how to manage the collision of the hitbox of it with my mouse. Some programs will just put a button on screen with one click, but pygame doesn´t, so it is what it is...

The second thing I learnt here, is to manage more than one window, this means, creating a window, closing it and creating another one. In this case there were 3 windows:
- The Main Menu
- The Game window
- The Game Over window

## The Play Game window
![image](/Images/game_nave_espacial.png){: width="500" }

The Game it self doesn't need much explanations, but there is one mechanic that perhaps does, and it was this particular  mechanic, that at the moment, took me several days to figure it out (I didn't watch any videos of how to do it because I wanted to imagine it by myself).
The thing I'm talking about is the *timer*. I needed a way to tell the asteroids when to appear, so I build a timer, using the module `time` from Python. The challenge was not this, but the increasing difficulty over time. At the end I managed to solve it, it doesn't work perfectly, but at the moment I was really proud.

There is also another mechanic that didn't take me that long, but was something out of the grid for me. *How to make the asteroids randomly generate everywhere except from the main screen, so the spaceship has time to react?* 
I managed to solve this problem too, If you want to see the solution, you can go to [My Github](https://github.com/Luulas-bot/Don-t-game-hit-Game-/tree/main). The main and only script is named `nave_espacial.py`.

## The game over window
![image](/Images/game_over_nave_espacial.png){: width="500" }

This window was not very difficult to do at the time. It is a simple *Game Over* screen that takes you back to the main menu.

## Wanna try it out yourself?

If you want to try the game by yourself, you can go to [My Github](https://github.com/Luulas-bot/Don-t-game-hit-Game-/tree/main) where you will find the repository and all of the files you need. There is also a `readme.md` file with some instructions to download it, install it and run it.
