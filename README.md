# Tic Tac Toe Game
### For the Hack Computer as part of the Nand2Tetris Project
**Copyright (c) 2013, John Pazzelli**

This is an implementation of the classic Tic Tac Toe game on the Hack computer as part of the Nand2Tetris project.  The game features a 1 or 2-player mode with a computer-controlled player for single player games.  The computer AI uses a 'minimax' algorithm and has 3 levels of difficulty - the **Impossible mode** is **unbeatable**!

## Screenshots
**Main Menu**
![alt text](https://github.com/pazzelli/Nand2Tetris/blob/master/Screenshots/MainMenu.png)

**Turn Selection**
![alt text](https://github.com/pazzelli/Nand2Tetris/blob/master/Screenshots/TurnSelect.png)

**Draw Game**
![alt text](https://github.com/pazzelli/Nand2Tetris/blob/master/Screenshots/DrawGame.png)

## Code
The main **challenges** in writing the code were finding a way to **support randomness** (required by the computer AI when selecting a move) and implementation of the **minimax gameplay algorithm**.  

Pseudo-randomness was achieved by manually implementing a **Linear Congruential Generator (LCG)** that is seeded with a value that is continuously incremented while the game is waiting on the home screen for the user to begin playing.  This seeding strategy ensures a **different seed will be selected from game-to-game** with high likelihood.  The code for the LCG is found in [LCGRandom.jack](https://github.com/pazzelli/Nand2Tetris/blob/master/Code/LCGRandom.jack).  

The code for the [minimax algorithm](https://en.wikipedia.org/wiki/Minimax) is found in [TicTacToeGame.jack](https://github.com/pazzelli/Nand2Tetris/blob/master/Code/TicTacToeGame.jack) in the functions **calcBestMove()** and **calcBestMoveRecursive()**.  Note that calcBestMove() could simply call calcBestMoveRecursive() for all cases, however in the case where it is the computer's turn to move and there are 8 empty spaces, **it can take up to 50s for the minimax algorithm to compute all 8! = 40,320 possible outcomes** due to the fact that both the virtual machine and all the computer hardware are being **emulated**.  To overcome this, I added some code in calcBestMove() that **randomly selects from a cache of the best moves** chosen by the algorithm in this case and the **AI is now able to calculate and select its best move in under 1s** for all cases, even under emulation.

## Instructions
1. Download the [Nand2Tetris software suite](http://www.nand2tetris.org/software.php) and follow the setup instructions.

2. Download the [TicTacToe.zip](https://github.com/pazzelli/Nand2Tetris/blob/master/TicTacToe.zip) file and unzip to a local directory

3. Open the *Virtual Machine emulator* supplied with the Nand2Tetris software files from step 1 (run the */tools/VMEmulator.bat* (Windows) or */tools/VMEmulator.sh* (Unix/Linux) file)

4. Choose *File --> Load Program* and select the directory from step 2 where the Tic Tac Toe game files are stored

5. Set the *speed* to *Fast* and the *Animate* dropdown to *'No Animation'*

6. Select *Run --> Run* (or press F5) and enjoy!

## Background (taken from www.nand2tetris.org)
The Nand2Tetris project contains all the software tools and project materials necessary to build a general-purpose computer system from the ground up. We also provide a set of lectures designed to support a typical course on the subject.

The materials also support two courses that we now teach in Coursera:

**Nand2Tetris Part I - Hardware**
1. Boolean Functions and Gate Logic
2. Boolean Arithmetic and the ALU
3. Memory
4. Machine Language
5. Computer Architecture
6. Assembler

**Nand2Tetris Part II - Software**
1. Virtual Machine I - Stack Arithmetic
2. Virtual Machine II - Program Control
3. Compiler I - Syntax Analysis
4. Compiler II - Code Generation
5. Operating System
6. High-Level Language and Custom Project
