# advent_of_code2020
Advent of Code 2020 Solutions in Python!
Author: Ben Greene
December 2020

## Goals:
- Refresh python skills
- Keep python as simple as possible
- Scalable solutions that would work with large inputs

## Tips & Tricks to remember:

- Debugging output is controlled by a `verbose` flag, set to `0/No debug` as a default. Values of `verbose=1` and `verbose=2` are accepted with the higher value increasing verbosity.

- **Day 1**:
  - Many possibilities, but the solution used was simple loops. Input was small so no need to do anything special.
- **Day 2**:
  - Used dictionaries
- **Day 3**:
  - Simple indexing in a list, used the modulo `%` operator, but not much else.
- **Day 4**:
  - More dictionary use. 
  - Part2: used modular functions to make an easy to read and use program.
- **Day 5**: 
  - The hint was "binary partitioning". This problem is essentially converting a string into two binary numbers' base 10 equivalent. This is done via python's `int(str,base=2)`
  - Translating a string with python: ```python's str.translate(str.maketrans('old_chars','new_chars'))```, **ref[1-2]**.
    - See **ref[7]** for removing punctuation from a string
- **Day 6**:
  - Part1: we want unique characters out of each group. This is done via building a string and then collapsing it.
  - Unique characters in a list like `''.join(set('aaabcabccd'))`, **ref[3]**.
  - Part2: we add the number of persons in each group as the only additional information we need. 
  - Ultimately unused, but interesting read is "best way to count char occurences in string" in **ref[4]**
- **Day 7**
  - Part1: This is a use-case for an implementation via **Graphs**. Generate a *Directed Graph* represented by an *adjcency list* (list of linked lists) where each color is a node and all sub-nodes are colors that can be stored in it. 
  	1. Reverse the graph
  	2. Run DFS on the reversed graph starting from "Shiny Gold" node and count number of visited nodes, this is the answer. Note, either BFS **ref[5]** or DFS **ref[6]** would work.
    3. Complexity will be `O(|V|+|E|)`
- **Day 8**
  - Part2; A scalable solution for Day 8 Part 2 can be implemented via a **Graph**, with each instruction being a "node", and edges representing program flow. Because of the problem formation, it is a *directed graph*, where each node can have multiple edges in, but only 1 edge out. With this knowledge, a solution for Part 2 can be found as such:
    1. Find all "nop" and "jmp" instructions in the loop. We know the corrupted line must be one of these because the problem stated only a single instruction is faulty.
    2. Build a reverse graph, and do a DFS search starting from the "END" to get a list of all operations that will allow the program to run to completion.
    3. For each `jmp` and `nop` instruction from step 1, check if swapping its type will make the next instruction be one in the set of instructions discovered in step 2. 
    4. Correct this line and run the program to completion to get final accumulator value.
- **Day 9**
  - Part1: is an application of the Twosum Algorithm, a special case of the Subset Sum problem that can be solved in linear time (**ref[8]**). The key is that the integer must be the sum of 2 (and only 2) of the previous 25 numbers, and that the 2 numbers will be different and positive.
  - Part2 was solved with a sliding window, maintained by 2 'pointers'. This is only possible because there are no negative numbers
- **Day 10**
  - Part1: Looks like a simplified version of the *Hamiltonian Path* problem (**ref[9]**). Based on the provided assumptions, the next adapter needs to always be the one closest in value to the current adapter (because we can't go down). We can do this via a simple sorted list of the adapter values.
  - Part2: The best way to solve is as a Graph problem. Adapters are represented as nodes, and there are directed edges to all adapters with values 1, 2, or 3 higher. The solution is to find all paths from the first node of "0" to last node 3 higher than the greatest adapter. 
    - The solution uses a count for each node. The count is of unique paths to goal, and is a summation of the counts for all of the node's children neighbors. The count is initialized to "1" for the goal node, and "0" for all other nodes.
    - Given the above, a DFS search solves the problem. The solution is the final count for the starting node.
    - This only works because the graph is a Directed Acyclic Graph (DAG).
- **Day 11**
  - Part1: This reminds me of *Conway's Game of Life* (**ref[10]**) with it's simple rules and evolving grid. Solved via a modular implementation. Converting the cells from characters to integers simplified implementation {0:Empty cell, 1:Occupied Cell, -1:Ground/Static cell}.
  - Part2: Because of the modular construction, only update needed was to the `update_cell()` function
- **Day 12**
  - Part1: Use a class to represent a ship and apply simple actions. See **ref[11]** on Manhatten distance.
  - Part2: Knowledge of cartesian coordinates and rotation of a point around the origin are the key concepts (**ref[12]**).

## References
[1] https://stackoverflow.com/questions/41535571/how-to-explain-the-str-maketrans-function-in-python-3-6/41536036  
[2] https://discuss.python.org/t/str-replace-of-a-set-of-characters/2758/3  
[3] https://stackoverflow.com/questions/13902805/list-of-all-unique-characters-in-a-string  
[4] https://stackoverflow.com/questions/613183/how-do-i-sort-a-dictionary-by-value  
[5] https://en.wikipedia.org/wiki/Breadth-first_search  
[6] https://en.wikipedia.org/wiki/Depth-first_search  
[7] https://stackoverflow.com/questions/265960/best-way-to-strip-punctuation-from-a-string  
[8] https://en.wikipedia.org/wiki/Subset_sum_problem  
[9] https://en.wikipedia.org/wiki/Hamiltonian_path  
[10] https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life  
[11] https://en.wikipedia.org/wiki/Taxicab_geometry  
[12] https://en.wikipedia.org/wiki/Cartesian_coordinate_system  
