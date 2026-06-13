N-Queens-Visualizer
# 👑 N-Queens Solver & Visualizer 

A high-performance Java implementation and visualizer for the classic **N-Queens Puzzle** using an optimized recursive backtracking algorithm.

---

## 📝 Project Overview
The N-Queens problem is a famous combinatorial puzzle where the goal is to place $N$ chess queens on an $N \times N$ chessboard such that no two queens threaten each other. This requires that no two queens share the same row, column, or diagonal path.

This project utilizes a **Branch-and-Bound Backtracking** engine to prune invalid paths early, resolving structural placements efficiently compared to brute-force combinations.

### 🧠 Core Algorithm Logic
Instead of checking the entire board matrix linearly at every step ($\mathcal{O}(N^2)$ verification), this engine tracks conflicts in $\mathcal{O}(1)$ time using state arrays:
1. **Vertical Blocks:** Checked via a `colsOccupied` boolean array.
2. **Main Diagonals ($\setminus$):** Verified via `row - col` offsets.
3. **Anti-Diagonals ($\slash$):** Verified via `row + col` equations.

---

## 🎨 Layout Visualizer (N=8 Sample Solution)

Below is an abstract tracking visual of the first valid chessboard state configuration outputted by the algorithm:

   C0  C1  C2  C3  C4  C5  C6  C7
R0 👑  .   .   .   .   .   .   .
R1  .   .   .   .  👑  .   .   .
R2  .   .   .   .   .   .   .  👑
R3  .   .   .   .   .  👑  .   .
R4  .   .  👑  .   .   .   .   .
R5  .   .   .   .   .   .  👑  .
R6  .  👑  .   .   .   .   .   .
R7  .   .   .  👑  .   .   .   .

---

## 🛠️ Code Architecture

The implementation uses low-overhead memory models and native structures:

* **`java.util.*`** components:
  * `List` / `ArrayList`: Manages dynamic arrays to append variable solution dimensions.
  * `Arrays`: Optimized byte-filling operations for visual string matrices.

### Key Snippet: The Backtracking Core
```java
private void backtrack(int row, int[] board) {
    if (row == size) {
        solutions.add(board.clone()); // Valid map found!
        return;
    }
    for (int col = 0; col < size; col++) {
        int d1 = row - col + (size - 1); // Main diagonal hashing
        int d2 = row + col;              // Anti-diagonal hashing

        if (colsOccupied[col] || diag1Occupied[d1] || diag2Occupied[d2]) continue;

        // Commit state
        board[row] = col;
        colsOccupied[col] = diag1Occupied[d1] = diag2Occupied[d2] = true;

        backtrack(row + 1, board); // Recurse

        // Revert state (Backtrack)
        colsOccupied[col] = diag1Occupied[d1] = diag2Occupied[d2] = false;
    }
}
```

---

## 🚀 How to Run the Project

Ensure you have the **Java Development Kit (JDK 8 or higher)** installed on your machine.

### 1. Clone or Save the File
Save the implementation source file locally as `NQueensVisualizer.java`.

### 2. Compile via Terminal
```bash
javac NQueensVisualizer.java
```

### 3. Run the Bytecode
```bash
java NQueensVisualizer
```

---

## 📊 Performance Matrix
As $N$ scales up, the solution search space expands exponentially. The table below represents total unique configurations found across varying grid dimensions:

| Board Dimension ($N$) | Total Unique Solutions Found |
| :---: | :---: |
| **$4 \times 4$** | 2 |
| **$6 \times 6$** | 4 |
| **$8 \times 8$** | 92 |
| **$10 \times 10$** | 724 |
