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




# Strategies used :-


## Strategy 1: Elimination


If a box has a value assigned, then none of the peers of this box can have this value.

Now that we know how to eliminate values, we can take one pass, go over every box that has a value, and eliminate the values that can't appear on the box, based on its peers. Once we do so, the board looks like this (for clarity, we've highlighted the original filled-in boxes in bold lettering):

(Notice that if we take a second pass through the puzzle, we can gain even more information, but this is not necessary for now.)


![sudoku_elimination](https://user-images.githubusercontent.com/21977558/34321544-861df954-e837-11e7-921e-b00ae9c54321.png)



As of now, we are recording the puzzles in dictionary form, where the keys are the boxes ('A1', 'A2', ... , 'I9') and the values are either the value for each box (if a value exists) or '.' (if the box has no value assigned yet). What we really want is for each value to represent all the available values for that box. For example, the box in the second row and fifth column above will have key 'B5' and value '47' (because 4 and 7 are the only possible values for it). The starting value for every empty box will thus be '123456789'.


## Strategy 2: Only Choice

If there is only one box in a unit which would allow a certain digit, then that box must be assigned that digit.


![sudoku_only_choice](https://user-images.githubusercontent.com/21977558/34321565-25c4698e-e838-11e7-93c2-f3b556e0da3e.png)



We will now  use the techniques of eliminate and only_choice to write the function reduce_puzzle, which receives as input an unsolved puzzle and applies our two constraints repeatedly in an attempt to solve it.

## Strategy 3: Search

Pick a box with a minimal number of possible values. Try to solve each of the puzzles obtained by choosing each of these values, recursively.

![sudoku_search](https://user-images.githubusercontent.com/21977558/34321611-174cde44-e839-11e7-9255-3a3845d8b83b.png)


## Strategy 4 : Naked Twins

The naked twins technique is the following. Consider the following puzzle, and look at the two highlighted boxes, 'F3' and 'I3'.



![sudoku_naked-twins_1](https://user-images.githubusercontent.com/21977558/34321628-b06a2e06-e839-11e7-80bc-a8126b0fe8ea.png)




As we can see, both belong to the same column, and both permit the values of 2 and 3. Now, we don't know which one has a 2 and which one has a 3, but we know one thing for sure — the values 2 and 3 are locked in those two boxes, so no other box in their same unit (the third column) can contain the values 2 or 3.

Thus, we go over all the boxes in their same unit, and remove the values 2 and 3 from their possible values.


![sudoku_naked-twins-2](https://user-images.githubusercontent.com/21977558/34321630-c845869c-e839-11e7-9a13-97502ab410f7.png)


As you can see, we've removed the values 2 and 3 from the boxes 'D3' and 'E3'. This is the naked twins technique. In this project, you'll write a function that implements this technique.






## Strategy 4 : Diagonal Sudoku

A diagonal sudoku is like a regular sudoku, except that among the two main diagonals, the numbers 1 to 9 should all appear exactly once. In this project, you'll modify the functions we've written in the lecture (or you can write your own!) in order to solve every diagonal sudoku.



![diagonal-sudoku](https://user-images.githubusercontent.com/21977558/34321637-fa94a7ae-e839-11e7-9e8a-fde2a65243bd.png)




## Visualization

**Note:** The `pygame` library is required to visualize the solution -- however, the `pygame` module can be troublesome to install and configure. It should be installed by default with the AIND conda environment, but it is not reliable across all operating systems or versions. Please refer to the pygame documentation [here](http://www.pygame.org/download.shtml), or discuss among your peers in the slack group or discussion forum if you need help.

Running `python solution.py` will automatically attempt to visualize the solution, but one must use the provided `assign_value` function (defined in `utils.py`) to track the puzzle solution progress for reconstruction during visuzalization.
