# Sudoku Solver - AI Project

## CSC 361 - Artificial Intelligence Project

A Sudoku solver implementation featuring multiple AI algorithms to generate and solve puzzles, complete with real-time visualization.

---

## overview

This project implements the classic **Sudoku** game with a graphical user interface (GUI) and explores different AI techniques to solve the puzzles efficiently:-

* **Naive Backtracking Algorithm**
* **Smart CSP** using the Minimum Remaining Values (MRV) heuristic
* **Simulated Annealing** (Local Search) using a stochastic, error-minimizing approach

Users can generate puzzles of varying difficulties, watch the AI solve them step-by-step, and compare the performance of different search strategies.

---

## features

* **Full-screen GUI** built with Tkinter, featuring a sleek dark theme
* **Puzzle Generation** with five difficulty levels (Easy, Medium, Hard, Expert, Extreme)
* **Real-time Visualization** of the solving process (showing steps, backtracks, and algorithm iterations directly on the grid)
* **Multiple Solvers** allowing you to compare brute-force vs. optimized AI methods
* **Batch Analysis Tool** integrated into the backend to compare average solve times and success rates across algorithms

---

## Structure

```text
Sudoku_AI/
|-- sudoku_gui.py           # GUI implementation (Tkinter) and main entry point
|-- sudoku_game.py          # Core game logic, board state, and AI algorithms
|-- README.md               # This file

```

---

## Installation

### what you need to run the program

* Python >= 3.8
* Tkinter (usually included with standard Python installations)
* NumPy (Required for the Simulated Annealing algorithm)
* `py-sudoku` (Optional, used for advanced puzzle generation. Falls back to an internal generator if not installed)

### Setup

* (Optional) create a virtual environment:
run these commands
```bash
python3 -m venv .venv
source .venv/bin/activate  # on macOS/Linux
# or
.venv\Scripts\activate     # on Windows

```


* Install required dependencies:
```bash
pip install numpy py-sudoku

```



---

## AI algorithms

### 1. Naive Backtracking (`solve_naive_generator`)

A standard brute-force search that attempts to solve the puzzle by picking the very first empty cell it finds and trying numbers 1 through 9. It is exhaustive but can be very slow for complex boards.

### 2. Smart CSP (MRV) (`solve_csp_generator`)

A Constraint Satisfaction Problem (CSP) approach that heavily optimizes the search space.

| Heuristic | Behavior | Advantage |
| --- | --- | --- |
| **MRV** (Minimum Remaining Values) | Always selects the empty cell with the fewest legal moves available. | "Fails fast" by tackling the most constrained cells first, vastly reducing the number of backtracks. |

### 3. Simulated Annealing (`solve_annealing_generator`)

A probabilistic local search algorithm that mimics the cooling process of metals. Instead of filling the board cell-by-cell, it fills all 3x3 blocks completely and randomly. It then iteratively swaps numbers within those blocks to minimize rule violations (errors).

| Feature | Description |
| --- | --- |
| **State** | A fully filled Sudoku board where all 3x3 boxes contain digits 1-9 exactly once. |
| **Cost Function** | Calculates the total number of duplicate digits in all rows and columns. A cost of 0 is a solved board. |
| **Transitions** | Randomly swaps two un-fixed numbers within the same 3x3 block. |
| **Acceptance** | Accepts better states automatically; accepts worse states with a probability that decreases over time (controlled by "temperature"/sigma). |

---

## How the Algorithms Work

### Backtracking Search (Naive & CSP)

Both deterministic algorithms use a recursive depth-first search approach to navigate the game tree:

```text
function BACKTRACK_SEARCH(board):
    if board is completely filled:
        return TRUE
    
    # Naive picks the first empty; CSP picks the MRV cell
    cell = SELECT_UNASSIGNED_VARIABLE(board) 
    
    for each value in 1 to 9:
        if value is safe to place in cell:
            assign value to cell
            
            if BACKTRACK_SEARCH(board):
                return TRUE
                
            remove value from cell (backtrack)
            
    return FALSE

```

### Simulated Annealing Optimization

The Simulated Annealing agent works completely differently:

1. **Initialize**: Fill the board so every 3x3 block is valid (ignoring rows/columns).
2. **Evaluate**: Calculate initial "errors" (duplicates in rows/columns) to set the starting temperature ($\sigma$).
3. **Iterate**:
* Propose a state by swapping two non-fixed cells in a random 3x3 block.
* Calculate the change in cost ($\Delta E$).
* If the new state has fewer errors, keep it.
* If it has *more* errors, keep it with probability $P = e^{-\Delta E / \sigma}$.


4. **Cool**: Slowly decrease $\sigma$ (e.g., multiply by 0.99) and repeat until errors = 0.

---

## Running the Game

To launch the Sudoku GUI and watch the AI in action:

run this command from the project root:

```bash
python3 sudoku_gui.py

```

This will open the full-screen interface where you can:

1. Select a difficulty from the dropdown and click **Generate**.
2. Select an algorithm (Smart CSP, Naive, or Simulated Annealing).
3. Click **Start Solving** to watch the visualization and track the metrics.

---

## references

* I relied heavily on the course slides and searching the internet for algorithmic heuristics (like MRV and Simulated Annealing cooling schedules).

---

## team member worked in this game:

**Mohammed Alwanis**
