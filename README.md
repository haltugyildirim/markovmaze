# Markov Maze

# The Maze // Final Project of [Computer Tutorial in Markov Modeling, WS17/18](http://www.mi.fu-berlin.de/w/CompMolBio/EmmaSeminar17_18)
by Mustafa Emre Coltu, H. Altuğ Yıldırım, Kenichi Maeda, Jakob Roßbach

Another version of the same project can be found in [here](https://github.com/JlR1/markovmaze) by Jakob.

Documentation related to PyEmma project can be found in [here](http://emma-project.org/latest/).

## Question:
Consider an unbiased random walk in a maze with one entry and one exit.
Find a way to generate a maze and to represent the random walk in it as a
transition matrix. Compute the committor _entry_ $\rightarrow$ _exit_ and the reactive flux.
Represent your results graphically.

## Solution:
![](https://github.com/haltugyildirim/markovmaze/blob/master/images/overview.png "Maze Transition Matrix Overview")
An overview of the solution: (a) is the created maze, (b) is the transition matrix obtained from the maze, (c) is the flux reactor over maze.


In order to create a maze, we execute a maze generation algorithm. This algorithm ensures that an $nxn$ maze created as a matrix and all related variables as paths, entry, exit, walls etc. created randomly. The created maze should not contain double walls or paths, which ensures that all the created mazes have an odd number of size lie $3x3$,$17x17$ etc. This will be an important property because it effects how we create our transition matrix. An example to this rule can be seen in the figure below. White parts of maze are paths and black/gray parts are walls.

![](https://github.com/haltugyildirim/markovmaze/blob/master/images/forbidden_maze.png "Forbidden Maze")
Forbidden formations in the maze creation.

In order to create the transition matrix, we first create a matrix of $n^2xn^2$ with all states(elements) as one and then exclude the ones that are not possible.

![](https://github.com/haltugyildirim/markovmaze/blob/master/images/tran_overview.png "How Transition Matrix Works")
Transition Matrix Overview. In (a), you can see one of the simplest possible maze. Transition matrix is the total probability of the states moving from one to another or to itself as represented in matrix, can be seen in the (b). But as you can see going to a wall state or coming from a wall state is meaningless thus, the related columns and rows to this sums to zero. If we exclude these zero transitions, we can achieve our final transition matrix, as seen in (c).


We first exclude the wall-to-wall and wall-to-path, path-to-wall states as seen in the figure. This creates empty rows and columns which will be deleted afterwards. For example, one can easily see that from state 12 to 25 or from state 52 to itself a transition is not possible.

![](https://github.com/haltugyildirim/markovmaze/blob/master/images/wall-to-wall.png "Wall-to-wall")
Wall related exception rules

After that, we exclude all the possible diagonal related movements. In order to that, we use the fact that our mazes are odd numbered and a transition from odd to odd or even to even numbered state is not possible. This can clearly be seen from figure below

![](https://github.com/haltugyildirim/markovmaze/blob/master/images/diag-to-diag.png "diagonal rules")
From state 3 to 15 or 108 to 118 is not possible, but an even to odd or vice versa transition is possible.

But this does not exclude jumps, like from state 3 to 18. In order to introduce neighboring rules, we use another numerical cheat that only possible transitions are related to each other as either with a $\pm1$ difference or $\pm n$ difference.

![](https://github.com/haltugyildirim/markovmaze/blob/master/images/neighbors.png "neighbor rules")
Transitions can only made between numerically related states as either a difference of 1 or n, For example between the states 14,13 and 15 the absolute value of difference is 1 and between states 50, 61 and 72, the absolute value of difference is 11 as relates to 11x11 maze.

An overview of the creation of transition matrix can be seen in the figure below.

![](https://github.com/haltugyildirim/markovmaze/blob/master/images/transition.png "transition matrix")
From the images as shown. (a.1) is the matrix related to horizontal neighbors. (a.2) is vertical neighbors. (a.3) is the all self moving states including the walls. (b) is the combined and normalized matrix of the previous three. (c) is the smaller matrix, which all the related wall states excluded. (d) is the largest connected part of the matrix, which is smaller than the (c) thus reduce the computational time for further calculations(?)
