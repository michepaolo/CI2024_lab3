# Lab 3 - Gem Puzzle

The **Gem Puzzle** (or sliding puzzle) involves rearranging a grid of numbered tiles, with one empty space (represented as 0), into a predefined goal configuration. The player can move tiles into the blank space by sliding them up, down, left, or right. The challenge is to find the shortest sequence of moves to solve the puzzle.

### **Techniques used**

To solve this problem efficiently, I used the **A*** search algorithm
and for the heuristic, I used:
- **Manhattan Distance**: Measures the sum of the distances between actual tiles and their goal positions.
- **Linear Conflict**: Adds penalties when tiles in the same row or column are in the wrong order, improving the heuristic’s accuracy.

---

### **Algorithm**

1. **Initialization**:
   - Start with the initial state, compute the heuristic \( h \), and add it to the priority queue (`open_list`) with \( f(n) = g(n) + h(n) \).
   - Maintain a `closed_set` to track visited states and their costs.

2. **Search Process**:
   - Pop the state with the lowest \( f(n) \) from the `open_list`.
   - If the state matches the goal, reconstruct the solution path and terminate.
   - Otherwise, expand the state by generating all possible moves (up, down, left, right for the blank tile).
   - For each resulting state:
     - Compute \( g \) (cost-so-far) and \( h \) (heuristic).
     - Skip the state if it has been visited with a lower cost.
     - Add valid states to the `open_list`.

3. **Termination**:
   - The algorithm stops when the goal state is found or all possibilities are exhausted (in which case, no solution exists).

4. **Solution Reconstruction**:
   - Once the goal state is reached, backtrack through the parent nodes of each state to generate the sequence of moves.

---

### **Final Considerations**

I managed to solve optimally puzzles of 3x3 and 4x4 tiles, when going to 5x5 puzzles the code sometimes finds a solution in a small amount of time (around 8 mins) sometimes not.

#### Result examples

   - 3x3 -> 26 moves, 352 calls to the heuristic function
   - 4x4 -> 60 moves, 6276 calls to the heuristic function