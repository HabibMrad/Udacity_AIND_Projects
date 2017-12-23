# Solve Sudoku with AI

## Synopsis

In this project, I will extend the Sudoku-solving agent developed in the classroom lectures to solve _diagonal_ Sudoku puzzles. A diagonal Sudoku puzzle is identical to traditional Sudoku puzzles with the added constraint that the boxes on the two main diagonals of the board must also contain the digits 1-9 in each cell (just like the rows, columns, and 3x3 blocks).


# Naming Conventions
## Rows and Columns

The convention for naming rows and columns is as follows.

    The rows will be labelled by the letters A, B, C, D, E, F, G, H, I.
    The columns will be labelled by the numbers 1, 2, 3, 4, 5, 6, 7, 8, 9. Here we can see the unsolved and solved puzzles with the labels for the rows and columns.
    The 3x3 squares won't be labelled, but in the diagram, they can be seen with alternating colors of grey and white.


![sudoku_board_naming_convention](https://user-images.githubusercontent.com/21977558/34321369-7d2357d0-e833-11e7-906f-16db50095d11.png)




## Boxes, Units and Peers

We have named important elements created by these rows and columns that are relevant to solving a Sudoku:

    The individual squares at the intersection of rows and columns will be called boxes. These boxes will have labels 'A1', 'A2', ..., 'I9'.
    The complete rows, columns, and 3x3 squares, will be called units. Thus, each unit is a set of 9 boxes, and there are 27 units in total.
    For a particular box (such as 'A1'), its peers will be all other boxes that belong to a common unit (namely, those that belong to the same row, column, or 3x3 square).

Let's see an example. In the grids below, the set of highlighted boxes represent units. Each grid shows a different peer of the box at E3.

![sudoku_peers](https://user-images.githubusercontent.com/21977558/34321370-7f3d1740-e833-11e7-8a5a-07520ca52a55.png)



Now, in order to implement an agent,  we will code the  Board in Python . Then, we'll code the necessary functions to solve the Sudoku. We'll record the puzzles in two ways — as a string and as a dictionary.

The string will consist of a concatenation of all the readings of the digits in the rows, taking the rows from top to bottom. If the puzzle is not solved, we can use a . as a placeholder for an empty box.

For example, the unsolved puzzle at the above left will be written as: ..3.2.6..9..3.5..1..18.64....81.29..7.......8..67.82....26.95..8..2.3..9..5.1.3..

And the solved puzzle at the above right, will be recorded as: 483921657967345821251876493548132976729564138136798245372689514814253769695417382

The dictionary was implemented as follows . The keys will be strings corresponding to the boxes — namely, 'A1', 'A2', ..., 'I9'. The values will either be the digit in each box (if there is one) or a '.' (if not).






## Visualization

**Note:** The `pygame` library is required to visualize the solution -- however, the `pygame` module can be troublesome to install and configure. It should be installed by default with the AIND conda environment, but it is not reliable across all operating systems or versions. Please refer to the pygame documentation [here](http://www.pygame.org/download.shtml), or discuss among your peers in the slack group or discussion forum if you need help.

Running `python solution.py` will automatically attempt to visualize the solution, but one must use the provided `assign_value` function (defined in `utils.py`) to track the puzzle solution progress for reconstruction during visuzalization.
