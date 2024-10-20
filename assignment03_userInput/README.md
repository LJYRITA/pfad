Minesweeper Game
This is a simple Minesweeper game implemented using Python and Pygame. The game allows players to choose between three difficulty levels: Easy, Medium, and Hard. The objective is to reveal all the cells that do not contain mines.

Requirements
Python 3.x
Pygame library

How to Play
Run the script:
python assignment03_Minesweeper.py

Choose a difficulty level by clicking on one of the buttons: Easy, Medium, or Hard.
Click on the cells to reveal them.
The game ends when you reveal all non-mine cells (win) or click on a mine (lose).
After the game ends, click the “Again” button to restart the game.

Code Explanation
Initialization and Setup: The game initializes Pygame, sets up the screen, and defines colors and difficulty levels.
Difficulty Selection Screen: Displays buttons for selecting the difficulty level.
Grid Creation and Mine Placement: Creates the game grid and randomly places mines.
Number Calculation: Calculates the number of mines surrounding each cell.
Grid Display: Draws the grid on the screen, showing revealed cells, numbers, and flags.
Win Check: Checks if the player has won by revealing all non-mine cells.
End Screen: Displays a message when the game ends and provides a button to restart the game.
Main Game Loop: Handles user input, updates the game state, and redraws the screen.

I hope this README is helpful to you!