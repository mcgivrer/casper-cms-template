---
date: 2019-09-02T13:01:00.000Z
title: GameDev : the Game loop basis
tags: gamedev,java,gameloop
author: Frédéric Delorme
---

Browsing the infinit web (or near infinity [^1]), I've spent a lot of timetrygin to find ultimate sresources about game development with java.
My Own research finally driven me to create my own  !
Here is a first post about "How to create a platform game with java ?"

# A Game Loop

This class is the entry point of execution of the this demo game. The main() method will bring somme common arguments to be interpreted with a CliManager and some ArgParser to set some contextual things:

- `width` and `height` of the game window,
- open with in `fullscreen` mode,
- activate tha `debug` level,
- etc...

and the Game class will also instantiate the Stystem dependencies to manage:

- rendering process,
- update process,
- resource management
- input processing,
- etc...

This will depict the main game loop:

```java
while(!exit request) :
    input()  // get key and mouse input
    update() // game mechanism,
    render() // display thing to window/screen
```

This class will also start the link to the OS via Java standard libraries.

```java
class Game extends JPanel implements Runnable{
    public Game(String title, String[] args){
        // do things
    }
    public static void main(String args){
        Game game = new Game("Demo",args);
        game.run();
    }
}
```

The Game has an objects map where all [`GameObject`](./03-gameobject.md "see GameObject documentation") to be managed and rendered by the game are stored.

## The Main Loop

The Main loop in a game ( A.k.A. Game Loop) is the most known part in any game, and this is where all things happened. First listen to the user commands, then computes a lot of things about some game objetcs, and then draw images through some rendering technologies.

Multiple kind of implementation exists, and each of them have pro's & con's. 2 of these must keep you attention:

1. "Fixed Frame based game loop", producing the same number of image per seconds, even if the object are not moving or nothing happened,
2. "Not fixed frame game loop", compute only needed things and wait to the next frame.

In our case and for refreshing CPU, we will use the second one.

> For more details about "Gamelooping", please read the fantastic [article](https://gameprogrammingpatterns.com/game-loop.html) from "Game programming Pattern" about Game Loops !

## Fixed rate gameloop

We are going to implmenta a Fixed rate gameloop with a thoughput of 30 to 60 images/seconds (or fps : Frame Per Seconds).

To achieve that, we will start from the siple mathematic formula:

```
1s = 1000ms
60 frames / s => 1 frame each 16ms.
```

So 16 ms to 
- Capture **input**, 
- Compute game's objects **update** those objects
- and then **Draw** visible game's objects to screen.
- **Wait** some ms if either needed,
- And **loop**.

To be Continued ...

McG.


[^1]: "Two things are infinite: the universe and human stupidity; and I'm not sure about the universe.", [Albert Einstein](https://www.goodreads.com/quotes/942-two-things-are-infinite-the-universe-and-human-stupidity-and).
