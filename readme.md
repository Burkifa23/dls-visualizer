# Depth-Limited Search (DLS) Visualizer

This document provides a detailed technical explanation of **Depth-Limited Search (DLS)** as implemented in **`dls-visualizer.html`** for solving the Ghana Route-Finding Problem.

---

## What is Depth-Limited Search?

**Depth-Limited Search (DLS)** is an uninformed (blind) search strategy designed to address the infinite loop vulnerability of standard **Depth-First Search (DFS)** in infinite or cyclic graphs. 

It accomplishes this by imposing a strict limit (L) on the maximum path depth it will explore:

1. **DFS Foundation**: It uses a stack-based, LIFO (Last-In, First-Out) exploration pattern to keep memory consumption low.
2. **Strict Boundary Condition**: Any branch that reaches a depth equal to the limit L is immediately pruned (stopped from expanding further), regardless of whether it has reached a leaf node.
3. **Completeness & Optimality**: Unlike standard DFS (which is incomplete on infinite spaces), DLS is complete if the depth limit L is set greater than or equal to the goal depth (L \ge d). However, it is not guaranteed to be optimal since it might find a deeper path before a shallower one, depending on the expansion order.

---

## Step-by-Step Algorithm Mechanics

DLS runs a single depth-bounded DFS traversal starting from the start city:

1. **Stack Initialization**: Push the start city onto the stack with a depth of 0 and path cost of 0.
2. **Node Evaluation**:
   * Pop the top node from the stack.
   * If the node is the destination (goal), terminate and return the successful path.
   * If the node's depth equals the limit L, do not expand its children. Record a `⊘ LIMIT REACHED` event and continue to the next stack element.
3. **Expansion**:
   * If the depth is less than L, retrieve the node's neighbors (successors).
   * Push unvisited neighbors onto the stack, incrementing their depth by 1 and adding edge weights to path costs.
4. **Search Exhaustion**:
   * If the stack becomes empty and the goal was not found:
     * If at least one branch was pruned due to the depth limit, DLS terminates with a `cutoff_fail` (the goal was not found within L steps, but might exist deeper).
     * If no branches hit the limit, DLS terminates with an `absolute_fail` (the entire graph was searched and no path exists).

---

## Visualizing the Ghana Road Network with DLS

In the visualizer, you can select a **Start City** (e.g., **Tamale**), a **Destination City** (e.g., **Korle Bu**), and a **Strict Depth Edge Limit** (e.g., 3 edges).

Here is a trace of the execution under L = 3:
* **Depth 0**: Tamale is expanded. Its neighbors Wa, Bolgatanga, Yendi, Kintampo, and Techiman are pushed onto the stack at Depth 1.
* **Depth 1**: Techiman is popped. Since its depth (1) is less than the limit (3), it is expanded, pushing Sunyani and Kumasi at Depth 2.
* **Depth 2**: Kumasi is popped. Since its depth (2) is less than the limit (3), it is expanded, pushing Koforidua and Cape Coast at Depth 3.
* **Depth 3**: Koforidua is popped. Since its depth (3) is equal to the limit (3), it is pruned (cutoff). The search backtracks to Cape Coast, which is also at Depth 3 and is pruned.
* **Result**: If the goal (e.g., Korle Bu) resides at a depth greater than 3 along the explored branches, DLS will fail to find it, yielding a `⊘ LIMIT REACHED` cutoff failure.

---

## Complexity Analysis

### 1. Space Complexity
DLS retains the space-efficiency profile of DFS. Because it only tracks the active search path and its sibling branches up to depth L:

\[O(b \cdot L)\]
where:
* b: average branching factor (\approx 3 to 5 in Ghana).
* L: chosen depth limit.

This linear space consumption is why DLS serves as the foundation for Iterative Deepening Search (IDS).

### 2. Time Complexity
In the worst case, the algorithm may explore all nodes down to the depth limit L:

\[O(b^L)\]
If L is set much larger than the depth of the shallowest solution (L \gg d), DLS will perform unnecessary exploration, leading to significant time overhead.

---

## Visualization State System

The visualizer shows the active execution states of DLS in real-time:
* 🔘 **Slate Gray (`#cbd5e1`)** — Unvisited cities.
* 🔵 **Soft Blue (`#74ade8`)** — Active stack search branch.
* 🔴 **Crimson Red (`#ef4444`) with shadow glow** — Limit Cutoff Node (node at max depth L where search was pruned).
* 🟢 **Emerald Green (`#10b981`)** — Final resolved route.
* **Execution Logs** — Real-time tracking of stack pops, node expansions, depth alerts, and search outcomes.
