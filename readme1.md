# Ghana Route-Finding Algorithmic Visualizer Suite

An interactive, highly performant, and fully responsive web application suite engineered to visualize classic and advanced Artificial Intelligence search algorithms. This suite solves the **Ghana Route-Finding Problem** using a localized graph network of transit points across Ghana, projecting spatial coordinates dynamically on a responsive canvas.

---

## 🚀 Core Features

* **Responsive Vector Projection Engine:** Automatically maps topological coordinates into fluid percentage layout markers, adapting perfectly across desktop, tablet, and mobile views.
* **Mathematical Execution Logs:** Exposes real-time step-by-step algorithm choices, explicitly printing path metrics (g(n)), straight-line heuristics (h(n)), and final evaluation scores (f(n)).
* **State-Isolation Architecture:** Built using specialized JavaScript **Generator Functions (`function*`)** to step through graphs incrementally without memory bloat, high execution overhead, or recursive call stack lock-ups.
* **Strict Design System Palette:**
    * 🔵 **Electric Blue (`#2979FF`)** — Frontier Queue / Search Boundary
    * 🟡 **Gold (`#D4AF37`)** — Explored / Closed Set
    * 🔴 **Crimson (`#FF3366`)** — Final Resolved Path / Cutoff Alerts
    * ⚫ **Charcoal (`#333`/`#111`)** — Base Infrastructure Layout

---

## 🧠 Supported Search Algorithms

The suite features separate dedicated visualization architectures engineered to show the native quirks of each strategy:

| Algorithm Class | Strategy Type | Visual Characteristic / Focus |
| :--- | :--- | :--- |
| **Uninformed / Blind** | Breadth-First Search (BFS) | Layer-by-layer uniform radial wave expansions. |
| | Depth-First Search (DFS) | Aggressive single-branch lunges deep into nodes. |
| | Depth-Limited Search (DLS) | Truncated DFS paths restricted by edge counts (L). |
| | Iterative Deepening (IDS) | Periodic complete graph resets with rising limits. |
| | Uniform-Cost Search (UCS) | Path cost optimization sorting solely by g(n). |
| **Informed / Heuristic** | Greedy Best-First Search | Pure look-ahead estimation matching h(n) targets. |
| | A\* Search | Optimal shortest path tracking combining g(n) + h(n). |
| | Weighted A\* | Accelerated target targeting utilizing g(n) + W \times h(n). |
| | Beam Search | Memory-restricted exploration capping the frontier width (k=2). |
| | Recursive Best-First (RBFS) | Linear space memory "yo-yo" backtracking via f-limits. |
| | Iterative-Deepening A\* (IDA\*) | Successive total cost bounding iterations. |
| | Simplified Memory-Bounded (SMA\*)| Strict leaf-node evictions and cost backups. |
| | Bidirectional Heuristic Search | Concurrent Forward and Backward frontiers meeting in-graph. |

---

## 🛠️ Architecture & System Design

Standard queue-based visualizers often fail when tackling memory-bounded or deeply recursive algorithms. This suite solves that problem by split-building complex handlers:

1.  **The Universal Engine Matrix:** Standard queue visualizers (BFS, DFS, UCS, GBFS, A\*) share a high-performance priority-array processor. The chosen strategy simply intercepts the sorting and slicing steps on each cycle tick.
2.  **Explicit Memory Virtualization:** Advanced strategies like **RBFS**, **SMA\***, and **IDA\*** simulate nested frame boundaries using localized javascript stacks and maps rather than leveraging native runtime engines, ensuring you see precise memory drops and value backups frame-by-frame.

---

## 📦 Installation & Usage Instructions

The entire system is written in native web standard formats without external compiler tools, frameworks, or package dependencies. 

1. Save any visualizer module file directly locally (e.g., `visualizer.html`, `rbfs_visualizer.html`).
2. Open the module directly inside any modern layout browser engine (Chrome, Safari, Firefox, Edge).

```bash
# Clone or move into your target workspace directory
cd ghana-route-visualizer

# Run a localized lightweight server or open the standalone files instantly
open visualizer.html
```

| File Name | Targeted Algorithm(s) | Operational Mechanism / Special Elements Tracked |
| :--- | :--- | :--- |
| **`visualizer.html`** | • Breadth-First Search (BFS)<br>• Depth-First Search (DFS)<br>• Uniform-Cost Search (UCS)<br>• Greedy Best-First Search<br>• A\* Search Strategy<br>• Weighted A\* (W=2)<br>• Beam Search Limit (k=2) | **The Master Queue Engine:** Runs all algorithms that fit seamlessly into a singular flat priority array list loop (`while frontier.length > 0`). The strategy type determines queue sorting and slicing dynamically. |
| **`dls_visualizer.html`** | • Depth-Limited Search (DLS) | **Explicit Depth Interception:** Tracks edge counts per branch node and explicitly yields a truncated `⊘ CUTOFF` event when hitting the limit. |
| **`ids_visualizer.html`** | • Iterative Deepening Search (IDS) | **Recursive Step Simulator:** Systematically forces complete graph wipes and resets every time the edge limit increment matches a new depth level. |
| **`rbfs_visualizer.html`** | • Recursive Best-First Search (RBFS) | **Virtual Recursion Stack:** Renders a visual sidebar of the active call stack while actively stepping through f-limit comparisons and parent tracking score updates. |
| **`idastar_visualizer.html`** | • Iterative-Deepening A\* (IDA\*) | **Dynamic Threshold Adjuster:** Combines A\* scores with IDS structure, shifting the max cost boundary box up on every full iteration loop. |
| **`sma_star_visualizer.html`** | • Simplified Memory-Bounded A\* (SMA\*) | **Allocation Cache Controller:** Features a live structural memory meter panel that actively showcases leaf-node evictions and cost value backups to parent nodes. |
| **`bidirectional_visualizer.html`** | • Bidirectional Heuristic Search | **Dual Concurrent Frontiers:** Alternates clock ticks between a Forward Queue (Electric Blue) and a Backward Queue (Safety Orange), tracking their physical collision meeting point. |

_Made With Gemini_
