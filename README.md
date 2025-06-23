
## ABOUT THE PROJECT:

- The objective of this project is to construct a polygonal containment field that captures the maximum value of crystals on a 2D grid while minimizing the inclusion of void mines.

- This project leverages prefix sums, factorization, greedy and sorting strategies to identify optimal divisions. The system is designed to maximize the sum of values enclosed in the polygon.

- Our solution aims to provide a near-optimal answer in a reasonable time, balancing performance with accuracy.

---

## 🚀 How to Run

### 🔧 Prerequisites
- A working C++ compiler (e.g., `g++`)
- C++11 or higher
- Sufficient memory (handles vectors of size up to 10000 × 10000)

### 🛠️ Compilation

```bash
g++ -std=c++11 -o program optimization.cpp
```

### ▶️ Running the Program

```bash
./program
```

- The program automatically reads from 10 input files (`input00.txt` to `input09.txt`) in the same directory.
- To customize the number of iterations or input file format, modify the loop inside the `main()` function.
- Accuracy and result summary are displayed in the terminal.

---

## 📥 Input File Format

Each file should follow the format:

```
N
x1 y1 c1
x2 y2 c2
...
xN yN cN
M
x1 y1 c1
x2 y2 c2
...
xM yM cM
```

- `N`: Number of positive crystals  
- Each of the next `N` lines contains coordinates and the value to **add** at `(x, y)`  
- `M`: Number of negative crystals  
- Each of the next `M` lines contains coordinates and the value to **subtract** at `(x, y)`

⚠️ Input files must be named exactly as: `input00.txt`, `input01.txt`, ..., `input09.txt`.

---
## 🎯 Optimization Objective

The goal is to:
- Segment a 2D grid such that the **sum of enclosed values** within a limited number of rectangles is **maximized**.
- Limit the number of rectangles to around 200 because the final polygonal output must not exceed **1000 vertices**.
- Output a set of **edges** defining the best polygonal.

## 🔍 Overview of Optimization Strategy

The solution uses a **factor-based rectangular partitioning method**:

### 📐 Grid Factorization
- All divisors of 10,000 are computed.
- These factors define possible horizontal and vertical cuts to form rectangular segments.

### 📊 Enclosure and Merging
- Each cell in the grid may have a positive or negative value.
- In Method 1: Kadane's algorithm is applied row-wise( and column-wise) to find maximum valued subarray.
- In Method 2: Rectangles with adjacent positive-value cells are merged row-wise( and column-wise) to reduce fragmentation.
- Both methods are separately applied row-wise and column-wise to increase accuracy.
- A prefix sum matrix is used to compute enclosed values in constant time.

### 🧮 Selection and Sorting
- All valid rectangles are sorted by their value sum.
- The top 0–200 positive rectangles are selected to form the best-case approximation of high-density regions.

### 🧾 Polygon Construction

To convert selected rectangles into a clean polygon with minimal vertices:

- All horizontal rectangles in the same row are **merged** and connected via a thin **"pipe"** of width 0.5 units.
- This 0.5-width connector ensures **no vertical overlap** between disjoint rectangles, keeping the edge structure simple and vertex count minimal.
- Once all rectangles at the same vertical level are connected, a **single vertical line** is added at the beginning (along the Y-axis) to enclose the region.
- The result is a closed polygon representing all selected rectangles using a **bounded number of vertices** (≤1000).
- Final output is a list of **edges**: each defined by two coordinate pairs, suitable for rendering or further analysis.


---

## ⚙️ Potential Enhancements

In future versions, the following methods may be integrated for more flexible optimization:

- **Ray Projection Method**  
  Check if points lie inside a polygon, enabling more arbitrary region definitions.

- **Linear Programming-Based Polygon Formation**  
  Use LP to optimize over (x, y) vertex placements while constraining axis-aligned edges.

---

## 🧪 Output

- Number of polygonal edges printed to stdout
- Accuracy reported as:
  ```
  Accuracy: <percentage>
  ```
- Final output includes:
  - Coordinates of rectangular boundaries
  - Accuracy of each test case
  - Average accuracy across all test cases

---

## 💡 Troubleshooting

- **File Not Found:** Ensure `input00.txt` to `input09.txt` exist in the code directory.
- **Permission Denied:** Check directory permissions for output files.
- **Memory Errors:** The program allocates large vectors; run on systems with ≥ 8 GB RAM for safety.
- **Compiler Issues:** Use `g++` with `-std=c++11` or higher.

---

## 🏁 Final Notes

- This code is optimized for speed and handles dense, large-scale grid computations efficiently.
- Designed for Kriti 2025: Hostel Code 90.
- For any further queries or debugging help, raise an issue in the repository.
