# Solve Sudoku with AI

## Synopsis

In this project, I will extend the Sudoku-solving agent developed in the classroom lectures to solve _diagonal_ Sudoku puzzles. A diagonal Sudoku puzzle is identical to traditional Sudoku puzzles with the added constraint that the boxes on the two main diagonals of the board must also contain the digits 1-9 in each cell (just like the rows, columns, and 3x3 blocks).




## Visualization

**Note:** The `pygame` library is required to visualize the solution -- however, the `pygame` module can be troublesome to install and configure. It should be installed by default with the AIND conda environment, but it is not reliable across all operating systems or versions. Please refer to the pygame documentation [here](http://www.pygame.org/download.shtml), or discuss among your peers in the slack group or discussion forum if you need help.

Running `python solution.py` will automatically attempt to visualize the solution, but one must use the provided `assign_value` function (defined in `utils.py`) to track the puzzle solution progress for reconstruction during visuzalization.
