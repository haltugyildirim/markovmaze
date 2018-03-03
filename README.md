# Markov Maze

## Question:
Consider an unbiased random walk in a maze with one entry and one exit.
Find a way to generate a maze and to represent the random walk in it as a
transition matrix. Compute the committor _entry_ $\rightarrow$ _exit_ and the reactive flux.
Represent your results graphically.

## Solution:
![An overview of the solution: (a) is the created maze, (b) is the transition matrix obtained from the maze, (c) is the flux reactor over maze](https://github.com/haltugyildirim/markovmaze/blob/master/images/overview.png)


In order to create a maze, we execute a maze generation algorithm. This algorithm ensures that an $nxn$ maze created as a matrix and all related variables as paths,entry,exit,walls etc. created randomly. The created maze should not contain double walls or paths, which ensures that all the created mazes have an odd number of size lie $3x3$,$17x17$ etc. This will be an important property because it effects how we create our transition matrix.

![Transition Matrix Overview. In (a), you can see one of the simplest possible maze. Transition matrix is the total probability of the states moving from one to another or to itself as represented in matrix, can be seen in the (b). But as you can see going to a wall state or coming from a wall state is meaningless thus, the related columns and rows to this sums to zero. If we exclude these zero transitions, we can achieve our final transition matrix, as seen in (c)](https://github.com/haltugyildirim/markovmaze/blob/master/images/tran_overview.png "How Transition Matrix Works")
