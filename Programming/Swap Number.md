# Time and Space Complexity in C 

Time and space complexity are foundational concepts in computer science. This estimates how good a program or algorithm is.

---

## What is Time Complexity?

Time complexity describes how the **execution time** of an algorithm grows with respect to the size of the input `n`.

Rather than measuring actual seconds, we describe the number of fundamental operations (comparisons, assignments, etc.) the algorithm performs.

---

## What is Space Complexity?

Space complexity describes how much **extra memory** (RAM or stack) an algorithm needs as the input size grows. This includes:

- Temporary variables
- Recursion stack
- Extra data structures (arrays, queues, etc.)

Space complexity is especially important in **embedded systems**, **low-memory environments**, and **recursive algorithms**.

---

## Why Analyze Complexity?

- To choose the **most efficient** algorithm for a task
- To understand how your program will **scale** with more data
- To meet performance and memory constraints
- To compare two solutions **objectively**, without benchmarking

---

## Notations Used

There are four main asymptotic notations:

| Notation       | Describes             | Example Meaning                              |
|----------------|------------------------|----------------------------------------------|
| **O (Big O)**  | Worst-case time/memory | Algorithm takes **at most** this many steps  |
| **Ω (Omega)**  | Best-case scenario     | Algorithm takes **at least** this many steps |
| **Θ (Theta)**  | Tight bound            | Algorithm always takes exactly this many steps|
| **o (little o)** | Non-tight upper bound | Used for theoretical comparison only         |

---

### Why use Big O notation?

- It describes the **worst-case performance**, which is often the most important in practice
- It’s simple, practical, and standard across interviews and industry
- It ensures the code performs well under the most demanding inputs

---

## Common Complexity Classes

| Complexity     | Description                              | Example Scenarios                           |
|----------------|------------------------------------------|---------------------------------------------|
| **O(1)**       | Constant time                             | Accessing an element in an array            |
| **O(log n)**   | Logarithmic time                          | Binary search                                |
| **O(n)**       | Linear time                               | Loop through array, string comparison        |
| **O(n log n)** | Log-linear time                           | Merge sort, quicksort (average case)         |
| **O(n²)**      | Quadratic time                            | Nested loops (e.g., bubble sort)             |
| **O(2ⁿ)**      | Exponential time                          | Solving Tower of Hanoi, brute-force recursion|
| **O(n!)**      | Factorial time                            | Generating all permutations (e.g., TSP)      |
