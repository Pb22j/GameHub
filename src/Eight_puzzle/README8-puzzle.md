# 8-Puzzle - Dual AI Solver

## CSC 361 - Artificial Intelligence Project

An interactive 8-Puzzle solver implementation featuring a graphical user interface (GUI) and a comparison between two fundamental search algorithms.

---

## Overview

This project implements the classic **8-Puzzle** (a $3 \times 3$ sliding puzzle) where the goal is to arrange tiles numbered 1-8 into a specific target state. The application focuses on comparing two informed search strategies:

* **Greedy Best-First Search**
* **A* Search Algorithm**

Users can input a custom puzzle state and visualize how each algorithm navigates the state space to find the solution.

---

## Features

* **Interactive GUI** built with Tkinter using a modern "GameHub" dark theme.
* **Side-by-Side Comparison**: Watch both algorithms solve the same puzzle simultaneously.
* **Step-by-Step Visualization**: Navigate through the solution path using "forward" and "backward" controls.
* **Performance Metrics**: Real-time display of time taken (in seconds) and total steps required for the solution.
* **Custom Input**: Supports any solvable or unsolvable 9-digit string input (e.g., `123456780`).

---

## Structure

```text
8-Puzzle_Solver/
|-- eight_puzzle_gui.py     # Main application (GUI & Logic combined)
|-- README.md               # This file

```

### Key Classes

* `Board`: Manages the $3 \times 3$ grid logic, calculates Manhattan distance, and generates successor states.
* `PriorityQueue`: A custom implementation of a linked-list-based priority queue for managing the search frontier.
* `Solver`: Contains the core logic for the Greedy and A* search implementations.
* `EightPuzzleGUI`: Handles the rendering of tiles, animations, and user interactions.

---

## Installation

### Requirements

* Python >= 3.8
* Tkinter (usually bundled with standard Python installations)

### Setup

1. Clone or download the `eight_puzzle_gui.py` file.
2. Run the application directly:
```bash
python eight_puzzle_gui.py

```



---

## AI Algorithms

### 1. Greedy Best-First Search

Greedy search expands the node that appears to be closest to the goal based solely on the heuristic.

* **Evaluation Function**: $f(n) = h(n)$
* **Heuristic ($h$n$)$**: Manhattan Distance.
* **Behavior**: Fast, but often finds suboptimal (longer) paths as it ignores the cost to reach the current state.

### 2. A* Search

A* search combines the cost to reach a node and the estimated cost to the goal to find the mathematically optimal path.

* **Evaluation Function**: $f(n) = g(n) + h(n)$
* **$g(n)$**: Path cost (depth of the node).
* **$h(n)$**: Manhattan Distance.
* **Behavior**: Guaranteed to find the shortest path (optimal solution) while remaining efficient.

---

## Heuristic Evaluation

The solver utilizes the **Manhattan Distance** heuristic. This is calculated by summing the absolute differences between the current coordinates $(x_1, y_1)$ and the target coordinates $(x_2, y_2)$ for every tile:

$$\text{Distance} = \sum |x_1 - x_2| + |y_1 - y_2|$$

| Component | Description |
| --- | --- |
| **Admissibility** | This heuristic is admissible because it never overestimates the number of moves to the goal. |
| **Successors** | The blank tile (0) can move Up, Down, Left, or Right depending on its current position. |

---

## How to Use

1. **Launch**: Run the script to open the "8-Puzzle Dual Solver" window.
2. **Input**: Enter a 9-digit sequence representing the board (e.g., `013425786` where `0` is the empty space).
3. **Compare**: Click **COMPARE**.
4. **Analyze**:
* Observe the **Time** difference (efficiency).
* Observe the **Steps** count (optimality).
* Use the arrow buttons (◄/►) to step through the moves manually.



---

## References

* Course slides on Informed Search Strategies.
* Artificial Intelligence: A Modern Approach (Russell & Norvig) for A* logic.

---

## Team Member

**Alwaleed Almutairi**

