
# a-graceful-Sudoku-player

A Sudoku player that is geared towards gracefully solving difficult Sudokus. Nearly all Sudoku players in the world are clunky. Mine is not. Anyone who can solve difficult Sudokus knows that the notes are everything, and they also know that generating the notes by hand is extremely tedious, so my player does the following...
* auto generates notes at start and when erasing, avoiding obvious contradictions
* auto removes notes when placing numbers
* does not let you place a number if the notes do not allow it
* does not let you place a note if it creates an obvious contradiction with numbers
* uses "number first" input. To place a number, select the number *then* place it
* nicely highlights notes and numbers of the selected number

Depending on your device...
* Instead of turning notes-editing on, you can always right click to edit notes. On a mobile-device, this is touch-and-hold. When I play, I never turn notes-editing on (I right click).
* Less useful, but, with a keyboard, you can also use number keys to select numbers.

When loading a puzzle, whitespace is ignored. Anything else not 1-9 is considered a blank (I prefer using *0*s). The number of solutions is not checked because this is a player, not a solver. However, if any of the clues have obvious contradictions (more than one of the same number in same row, column, or block), this is detected.

The code was written to be as simple as possible, so feel free to edit the code if you want to (perhaps easily) change any of the above!

If you are on a mobile device and cannot easily download and display the HTML file, here is a link to a live version: [https://www.bradleyknockel.com/sudokuPlayer.html](https://www.bradleyknockel.com/sudokuPlayer.html)



# another great Sudoku player

I was inspired by the following great Sudoku app...  
[https://play.google.com/store/apps/details?id=sudoku.puzzle.free.game.brain](https://play.google.com/store/apps/details?id=sudoku.puzzle.free.game.brain) for Android  
[https://apps.apple.com/us/app/sudoku-puzzle-brain-games/id1492978794](https://apps.apple.com/us/app/sudoku-puzzle-brain-games/id1492978794) for iOS

Unlike this app, my player does not require watching ads and lets you load your own puzzle, and mine does not have the constant risk of accidentally leaving "number first" mode. I cannot alert the player when a number is placed incorrectly. This could be a pro or a con depending on your preference. Mine is a player, not a solver, so I don't know the solution. I do alert the player when a number that disagrees with the notes is placed.

Pros of their app over mine...
* Theirs looks nicer on mobile devices, partly due to nice screen autofill and no risk of webpage scrolling. Though, being only an app, their computer compatibility is horrible.
* Theirs can give you a hint that includes the reason why the move can be made, though their hints are too much. Just tell me the TYPE of strategy to look for rather than the exact where and why of it. Note that all of their puzzles can be solved using only a small subset of strategies, and watching ads is required to get hints. My next goal would be to provide a button that would list which strategies can be currently done.



# my thoughts

This is the first time in my life I have focused on making a GUI. The experience was, as expected, less mathematical and more organizational, which felt tedious at times (especially CSS), but directly seeing the graphical results was rewarding! The code took more time than I expected (4 days), so I now have more empathy for my high school computer-science students who often make GUIs for their projects.

Normally, I would be more interested in *generating* (and solving) Sudokus with code, but this has been thoroughly accomplished! The code, Tdoku, is at [https://github.com/t-dillon/tdoku](https://github.com/t-dillon/tdoku).
Using their code, you can generate a random Sudoku by running
```
./BUILD.sh
build/generate -s0 -p0 -n1 -l1
```
On Windows with Cygwin64, the compile command is *bash BUILD.sh*. Better yet, edit their generate.cc to suit your needs! For example, I also have it print the solutions via TdokuSolverDpllTriadSimd(), and I allow it to generate batches of random Sudokus that are not evolved from previously generated ones. Even better, I downloaded just the files I needed for compiling generate.cc (they were all in the *src* folder), then I had to tinker with some of the *\#include* lines in generate.cc and solver_dpll_triad_simd.cc. I could then compile it by doing
```
g++ -std=c++11 -O3 generate.cc
```
In generate.cc, I changed
```
#include "../include/tdoku.h"
#include "util.h"
```
to
```
#include "util.cc"
#include "solver_dpll_triad_simd.cc"
```
In solver_dpll_triad_simd.cc, I commented out
```
#include "util.h"
```

The goal of my Sudoku player is to make solving difficult Sudokus less tedious. However, the advanced strategies themselves become tedious to search for manually. What is now interesting to me is trying to find the *fastest* way of solving difficult Sudokus. Towards this goal, if I were to ever do more coding for Sudokus, I would try to do analyses such as this: [https://www.sudokuwiki.org/The_Relative_Incidence_of_Sudoku_Strategies](https://www.sudokuwiki.org/The_Relative_Incidence_of_Sudoku_Strategies). Even the amazing Tdoku code above does not evaluate the difficulty of Sudokus based on using these strategies, so a strategy-based solver could be added to the Tdoku code. Making this strategy-based code would help me allow my Sudoku player provide strategy hints to the user.



