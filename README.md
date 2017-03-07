# n-puzzle
Overview-------------------------
Solver for the n-puzzle game (visit http://mypuzzle.org/sliding to see the actual game) using uninformed search.

An instance of the n-puzzle game consists of a board holding n^2 − 1 distinct movable tiles, plus an empty space. The tiles are numbers from the set {1, …, n^2 − 1}. For any such board, the empty space may be legally swapped with any tile horizontally or vertically adjacent to it. The blank space is represented with the number 0.

Given an initial state of the board, the combinatorial search problem is to find a sequence of moves that transitions this state to the goal state; that is, the configuration with all tiles arranged in ascending order ⟨0, 1, …, n^2 − 1⟩.

The blank space may be swapped with a component in one of the four directions {‘Up’, ‘Down’, ‘Left’, ‘Right’}, one move at a time. The cost of moving from one configuration of the board to another is the same and equal to one. Thus, the total cost of path is equal to the number of moves made from the initial state to the goal state. Where an arbitrary choice must be made, the program visit child nodes in the "UDLR" order; that is, [‘Up’, ‘Down’, ‘Left’, ‘Right’] in that exact order.

Execution-----------------------
The program is designed to be  executed as follows:

$ python driver.py <method> <board>

The method argument is bfs for Breath First Search and dfs for Depth First Search. The board argument will be a comma-separated list of integers containing no spaces. For example, to use the bread-first search strategy to solve the input board given by the starting configuration {0,8,7,6,5,4,3,2,1}, the program will be executed like so (with no spaces between commas):

$ python driver.py bfs 0,8,7,6,5,4,3,2,1

Output-------------------------

When executed, the program will create/write to a file called output.txt, containing the following statistics:

path_to_goal: the sequence of moves taken to reach the goal
cost_of_path: the number of moves taken to reach the goal
nodes_expanded: the number of nodes that have been expanded
fringe_size: the size of the frontier set when the goal node is found
max_fringe_size: the maximum size of the frontier set in the lifetime of the algorithm
search_depth: the depth within the search tree when the goal node is found
max_search_depth:  the maximum depth of the search tree in the lifetime of the algorithm
running_time: the total running time of the search instance, reported in seconds
max_ram_usage: the maximum RAM usage in the lifetime of the process in megabytes
