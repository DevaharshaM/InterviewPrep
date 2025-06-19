# Data Structures in C 

The data structures help solve problems efficiently and provide a solid foundation for systems programming and embedded development. Commonly used data structures are:

---

## 1. Linked List

A **linked list** is a linear collection of nodes where each node contains data and a pointer to the next node.

### Types:
- **Singly Linked List** – each node points to the next
- **Doubly Linked List** – nodes have both next and previous pointers
- **Circular Linked List** – last node links back to the first

### Key Concepts:
- Nodes are dynamically allocated.
- No fixed size; grows as needed.
- Access is sequential, not random.

### Use Cases:
- Implementing dynamic stacks and queues
- Memory-efficient insertion/deletion
- Undo functionality, playlists, hash chains

---

## 2. Stack

A **stack** is a linear data structure that follows the **LIFO** (Last In, First Out) principle.

### Key Concepts:
- Only the top element is accessible.
- Commonly implemented using arrays or linked lists.
- Recursion and function calls internally use a call stack.

### Use Cases:
- Backtracking (e.g., maze solving, recursion)
- Expression evaluation (postfix, prefix)
- Undo operations in editors

---

## 3. Queue

A **queue** follows the **FIFO** (First In, First Out) principle. Elements are added at the rear and removed from the front.

### Types:
- **Simple Queue** – linear FIFO
- **Circular Queue** – wraps around using modulo logic
- **Deque (Double-ended Queue)** – insertion/deletion from both ends
- **Priority Queue** – elements removed based on priority, not just order

### Key Concepts:
- Implemented using arrays or linked lists.
- Efficient for buffering and scheduling.

### Use Cases:
- Task scheduling
- Print queues, job queues
- Breadth-first search (BFS) in graphs

---

## 4. Tree

A **tree** is a hierarchical data structure with a root node and children.

### Key Concepts:
- Nodes connected in a parent-child relationship.
- No cycles or loops (unlike graphs).
- Recursive in nature — each subtree is itself a tree.

### Use Cases:
- Representing hierarchical data (e.g., file systems)
- Expression trees in compilers
- Decision trees in AI

### a) Binary Tree

A **binary tree** is a special tree where each node has at most two children: left and right.

### Variants:
- **Binary Search Tree (BST)** – left < root < right
- **AVL Tree** – self-balancing BST
- **Heap** – complete binary tree used in priority queues

### Traversals:
- **Inorder** – left, root, right
- **Preorder** – root, left, right
- **Postorder** – left, right, root

### Use Cases:
- Efficient searching and insertion (in BST)
- Priority scheduling (in heaps)
- Syntax trees in interpreters and compilers

---

## 5. Graph

A **graph** is a non-linear structure made of **nodes (vertices)** and **edges**.

### Key Concepts:
- Can be **directed** or **undirected**
- May be **weighted** or **unweighted**
- Represented using adjacency matrix or list

### Use Cases:
- Routing algorithms (GPS, networks)
- Social network connections
- Dependency resolution (e.g., package managers)

---

# Summary

| Structure     | Real World Analogy     | Key Feature         |
|---------------|------------------------|----------------------|
| Linked List   | Train with coaches     | Dynamic size         |
| Stack         | Plates in a stack      | LIFO                 |
| Queue         | Ticket line            | FIFO                 |
| Tree          | File directory         | Hierarchical         |
| BST           | Dictionary             | Sorted + fast lookup |
| Heap          | Task prioritization    | Min/Max property     |
| Graph         | Road map / Network     | Flexible connections |
